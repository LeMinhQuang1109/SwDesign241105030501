# Lab 1 - Kết quả bài thực hành
## 1.Phân tích kiến trúc
- Kiến trúc đề xuất: Kiến trúc Microservices  
- Lý do đề xuất:  
  + Tách biệt chức năng: Mỗi dịch vụ (như Payroll Service, Payment Service, v.v.) xử lý một nhiệm vụ riêng, dễ duy trì và phát triển mà không ảnh hưởng đến các phần khác.
  + Dễ mở rộng: Nếu công ty phát triển, chúng ta chỉ cần mở rộng dịch vụ nào cần thiết thay vì phải thay đổi toàn bộ hệ thống.
  + Tích hợp với hệ thống cũ: Vì Acme cần sử dụng cơ sở dữ liệu cũ (DB2), chúng ta có thể tạo một dịch vụ riêng (Project Service) để lấy dữ liệu từ DB2, giúp hệ thống Payroll hoạt động tốt mà không cần thay đổi DB2.
  + Bảo mật và tính linh hoạt: Kiến trúc này cho phép kiểm soát quyền truy cập theo từng dịch vụ, bảo vệ dữ liệu nhạy cảm, và điều chỉnh linh hoạt các thành phần khi cần thiết.
  
## Biều đồ package mô tả kiến trúc:
![Diagram](https://www.planttext.com/api/plantuml/png/V98z3i8m38NtdCBA10CB8mC210C34kBd02Or26XI50T4XJWP0qVY2YIb5KgfoERdxoNFLbwFvu0TMdVMgJYXEkAEGCunjrcQmZ9dHrh2JO0_lssobxqY2SXGQgLKusrs8ELY_gCryvXhCgv-Vz0Q-TLUaqARH8PAh1ntyPrlSdLa3LO3yk-4PU8P6byNOSReS8DCq1gFkf0Pc8vcxU8bNuVRumr0fzElXOOUo3KJooQq5lSl6-yke4EbY3rUjOgqtXk3mHl2UyE2CE62WgtDj1G3Cadu0-8D003__mC0)

## 2.Cơ chế phân tích
- Bảo mật dữ liệu: Do hệ thống xử lý thông tin lương của nhân viên, cần cơ chế mã hóa dữ liệu và quyền truy cập an toàn.  
- Giao tiếp, tích hợp với cơ sở dữ liệu cũ (DB2): Dịch vụ cần phải đảm bảo kết nối an toàn và hiệu quả với DB2 để truy xuất thông tin về dự án và mã chi phí mà không làm ảnh hưởng đến hệ thống cũ.  
- Cơ chế quản lý thanh toán: Đảm bảo tính toán chính xác và đúng hạn cho mỗi nhân viên với các phương thức thanh toán khác nhau, như chuyển khoản ngân hàng, phát hành séc, hoặc thanh toán qua ví điện tử.  
- Đồng bộ hóa dữ liệu: Đảm bảo rằng thông tin thời gian làm việc và dự án của nhân viên được cập nhật kịp thời để tính lương chính xác, ngay cả khi có các thay đổi từ hệ thống DB2 hoặc dữ liệu mới từ nhân viên.

## 3.Phân tích ca sử dụng Payment
- PaymentController: Quản lý giao diện người dùng và nhận yêu cầu thanh toán.  
- PaymentService: Xử lý logic nghiệp vụ liên quan đến thanh toán, xác định phương thức thanh toán.  
- Employee: Đại diện cho nhân viên; có các thuộc tính liên quan như ID, tên, và thông tin phương thức thanh toán.  
- PaymentMethod: Lưu thông tin về các phương thức thanh toán, như chuyển khoản, séc, ví điện tử.  
- PaymentRepository: Quản lý dữ liệu liên quan đến thanh toán, lưu trữ và truy xuất thông tin từ cơ sở dữ liệu.
## Biểu đồ Sequence cho Ca Sử Dụng Payment:
![Diagram](https://www.planttext.com/api/plantuml/png/b58zIiH05EvpYky2Uu4KDejWeI3-W9Rhx622sJVPP198RM6nM7W2Dug82wA5LQROOYJtc1Du1LzYH2L1j9d7FERxUT-RDxC-J6M2qGPs9yLCaXuhqecA8fduEBQh3C9Lztm6pbmIug1-haiwXURxW-0oeG1QsPAy7i4trdsPvA6GFiP_vkaW3SdcB8vK8Hc-xQgxWb_RbmOR4YYmDuGyjAiXODVPaJfGKnz7jXHulN9cmMB_iz1rzcIiqb2hfE1HNFKOim4k-ZSsv7Qf8EeIgJFNc3hpX2XqvYBpUgmO3MJMscvrgDd6boZdi6GLqQJHypoyqeEFw4vigN3cghN6F7FLxT3ocA3v6pwssEmvjPCjFhDl2NxeU-y0003__mC0)  

## 4.Phân tích ca sử dụng Maintain Timecard
- TimecardController: Nhận yêu cầu từ người dùng để ghi nhận giờ làm việc.  
- TimecardService: Xử lý logic ghi nhận thời gian làm việc.  
- Employee: Đại diện cho nhân viên và chứa dữ liệu chấm công.  
- Project: Lưu thông tin dự án mà nhân viên đang làm.  
- TimecardRepository: Tương tác với cơ sở dữ liệu để lưu thông tin chấm công.
## Biểu Đồ Sequence cho Ca Sử Dụng Maintain Timecard
![Diagram](https://www.planttext.com/api/plantuml/png/T98nJiCm68Ntdk9Te1Vem88G30m8YiGQN2inf7Pnd4YP6HWuGqK2GaYLAa1YYeSEbdeFdu0hy8SG0OgxsdxVU__x_MatvndN6EzXAkQSHNgshwJHAasvdk3GsxL0wLOvc6zUSiI9W4nyivOmYRTBWLX44gchvYY4jtTiDEJyfPznNGZ62VrBYacu339-NhU0W_aYLIKdvR5ldakoTnyoXX6ICEvHajIjP4XvejKLPoOWd7dx3bTJ_bQBcpmA0lgZKxvGcJ1AbyJQlkMxAa3XAWMshP5v-z2wl983tUIZ8GhZK3iNhcPzFMbdvIgPWBNPXnbth6_QZNhfQeLhtsmCZUYRf-2A2D7-X0cEAEbjjzxxlgnlmhy8Nm000F__0m00)  

## 5.Hợp nhất kết quả phân tích  
- Kết quả hợp nhất tạo nên một hệ thống Payroll System với các lớp phân tích chính, bao gồm các lớp cho xử lý thanh toán và ghi nhận thời gian làm việc của nhân viên, quản lý dữ liệu nhân viên và tương tác với cơ sở dữ liệu. Hệ thống này bao gồm các lớp Controller, Service, Entity, và Repository với các nhiệm vụ cụ thể, đảm bảo tính chính xác và an toàn trong xử lý nghiệp vụ lương.
  + Tính nhất quán: Các lớp Service đóng vai trò thực thi nghiệp vụ, đảm bảo dữ liệu trong Employee và các thực thể liên quan luôn chính xác.  
  + Phân tách chức năng: Mỗi lớp Controller, Service và Repository xử lý một chức năng riêng biệt, từ giao diện người dùng đến quản lý dữ liệu, giúp hệ thống dễ duy trì và mở rộng.  
  + Kết nối chặt chẽ: Employee liên kết với các lớp như PaymentMethod và Project để lưu giữ thông tin cần thiết, từ đó thực hiện chính xác các nghiệp vụ thanh toán và chấm công.

## Biểu đồ lớp hợp nhất:
![Diagram](https://www.planttext.com/api/plantuml/png/f5DBJiCm4Dtd55PN8BKNo09r0GiMe8fmWP4pQWnsRDcJIXRgoLXm9Aw0qtom4mkfmYjdvisRzsQSxy-llIEmr2bP6E3lS4Hs06-rb9LtX8fz52mSBi4vzg2Cr1vn30xdyRvaegKeqeB2abLaHNkCmWQymfQUa1fTbtsRtyy8Ha8X1niGh-FjaZmNaP2aDb53tkHwrqWWf4ioAQFLRyWfuJ93h3UuDZFadfTMSp8hj2V1qwavbA4yyN4pZNUR-hjT4q-JoJ5RvDhMFI8c7EHkMQCxwouBoz2ERL_GQ2T8MvzAXXF-L_0Vr1Fa2jNpUzpjxXPlecIR1jnc3PlQ98Z5eYAwI70ew1oE5SiDnDJNr4plBW21StGpE2Dfzh42vvZpw7EnnxRkV_SV0000__y30000)
