# Phân tích Use Case: Maintain Timecard
Mô tả ca sử dụng:
Maintain Timecard là một ca sử dụng trong hệ thống Payroll System, cho phép quản lý thông tin về thời gian làm việc của nhân viên. Đây là một chức năng quan trọng giúp đảm bảo việc ghi nhận và xử lý tiền lương được chính xác.

Các bước phân tích:
Tác nhân chính:

Employee: Người nhập và kiểm tra thông tin về thời gian làm việc.
Manager/HR: Người xác minh và duyệt thông tin thời gian làm việc.
Tiền điều kiện:

Nhân viên hoặc quản lý phải đăng nhập thành công vào hệ thống.
Thông tin nhân viên đã được lưu trong hệ thống.
Luồng sự kiện chính:

Nhân viên chọn chức năng "Maintain Timecard".
Nhập thông tin thời gian làm việc (ngày, giờ bắt đầu, giờ kết thúc, v.v.).
Hệ thống xác nhận và lưu trữ thông tin vào cơ sở dữ liệu.
Quản lý hoặc HR xác minh thông tin và phê duyệt nếu hợp lệ.
Luồng sự kiện phụ (xử lý lỗi):

Nếu thông tin nhập sai (thời gian kết thúc trước thời gian bắt đầu): Thông báo lỗi.
Nếu không có quyền truy cập: Hiển thị thông báo không có quyền.
Hậu điều kiện:

Thông tin thời gian làm việc được lưu thành công và sẵn sàng để xử lý lương.


# Viết code Java mô phỏng ca sử dụng Maintain Timecard.

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
