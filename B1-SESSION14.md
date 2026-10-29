# Phần 1: Phân tích 


## 1. Mất vĩnh viễn nội dung quan trọng, không có cách khôi phục tức thời

-   File `final.py` đã bị **lưu đè** sau khi xóa đoạn code cốt lõi, và vì Nam chỉ duy trì bản trên máy cá nhân mà không có bản sao lưu phiên bản trước
-   Việc gửi file qua Zalo chỉ tạo bản tĩnh tại thời điểm gửi, **không có cơ chế theo dõi thay đổi**

### 2. Quy trình làm việc nhóm bị gián đoạn, mất thời gian tái tạo lại công việc

-   Mã nguồn là sản phẩm cốt lõi của dự án **Smart Food**, việc mất đoạn code quan trọng sẽ làm dừng tiến độ phát triển
-   Khi trao đổi file qua Zalo, dễ xảy ra **trùng lặp, nhầm lẫn phiên bản** (v1.py, final.py…), không ai xác nhận được bản nào là chính thức

### 3. Rủi ro mất dữ liệu hoàn toàn khi có sự cố phần cứng hoặc sai thao tác

-   Chỉ lưu trữ duy nhất trên ổ đĩa cá nhân  nếu máy tính hỏng, mất, **toàn bộ tiến độ có thể biến mất hoàn toàn** mà không có bản dự phòng.
-   Quan niệm "lưu ra nhiều bản trên cùng máy là an toàn" là **sai lầm**: các bản sao vẫn nằm trên cùng thiết bị, không phòng ngừa được nguy cơ mất mát do thiết bị gặp sự cố; đồng thời không theo dõi được ai sửa gì, khi nào, và tại sao.

**không có bảo vệ, không có theo dõi, không có khôi phục nhanh**.

----------

# Phần 2: Quy trình Hybrid Workflow 

Mục tiêu: Tích hợp **Git + Dịch vụ đám mây** để mọi thay đổi đều được ghi lại, xem lại và khôi phục chỉ trong 1 cú nhấp chuột, vẫn làm việc thoải mái trên máy cá nhân.

## Bước 1: Thiết lập môi trường một lần duy nhất

### 1.1 Cài đặt công cụ

- cho dự án công khai/riêng tư nhỏ

### 1.2 Khởi tạo kho mã nguồn

Mở thư mục `D:\Project\` trong Terminal / PowerShell, chạy lệnh:

bash

```
# Vào thư mục dự án
cd D:\Project

# Khởi tạo Git
git init

# Định danh người viết mã
git config user.name "Tên của Nam"
git config user.email "email_nam_dung_de_dang_ky@gmail.com"

# Thêm file vào theo dõi
git add v1.py final.py

# Lưu lại phiên bản đầu tiên
git commit -m "Khởi tạo: phiên bản đầy đủ ban đầu"

# Tạo kho trống trên GitHub, sau đó liên kết đẩy lên
git remote add origin https://github.com/ten-tai-khoan/smartfood-code.git
git branch -M main
git push -u origin main

```

## Bước 2: Quy trình làm việc hàng ngày


|Bước|Hành động|
|-|-|
|1|Mở file, viết mã bình thường.Dùng trình soạn thảo trên máy cá nhân|
|2|Hoàn thành một phần công việc.Ghi lại thay đổi|
|3|Lưu phiên bản`git add .` => `git commit -m "Mô tả ngắn gọn thay đổi"`|
|4|Đẩy lên đám mây`git push`|

 Trước khi tắt máy / kết thúc ngày làm việc  **luôn đẩy lên GitHub**

## Bước 3: Khôi phục chỉ trong 1-Click

Khi lỡ xóa, sửa sai hoặc lưu đè như trường hợp file `final.py`:

### Cách 1  Trên giao diện GitHub 

1.  Mở kho chọn file `final.py`
2.  Nhấn vào biểu tượng **Lịch sử / Commits** 
3.  Chọn phiên bản trước khi bị lỗi
4.  Nhấn **Tải xuống** hoặc **Xem nội dung  Sao chép thay thế** 

#### Cách 2  Trên máy tính (Nhanh hơn)

bash

```
# Xem danh sách các phiên bản
git log --oneline

# Khôi phục ngay file về trạng thái phiên bản mong muốn
git checkout -- final.py

```

### Bước 4: Lưu ý tránh lặp lại sai lầm

-    **Không gửi file trực tiếp qua Zalo** => gửi link GitHub thay thế, mọi người tự cập nhật phiên bản mới nhất
-    **Không chỉ lưu trên máy** => mỗi khi hoàn thành phần nào, đẩy lên đám mây ngay
-    **Viết thông điệp rõ ràng** khi lưu phiên bản: `Sửa lỗi đăng nhập`, `Hoàn thành module xử lý đơn hàng`…
-    **Tạo nhánh** khi phát triển tính năng mới để không ảnh hưởng bản chính


