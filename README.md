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
├── attack/ # Mã nguồn tấn công và log đầu ra
├── defense/ # Cấu hình phòng thủ
├── screenshots/ # Hình ảnh mô phỏng
├── tools/ # Hướng dẫn cài đặt các công cụ
├── report/ # Báo cáo đầy đủ (PDF nếu có)
├── README.md # File giới thiệu chính
└── scenario.md # Mô tả chi tiết các bước thực nghiệm

## 🛠 Công cụ sử dụng
- Kali Linux / Ubuntu Server
- Hydra, Nmap
- sshd (OpenSSH)
- Fail2Ban
- Python/Bash scripts
