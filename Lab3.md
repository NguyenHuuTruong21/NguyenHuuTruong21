# 1. Hỗ trợ tìm kiếm các transactions

Cải tiến trong lớp BankStatementProcessor:

+ Tìm kiếm theo khoản tiền (amount)

+ Tìm kiếm theo khoảng thời gian (date range)

+ Tìm kiếm theo mô tả (description)

#  2. Hỗ trợ các định dạng dữ liệu vào khác nhau

Thiết kế lại hệ thống Parser

Tạo Interface BankStatementParser làm trung gian giữa các định dạng (CSV, JSON, XML).

Triển khai từng lớp Parser riêng biệt, ví dụ:

+ BankStatementCSVParser xử lý file CSV.
+ BankStatementJSONParser xử lý file JSON.
+ BankStatementXMLParser xử lý file XML.

# 3. Hỗ trợ xuất kết quả theo các định dạng khác nhau

Thiết kế hệ thống Exporter

Tạo Interface ResultExporter để chuẩn hóa các định dạng xuất dữ liệu.

Triển khai các lớp cụ thể:

HTMLResultExporter: Xuất dữ liệu dưới dạng HTML.

JSONResultExporter: Xuất dữ liệu dưới dạng JSON.

PlainTextResultExporter: Xuất dữ liệu dạng văn bản thông thường.

# 4. Xử lý lỗi

Các lỗi cần xử lý:

File không tồn tại hoặc không hợp lệ.

Lỗi định dạng dữ liệu (CSV, JSON, XML).

Giá trị không hợp lệ (ví dụ: số âm, ngày sai).

Cách xử lý:

Dùng các khối try-catch để xử lý lỗi cục bộ.

Sử dụng IllegalArgumentException hoặc tự định nghĩa Exception mới.

