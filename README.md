# BT3_WEB
# NGUYỄN THẾ DƯƠNG - K225480106007
## Yêu cầu bài tập:
1. Cài đặt môi trường linux: SV chọn 1 trong các phương án
 - enable wsl: cài đặt docker desktop
 - enable wsl: cài đặt ubuntu
 - sử dụng Hyper-V: cài đặt ubuntu
 - sử dụng VMware : cài đặt ubuntu
 - sử dụng Virtual Box: cài đặt ubuntu
2. Cài đặt Docker (nếu dùng docker desktop trên windows thì nó có ngay)
3. Sử dụng 1 file docker-compose.yml để cài đặt các docker container sau: 
   mariadb (3306), phpmyadmin (8080), nodered/node-red (1880), influxdb (8086), grafana/grafana (3000), nginx (80,443)

 ## BÀI LÀM
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
Lưu và thoát:  
- Bấm Ctrl + O → Enter → Ctrl + X.  
- Chạy tất cả container: **docker compose up -d**  
Sau vài phút, Docker sẽ tự tải toàn bộ images và khởi động 6 container.  
- Kiểm tra:**docker ps**  
<img width="1569" height="329" alt="image" src="https://github.com/user-attachments/assets/e754b30f-0742-4347-9b5c-53bd028efe85" />
 
  
