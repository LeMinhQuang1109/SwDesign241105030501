# Kết quả Lab4:
## I. Ca sử dụng: Maintain Timecard
### 1. Mô tả sự tương tác giữa các đối tượng thiết kế
  - Tác nhân:
    + Employee (Nhân viên): Nhân viên nhập giờ làm việc vào hệ thống.
    + ProjectManager (Quản lý dự án): Người xem xét và phê duyệt Timecard đã gửi.
  - Các đối tượng chính trong hệ thống:
    + TimecardForm: Giao diện nhập liệu và gửi thông tin giờ làm việc.
    + TimecardService: Xử lý logic liên quan đến Timecard.
    + Database: Lưu trữ và quản lý dữ liệu Timecard.

### 2. Sơ đồ trình tự đơn giản hóa
![Diagram](https://www.planttext.com/api/plantuml/png/V9BBIWCn68NtUOf_gOk-G1TIQhqKEcN05joccJ29J3939bFeKbouSEDUX1PnPy658CmWBYA-Hvx0Lp2ZqriGDo7yvoJdoo5VrNidrrZfGYG84vqgE19PaiueHPaRSy8pB3MCkA04g-WuLG9m3kF-d_8PLLDEQErejZks7jPuWlCVlTVTaKALNb2Y0onnJ0Lr4-S90uHMED0wSAbj639RBZE8kQtk8J5p0LEtlIPetAyjJMmRpcsrTFhRcWtsj7aIm59RlXBGjboa86nrn_VH2jkT3uCs36pvE8C8ImQvMH06XmohcCAm41EgSXG6qDgE6YbRFi3KLfU-Strn0t_gKAyaQ6Qh6z_hyGy-duir-pPXhzk8cfaN6OFcSkFpspfnBV2Dx6LugXVoSMiMheB8jL6usioy1dSh-_zP3TR4k7v__K3g2UfG6TNVx1i00F__0m00)

### 3. Hành vi lưu trữ
  - Timecard mới: Tạo bản ghi mới với thông tin nhân viên, ngày làm việc, và số giờ làm.
  - Timecard đã tồn tại: Cập nhật số giờ làm hoặc trạng thái của Timecard hiện tại.

### 4. Tinh chỉnh mô tả luồng sự kiện
  - Nhập giờ làm việc:
    + Nhân viên nhập mã  và số giờ làm việc qua TimecardForm.
    + TimecardService kiểm tra: Tính hợp lệ của mã dự án. Số giờ làm việc nhập vào.
    + Nếu hợp lệ, TimecardService lưu dữ liệu vào Database.
  - Gửi Timecard:
    + Nhân viên nhấn "Gửi" để hoàn tất.
    + TimecardService đánh dấu trạng thái Timecard là "Đã gửi".
    + Database cập nhật trạng thái và gửi thông báo đến ProjectManager.

### 5. Hợp nhất các lớp và hệ thống con
  - TimecardForm tập trung vào giao diện nhập liệu.
  - TimecardService đảm nhận toàn bộ logic nghiệp vụ.
  - Database chịu trách nhiệm lưu trữ dữ liệu.



## II. Ca sử dụng: Run Payroll
### 1. Mô tả sự tương tác giữa các đối tượng thiết kế
  - Tác nhân:
    + SystemClock: Xác định ngày trả lương.
    + Printer: In hóa đơn lương (pay slip).
    + BankSystem: Thực hiện giao dịch chuyển khoản lương.
  - Các đối tượng chính trong hệ thống:
    + PayrollService: Xử lý toàn bộ quy trình trả lương.
    + EmployeeRepository: Quản lý thông tin nhân viên.
    + TimecardRepository: Quản lý thông tin giờ làm việc.

### 2. Sơ đồ trình tự đơn giản hóa
![Diagram](https://www.planttext.com/api/plantuml/png/T951JiCm54JtESLSW0jaWQeq6oGMIEq5J6hLLfAVu7nNPCq9k0458IGaH2LO9OikZ7AFd80h44CBZKGtbgtvC_DiVxRRISN2iCspG2HS6CpgYcK-pOea3Sf1qOak1J4kH6sAB9j9izA9XAYmsuwcOi7YKbJVUXoDf4XG-XFkHNyQvnjDB4qG703Wv7JV4YBgcrV6nstVF5caVVi6DdtpWApRT6jQ1dkomHD78UR6rhYsVVF8OENUQGdM15Bkdh3IxdbOtHtcEfU9C8j3-s_btBsG0XTkJSTgphkDfscsZ2lhSOv2xIuOuenGAZrOx7zZ_c52J9Mj-_Q6aAfYoFkhdqXQ-C_w0W00__y30000)

### 3. Hành vi lưu trữ
  - Kết quả trả lương: Lưu vào cơ sở dữ liệu với trạng thái "Đã trả lương".
  - Trạng thái nhân viên: Đánh dấu nhân viên đã nhận lương trong kỳ trả lương.

### 4. Tinh chỉnh mô tả luồng sự kiện
  - Tính toán và trả lương:
    + PayrollService lấy danh sách nhân viên từ EmployeeRepository.
    + Kết hợp dữ liệu giờ làm từ TimecardRepository để tính toán:
      Lương cơ bản.
      Số giờ làm thêm.
      Phụ cấp và khấu trừ (nếu có).
  - In phiếu lương và chuyển khoản:
    + PayrollService gửi thông tin đến Printer để in phiếu lương.
    + Gửi dữ liệu đến BankSystem để thực hiện giao dịch chuyển khoản.

### 5. Hợp nhất các lớp và hệ thống con
  - PayrollService tích hợp xử lý toàn bộ logic:
    + Tính toán.
    + Tương tác với Printer và BankSystem.
  - Đơn giản hóa bằng cách tích hợp SystemClock vào PayrollService để quản lý lịch trả lương.