Ghi log lỗi và hiển thị thông báo cho người dùng.


    // Domain Class
    class BankTransaction 
    {
        private final LocalDate date;
        private final double amount;
        private final String description;

      public BankTransaction(LocalDate date, double amount, String description) 
      {
          this.date = date;
          this.amount = amount;
          this.description = description;
      }
  
      public LocalDate getDate() 
      {
          return date;
      }
  
      public double getAmount() 
      {
          return amount;
      }
  
      public String getDescription() 
      {
          return description;
      }

      @Override
      public String toString() 
      {
          return "BankTransaction{" +
                  "date=" + date +
                  ", amount=" + amount +
                  ", description='" + description + '\'' +
                  '}';
      }
    }
    
    // Parsing Interface
    interface BankStatementParser 
    {
        BankTransaction parseFrom(String line);
        List<BankTransaction> parseLinesFrom(List<String> lines);
    }

    // CSV Parser Implementation
    class BankStatementCSVParser implements BankStatementParser 
    {
        private static final DateTimeFormatter DATE_PATTERN = DateTimeFormatter.ofPattern("dd-MM-yyyy");

    @Override
    public BankTransaction parseFrom(String line) 
    {
        String[] columns = line.split(",");
        LocalDate date = LocalDate.parse(columns[0], DATE_PATTERN);
        double amount = Double.parseDouble(columns[1]);
        String description = columns[2];
        return new BankTransaction(date, amount, description);
    }
  
      @Override
      public List<BankTransaction> parseLinesFrom(List<String> lines) 
      {
          return lines.stream()
                  .map(this::parseFrom)
                  .collect(Collectors.toList());
      }
    }

    // JSON Parser Implementation
    class BankStatementJSONParser implements BankStatementParser 
    {
      @Override
      public BankTransaction parseFrom(String line) {
          // Example JSON: {"date":"2023-11-01","amount":100.5,"description":"Groceries"}
          String[] parts = line.replace("{", "").replace("}", "").replace("\"", "").split(",");
          LocalDate date = LocalDate.parse(parts[0].split(":")[1]);
          double amount = Double.parseDouble(parts[1].split(":")[1]);
          String description = parts[2].split(":")[1];
          return new BankTransaction(date, amount, description);
      }

      @Override
      public List<BankTransaction> parseLinesFrom(List<String> lines) 
      {
          return lines.stream()
                  .map(this::parseFrom)
                  .collect(Collectors.toList());
      }
    }

    // XML Parser Implementation
    class BankStatementXMLParser implements BankStatementParser 
    {
        @Override
        public BankTransaction parseFrom(String line) {
            // Example XML: <transaction><date>2023-11-01</date><amount>100.5</amount><description>Groceries</description></transaction>
            String date = line.split("<date>")[1].split("</date>")[0];
            String amount = line.split("<amount>")[1].split("</amount>")[0];
            String description = line.split("<description>")[1].split("</description>")[0];
            return new BankTransaction(LocalDate.parse(date), Double.parseDouble(amount), description);
        }

    @Override
    public List<BankTransaction> parseLinesFrom(List<String> lines) 
    {
        return lines.stream()
                .map(this::parseFrom)
                .collect(Collectors.toList());
      }
    }

    // Processor
    class BankStatementProcessor 
    {
        private final List<BankTransaction> bankTransactions;

    public BankStatementProcessor(List<BankTransaction> bankTransactions) 
    {
        this.bankTransactions = bankTransactions;
    }

    public double calculateTotalAmount() 
    {
        return bankTransactions.stream()
                .mapToDouble(BankTransaction::getAmount)
                .sum();
    }

    public List<BankTransaction> searchTransactions(String criteria) 
    {
        return bankTransactions.stream()
                .filter(tx -> tx.getDescription().toLowerCase().contains(criteria.toLowerCase()))
                .collect(Collectors.toList());
        }
    }

    // Exporter Interface
    interface BankStatementExporter {
        void export(List<BankTransaction> transactions, String outputPath) throws IOException;
    }

    // HTML Exporter Implementation
    class HTMLBankStatementExporter implements BankStatementExporter {
        @Override
        public void export(List<BankTransaction> transactions, String outputPath) throws IOException {
            StringBuilder html = new StringBuilder();
            html.append("<html><body><table border='1'>")
                .append("<tr><th>Date</th><th>Amount</th><th>Description</th></tr>");
            for (BankTransaction tx : transactions) {
                html.append("<tr>")
                    .append("<td>").append(tx.getDate()).append("</td>")
                    .append("<td>").append(tx.getAmount()).append("</td>")
                    .append("<td>").append(tx.getDescription()).append("</td>")
                    .append("</tr>");
            }
            html.append("</table></body></html>");
            Files.write(Paths.get(outputPath), html.toString().getBytes());
        }
    }

    // Analyzer
    class BankStatementAnalyzer {
    private static final String RESOURCES = "src/main/resources/";

    public void analyze(String fileName, BankStatementParser parser, BankStatementExporter exporter, String outputPath) 
    {
        try {
            Path path = Paths.get(RESOURCES + fileName);
            List<String> lines = Files.readAllLines(path);
            List<BankTransaction> transactions = parser.parseLinesFrom(lines);

            BankStatementProcessor processor = new BankStatementProcessor(transactions);
            System.out.println("Total Amount: " + processor.calculateTotalAmount());

            List<BankTransaction> groceries = processor.searchTransactions("Groceries");
            System.out.println("Groceries Transactions: " + groceries);

            exporter.export(transactions, outputPath);
            System.out.println("Exported to: " + outputPath);
        } catch (IOException e) {
            System.err.println("Error: " + e.getMessage());
        }
      }
    }

# Biểu đồ các lớp:

  ![PlantText](https://www.planttext.com/api/plantuml/png/r5PBRjim4Dth55owW7s3meYIA0W2sp4ijIXG5CM4OXoY52cGew0Vz6HTz4YzGYcAj6HzZ6GHfDL24kRpvirmPgG_ltwV6GIDLI4YAi0OSWxoIwP16g38bIG_8cAl1Laf2k8Ia97SthmmLzMTO0GALKdqiXGrbtkICqCrBsiCfo1zvDanulmOR3w2yyO3jOvxXlLp5ZGUmefZXt9GUB3QliNhQr4rBrR-CuguHARlWJ97F4KRfs0Ijw0DqxuiWwH8MQklj2fc7bHmoGx4kS6tFOzbuxAoPiRvEQF6UUcyZQFJdiw1oaNwthFXHIcSo9mWko1rhJ9Ui2kb2q2R7hcCi-JpDiwoPBVv1pAwIMytpqdfTTb-MA_-7x9RhIWpHhNTC1xWxbXWEjI7MBEdOVJ6qqulhKJTYmf1z2Pr7D4mqFIXYnbAPeVPDZA7KpERV2sLniv1F2gU4-Qa4obW9zHX5waAoyeUAZvqgdoThLVZqQQwuaNf74MA9OXltpiRm2vxv3G0x9Bqzjtk8acxFA3n2VMzvu9jeB3xUQopNJlg-KH-pB-SPhm6BkEo59n2vuj30bT7gh0sdj77JmJqlkdpYNMuM2p7s4PJk-P9zksqJvbFTyB08sYYyUCQHWWJ5qqCTV3eT4tKB-m0DSIBpfZCwr-0lm000F__0m00)
