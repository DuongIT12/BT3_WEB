# BT3_WEB
# NGUYỄN THẾ DƯƠNG - K225480106007
## Yêu cầu bài tập:
1. Cài đặt môi trường linux: SV chọn 1 trong các phương án
 - enable wsl: cài đặt docker desktop
 - enable wsl: cài đặt ubuntu
 - sử dụng Hyper-V: cài đặt ubuntuv
 - sử dụng VMware : cài đặt ubuntu
 - sử dụng Virtual Box: cài đặt ubuntu
2. Cài đặt Docker (nếu dùng docker desktop trên windows thì nó có ngay)
3. Sử dụng 1 file docker-compose.yml để cài đặt các docker container sau: 
   mariadb (3306), phpmyadmin (8080), nodered/node-red (1880), influxdb (8086), grafana/grafana (3000), nginx (80,443)

 ## BÀI LÀM
 ## 🎯 Mục tiêu đề bài
Xây dựng **Web thương mại điện tử dạng Single Page Application (SPA)**  
toàn bộ giao diện sinh động bằng **JavaScript**,  
xử lý backend qua **Node-RED**, lưu trữ bằng **MariaDB**,  
và **thống kê bán hàng bằng Grafana**.
### 1. Cài đặt môi trường Linux  
Enable WSL và cài Docker Desktop trên Windows  
Mở PowerShell (Administrator) → chạy lệnh: **wsl --install**  
→ Máy sẽ tự cài WSL2 và Ubuntu.  
2.Khởi động lại máy, sau đó mở Ubuntu  để thiết lập tài khoản.   
3.Cài Docker Desktop for Windows:  
🔗 https://www.docker.com/products/docker-desktop   
4.Trong Settings → General, tick chọn:  
✅ “Use the WSL 2 based engine”  
✅ “Enable integration with Ubuntu”  

### 2. Tạo file docker-compose.yml  
Mở Ubuntu Terminal.   
Tạo thư mục làm việc: **mkdir ~/web_app && cd ~/web_app**  
Tạo file docker-compose.yml:**nano docker-compose.yml**  
Tạo file docker-compose.yml
🎯 Mục tiêu  
Tạo file docker-compose.yml để chạy toàn bộ các dịch vụ: 
mariadb – cơ sở dữ liệu  
phpmyadmin – giao diện quản lý DB  
nodered – backend (API xử lý logic)    
nginx – web server phục vụ SPA & reverse proxy cho API  
Lưu và thoát:  
- Bấm Ctrl + O → Enter → Ctrl + X.  
- Chạy tất cả container: **docker compose up -d**  
Sau vài phút, Docker sẽ tự tải toàn bộ images và khởi động 6 container.  
- Kiểm tra:**docker ps**  
<img width="1569" height="329" alt="image" src="https://github.com/user-attachments/assets/e754b30f-0742-4347-9b5c-53bd028efe85" />
- Các container đều chạy
- <img width="1553" height="631" alt="image" src="https://github.com/user-attachments/assets/498e7207-a8f6-465d-93cf-206fac4e8c08" />
- Tạo 2 file  db-init/init.sql
  Khi container mariadb khởi động, nó sẽ chạy tất cả các file .sql trong thư mục db-init/.
File init.sql này sẽ:
<img width="849" height="242" alt="image" src="https://github.com/user-attachments/assets/b8a3bf5d-5691-42d7-8866-434f49a7ffe9" />

Tạo database ecommerce
Tạo các bảng users, sessions, products, orders, order_items
Thêm dữ liệu mẫu (1 user và 3 sản phẩm)
-  file nginx/nginx.conf
  <img width="874" height="226" alt="image" src="https://github.com/user-attachments/assets/6b60c251-a555-4ca4-b6b5-1d72dc126d54" />
Cấu hình nginx để:  
Người dùng truy cập web qua http://localhost  
Mọi request bắt đầu bằng /nodered/ được chuyển đến Node-RED container (cổng 1880)  

Bước 5 — Tạo file frontend/index.html
<img width="948" height="331" alt="image" src="https://github.com/user-attachments/assets/cba0983f-ec9f-4b9b-9dfe-c6faa4e64c9a" />

Mục tiêu  
Tạo 1 trang web đơn giản:  
Giao diện đăng nhập / đăng ký  
Danh sách sản phẩm  
Giỏ hàng (cart)  
Đặt hàng (checkout)  
Hiển thị đơn hàng đã mua  
Frontend sẽ gọi các API từ Node-RED qua đường dẫn /nodered/api/   
 ### các chức năng 
 ## 🧱 Cấu trúc hệ thống
 T3_WEB/
│
├── docker-compose.yml # Khởi tạo toàn bộ stack   
├── db-init/   
│ └── init.sql # Script tạo bảng & dữ liệu mẫu  
├── nodered_data/ # Node-RED flow (API backend)   
├── frontend   
│ ├── index.html # Ứng dụng chính cho khách hàng   
└── nginx/   
└── nginx.conf # Reverse proxy frontend/backend    

 - login cho user, account được tạo trong database và đc 

  <img width="1859" height="716" alt="image" src="https://github.com/user-attachments/assets/10712e53-0b04-4bb6-823d-5a4a0e9a7818" />
