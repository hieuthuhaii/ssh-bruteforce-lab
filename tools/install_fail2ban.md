```markdown
# Cài đặt Fail2Ban

Fail2Ban giúp tự động chặn IP brute-force SSH hoặc các dịch vụ khác.

## 🔧 Cài đặt trên Ubuntu Server

```bash
sudo apt update
sudo apt install fail2ban -y

⚙️ Cấu hình nhanh
Tạo file cấu hình:

bash
Sao chép
Chỉnh sửa
sudo nano /etc/fail2ban/jail.local
Thêm nội dung:

ini
Sao chép
Chỉnh sửa
[sshd]
enabled = true
port = ssh
filter = sshd
logpath = /var/log/auth.log
maxretry = 3
bantime = 600
findtime = 600
Khởi động lại dịch vụ:

bash
Sao chép
Chỉnh sửa
sudo systemctl restart fail2ban
✅ Kiểm tra IP bị chặn
bash
Sao chép
Chỉnh sửa
sudo fail2ban-client status sshd
