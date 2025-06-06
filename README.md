# SSH Brute Force Attack Lab

## 🎯 Mục tiêu
Thực hiện tấn công brute force vào dịch vụ SSH, đánh giá mức độ nguy hiểm, và triển khai các biện pháp phòng chống hiệu quả.

## 📌 Nội dung
- Tổng quan về SSH và cơ chế xác thực
- Kịch bản brute force tấn công SSH sử dụng từ điển
- Demo thực tế với các công cụ như Hydra
- Biện pháp phòng chống brute force: SSH Key, Fail2Ban, 2FA...

## 🧪 Kịch bản triển khai
> Xem chi tiết tại [`scenario.md`](scenario.md)

## 📂 Cấu trúc thư mục
ssh-bruteforce-lab/
├── brute.py # Script brute-force SSH dùng Paramiko
├── users.txt # Danh sách tên đăng nhập mẫu
├── passwords.txt # Danh sách mật khẩu mẫu
├── tools/ # Hướng dẫn cài đặt các công cụ sử dụng
├── screenshots/ # Hình ảnh minh họa tấn công và phòng thủ
├── report/ # Chứa báo cáo đầy đủ 
├── scenario.md # Mô tả chi tiết các bước thực nghiệm
└── README.md # Giới thiệu chính của dự án


## 🛠 Công cụ sử dụng
- Kali Linux / Ubuntu Server
- Hydra, Nmap
- sshd (OpenSSH)
- Fail2Ban
- Python/Bash scripts