- dev quản trị bằng phpMyadmin
<img width="1694" height="798" alt="image" src="https://github.com/user-attachments/assets/476d26b7-a951-446d-a5ed-36805e40c9b8" />


**API Backend (Node-RED)**
Endpoint	Chức năng    
/api/register	Đăng ký người dùng  
/api/login	Đăng nhập & lưu session   
/api/logout	Đăng xuất  
/api/products	Lấy danh sách sản phẩm  
/api/categories	Lấy danh mục  
/api/products_by_category/:id	Lấy sản phẩm theo nhóm  
/api/search?q=	Tìm kiếm    
/api/order	Đặt hàng     
/api/orders	Đơn hàng của người dùng   
/api/admin/orders	Quản trị đơn hàng   
/api/admin/orders/update	Cập nhật trạng thái   
/api/top_selling	Top bán chạy   



**Có Top sản phẩm bán chạy**
<img width="1886" height="207" alt="image" src="https://github.com/user-attachments/assets/8d7d3b49-7322-4f7d-a9a5-c59bc8581729" />
- tạo một /api/top_selling với Node-red , → Liệt kê top 5 sản phẩm bán chạy nhất.
- Flow Node-RED /api/top_selling test
  <img width="526" height="442" alt="image" src="https://github.com/user-attachments/assets/279e1af0-bcac-4989-b44d-c76bda4889a3" />
 
  <img width="1812" height="596" alt="image" src="https://github.com/user-attachments/assets/d1787e30-d514-4235-b2f9-e9e854310d51" />
**Tìm kiếm sản phẩm và hiển thị danh mục sản phẩm**
  <img width="1885" height="728" alt="image" src="https://github.com/user-attachments/assets/cf5aa2ff-d3a4-405f-a092-976d34511a0b" />
và API: GET /api/search?q=keyword — Tìm kiếm sản phẩm
<img width="1384" height="733" alt="image" src="https://github.com/user-attachments/assets/e4e64fc5-8b8d-44b9-9444-66ee0782e938" />

  có API: GET /api/products_by_category/:id — Sản phẩm theo nhóm
  <img width="1545" height="509" alt="image" src="https://github.com/user-attachments/assets/d6d0bff8-57b1-431c-b3f1-6311345f617a" />

**Có tính năng chọn sản phẩm (đưa sản phẩm vào giỏ hàng, thay đổi số lượng sản phẩm trong giỏ, cập nhật tổng tiền)**
  <img width="1895" height="956" alt="image" src="https://github.com/user-attachments/assets/2ab1e02b-df66-4777-8f9c-1e7244c8fcc2" />
- sau khi thêm sản phẩm , ở phần giỏ hàng có số lượng sản phẩm và tổng số tiền
  <img width="423" height="246" alt="image" src="https://github.com/user-attachments/assets/abd40924-1d27-4a1a-bcc9-165538d74f86" />
- Sau khi Bấm "Đặt hàng" sẽ hiện thị ở database với id, status, code..vv
  <img width="1245" height="237" alt="image" src="https://github.com/user-attachments/assets/923aca77-40b6-40d9-999f-618f79ccb3a4" />

- **Có tính năng chọn sản phẩm (đưa sản phẩm vào giỏ hàng, thay đổi số lượng sản phẩm trong giỏ, cập nhật tổng tiền)**
  khi thêm sản phẩm vào giỏ hàng mà muốn thay đổi thì bấm vào dấu trừ bên cạnh sẽ thay đổi, và cập nhật lại số tiền
  <img width="383" height="259" alt="image" src="https://github.com/user-attachments/assets/97a5e7a4-d1c6-4d69-9b5d-b5e8c352a8cf" />
- khi bỏ bớt một sản phẩm số lượng giảm + giá tiền cũng được cập nhật theo số lượng sản phẩm hiện có :
  <img width="383" height="259" alt="image" src="https://github.com/user-attachments/assets/2a1d7222-a5ad-4763-a143-8b8c17aeb70b" />

  _ Admin kiểm tra trạng thái, cập nhật đơn hàng :
  <img width="1630" height="930" alt="image" src="https://github.com/user-attachments/assets/4ba43686-2459-4ddb-a70b-cc079efd2530" />
- API ADMIN: POST /api/admin/orders/update — Cập nhật trạng thái đơn hàng
  <img width="1205" height="654" alt="image" src="https://github.com/user-attachments/assets/8a660e32-5564-4db2-9063-bc029f28f956" />

**Có tính năng dành cho admin: biểu đồ thống kê số lượng mặt hàng bán được trong từng ngày. (sử dụng grafana)**
trạng thái Refresh 30s
<img width="1474" height="636" alt="image" src="https://github.com/user-attachments/assets/d3f3c4cb-3355-4fee-b625-8d1d694b1273" />

và xem số lượng đơn dựa trên biểu đồ 
<img width="774" height="678" alt="image" src="https://github.com/user-attachments/assets/1388622f-1e77-4307-8c16-a8f194eec20d" />













👨‍💻 Tác giả
Nguyễn Dương IT
📧 Email: [nguyenduongg24ct@gmail.com]
🌐 GitHub: https://github.com/DuongIT12/BT3_WEB






  
