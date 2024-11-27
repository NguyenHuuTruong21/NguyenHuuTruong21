## Tổng hợp các ca sử dụng chính:
- ### Employee
- ### Timecard
- ### Paycheck
- ### PurchaseOder
- ### ProjectManagementDatabase
- ### BankSystem
## *I.Phân tích tất cả các ca sử dụng còn lại trong hệ thống Payroll System.*
### *1. Paycheck (Bảng lương)*
### Bảng lương là kết quả của việc tính toán tiền lương dựa trên số giờ làm việc, lương cơ bản và các khoản hoa hồng. Bảng lương có thể được tạo và phân phối cho nhân viên vào các kỳ thanh toán định kỳ.
### Ca sử dụng:
- ### Run Payroll: Hệ thống tự động tính toán bảng lương cho tất cả nhân viên vào mỗi kỳ thanh toán (thứ Sáu hoặc cuối tháng). Hệ thống sử dụng thông tin từ bảng chấm công, đơn hàng mua (với nhân viên nhận hoa hồng), và các thông tin khác để tính toán.
- ### Generate Paycheck: Dựa trên các yếu tố như giờ làm việc, tỷ lệ lương, và hoa hồng (nếu có), hệ thống sẽ tạo bảng lương cho từng nhân viên và chuyển chúng đến hệ thống ngân hàng (cho các nhân viên chọn phương thức thanh toán chuyển khoản).
### Biểu đồ Sequence: 
![PlanText](https://www.planttext.com/api/plantuml/png/R94zJWD138NxEONBKEG2MwH9aA0YOYDHcrd3MfcVuF60zcmK78ahC9ja_nGwwytpzspFx_VFWTLH1JLzP0gMOCVuBkZXBGhiiRCjsQCnUnHbooSC2dMNbFn26erpyS2UB4gpT6QnBIPwaeR4c0jhlHcy5JoJ2jCdGPrVFQjICu66Ohsvz9tTMG8yn2m9Ng8SgHcPYwWPUD3X_91WrQ-wZTvpIXn32Rpt9nSxedHd5f2RtAaB7aF1UDHIJnDSprB15ftD3fN6Ky6g7zfrlG0m8vNCg-KcRkpzBsmOklnb6xycxuuKsINp1m00__y30000)
### *2. PurchaseOrder (Đơn hàng)*
### Đơn hàng là đối tượng được sử dụng bởi nhân viên có hoa hồng (Commissioned Employees) để ghi nhận các giao dịch bán hàng. Mỗi đơn hàng có thể được dùng để tính toán hoa hồng cho nhân viên.
### Ca sử dụng:
- ### Maintain Purchase Order: Nhân viên bán hàng có thể tạo, chỉnh sửa hoặc xóa các đơn hàng mà họ đã thực hiện trong hệ thống. Thông tin về khách hàng, sản phẩm bán, và ngày thực hiện sẽ được ghi lại.
- ### Calculate Commission: Các đơn hàng bán sẽ được dùng để tính hoa hồng cho nhân viên bán hàng. Tỷ lệ hoa hồng có thể dao động từ 10% đến 35% tùy theo chính sách của công ty.
### Biểu đồ Sequence: 
![PlanText](https://www.planttext.com/api/plantuml/png/f8wz3S8m44PxJt4Bi40AceIQI841JlO5Jl8VPoSIir4m4Yk055Caf03Hl_Uzxt6x7pXRgg2Zoq1U4pIC9q47VH1e1z5dJ0HxCIHAjIYPDKVq6UhW7AV4mPFPkMZ3bMW6lENYhl6RxGoge1R2JClk3FfmEXmB20rbP9kMmbhwrGg-Pt55dShcov_7Q7x-MPo_dquxHZq1003__mC0)
### *3. ProjectManagementDatabase (Cơ sở dữ liệu quản lý dự án)*
### Cơ sở dữ liệu này lưu trữ thông tin về các dự án, mã công việc, và các chi tiết liên quan. Các thông tin này sẽ được sử dụng trong bảng chấm công để phân bổ giờ làm việc cho các dự án cụ thể.
### Ca sử dụng:
- ### Maintain Timecard: Khi nhân viên ghi nhận giờ làm việc vào bảng chấm công, hệ thống sẽ lấy danh sách các mã công việc (charge number) từ cơ sở dữ liệu quản lý dự án để nhân viên có thể chọn mã phù hợp cho công việc mà họ đã làm.
### Biểu đồ Sequence: 
![PlanText](https://www.planttext.com/api/plantuml/png/V8p13O9G40NlLB4Dq0074YDN3L4QU7oVk8R_qMMXEG-MP0ic9XoCmUjaPbwFPwFUiv0ZxnDJe5IApX3bF9ZKDbmPV8U4Zf79ApXQZCoo6kOQz8RaqcXaW9s-u9zsyVDoLIhaG3VbJDbUO1rbFyMMDcQhILuktqyyMPBD3EtHzZ-JDm000F__0m00)
### *4. BankSystem (Hệ thống ngân hàng)*
### Hệ thống ngân hàng xử lý các giao dịch thanh toán cho nhân viên, đặc biệt là những nhân viên chọn phương thức thanh toán chuyển khoản trực tiếp.
### Ca sử dụng:
- ### Run Payroll: Sau khi tính toán bảng lương, hệ thống sẽ gửi thông tin thanh toán cho ngân hàng để xử lý các giao dịch chuyển khoản cho nhân viên chọn phương thức này.
- ### Process Payment: Hệ thống ngân hàng nhận thông tin từ hệ thống Payroll và thực hiện các giao dịch thanh toán cho nhân viên qua chuyển khoản ngân hàng.
### Biểu đồ Sequence: 
![PlanText](https://www.planttext.com/api/plantuml/png/X90x3i9034JxdC8b58YU8X8G2WgaY701Asl0Odzi7AISZO8ZSGMoV490I5Ih7StORtmzNpOicYPGqB4cMn9aZBk01hOkm0pjeMWg8PCaEGRXaZrQWONnsZL47-BJs9Vw-LTcb3wKk59JAP1ZOwWrhqZsJi4Wun3bZBohM60CAsJTFZcNXzeFaqTybBu6Jc0TsIk1gL8ix2ngMDgMts3ymI1M-Pmw_86J1tTYHNVeVhvR-6uJsQtgoFykUoVxs7DdjnnCDwOWgVsFUj--vw5QUt83003__mC0)
## *II. Mô phỏng Java cho ca sử dụng Maintain Timecard* 

```markdown

``` java

class Timecard {

    private String employeeId;
    private String date;
    private int hoursWorked;

    public Timecard(String employeeId, String date, int hoursWorked) {
        this.employeeId = employeeId;
        this.date = date;
        this.hoursWorked = hoursWorked;
    }

    public String getEmployeeId() {
        return employeeId;
    }

    public String getDate() {
        return date;
    }

    public int getHoursWorked() {
        return hoursWorked;
    }

    public String toString() {
        return "Timecard{" +
                "employeeId: '" + employeeId + '\'' +
                ", date: '" + date + '\'' +
                ", hoursWorked: " + hoursWorked +
                '}';
    }
}

class TimecardManager {

    private List<Timecard> timecards;

    public TimecardManager() {
        this.timecards = new ArrayList<>();
    }

    public void addTimecard(String employeeId, String date, int hoursWorked) {
        Timecard timecard = new Timecard(employeeId, date, hoursWorked);
        timecards.add(timecard);
        System.out.println("Timecard added: " + timecard);
    }

    public void updateTimecard(String employeeId, String date, int newHoursWorked) {
        for (Timecard timecard : timecards) {
            if (timecard.getEmployeeId().equals(employeeId) && timecard.getDate().equals(date)) {
                // Update the hours worked (for simplicity, we just remove and re-add)
                timecards.remove(timecard);
                addTimecard(employeeId, date, newHoursWorked);
                System.out.println("Timecard updated: " + timecard);
                return;
            }
        }
        System.out.println("Timecard not found for employeeId: " + employeeId + ", date: " + date);
    }

    public void deleteTimecard(String employeeId, String date) {
        for (Timecard timecard : timecards) {
            if (timecard.getEmployeeId().equals(employeeId) && timecard.getDate().equals(date)) {
                timecards.remove(timecard);
                System.out.println("Timecard deleted: " + timecard);
                return;
            }
        }
        System.out.println("Timecard not found for employeeId: " + employeeId + ", date: " + date);
    }

    public void displayTimecards() {
        System.out.println("Timecards:");
        for (Timecard timecard : timecards) {
            System.out.println(timecard);
        }
    }
}

public class Main {

    public static void main(String[] args) {
        TimecardManager manager = new TimecardManager();
        Scanner scanner = new Scanner(System.in);
        int choice;

        do {
            System.out.println("\n1. Add Timecard");
            System.out.println("2. Update Timecard");
            System.out.println("3. Delete Timecard");
            System.out.println("4. Display Timecards");
            System.out.println("5. Exit");
            System.out.print("Choose an option: ");
            choice = scanner.nextInt();

            switch (choice) {
                case 1:
                    System.out.print("Enter Employee ID: ");
                    String employeeId = scanner.next();
                    System.out.print("Enter Date (YYYY-MM-DD): ");
                    String date = scanner.next();
                    System.out.print("Enter Hours Worked: ");
                    int hoursWorked = scanner.nextInt();
                    manager.addTimecard(employeeId, date, hoursWorked);
                    break;
                case 2:
                    System.out.print("Enter Employee ID: ");
                    employeeId = scanner.next();
                    System.out.print("Enter Date (YYYY-MM-DD): ");
                    date = scanner.next();
                    System.out.print("Enter New Hours Worked: ");
                    int newHoursWorked = scanner.nextInt();
                    manager.updateTimecard(employeeId, date, newHoursWorked);
                    break;
                case 3:
                    System.out.print("Enter Employee ID: ");
                    employeeId = scanner.next();
                    System.out.print("Enter Date (YYYY-MM-DD): ");
                    date = scanner.next();
                    manager.deleteTimecard(employeeId, date);
                    break;
                case 4:
                    manager.displayTimecards();
                    break;
                case 5:
                    System.out.println("Exiting...");
                    break;
                default:
                    System.out.println("Invalid choice. Please try again.");
            }
        } 
        while (choice != 5);
        scanner.close();
    }
