#  SOC Analyst Intern Mini Project - RDP Brute-force & Remote Access  (Remcos) Attack Simulation

#  Mô tả dự án

Dự án mô phỏng một kịch bản tấn công thực tế vào máy tính Windows thông qua brute-force dịch vụ RDP, triển khai mã độc Remcos (RAT - Remote Access Trojan) để thực hiện điều khiển từ xa, đánh cắp dữ liệu và xóa dấu vết. Đây là một bài lab thực hành dành cho vị trí SOC Analyst nhằm rèn luyện kỹ năng phát hiện, phân tích log và điều tra sự cố bảo mật.

---

##  Môi trường thực hiện

 **1 máy Kali Linux** (IP: `192.168.1.137`)
 **1 máy Windows 10** (IP: `192.168.1.5`)
  - Tắt Firewall
  - Bật Remote Desktop (RDP), mở port `3389`
 **Mã độc sử dụng:** Remcos v6.1.0 (bản Light)
 **Yêu cầu:** Cả hai máy có thể ping được nhau
## thực hiện 
# 1, thực hiện brute force mật khẩu thành công từ kali -> windows. Tải về mã độc, thực hiện persistent mã độc, thực thi RCE từ xa bằng mã độc đã cài ( lấy cắp file và xóa file gốc đi)
# 2, memory( dùng volatility) để phân tích
# 3,tra lại log để biết luồng tấn công và nguyên nhân hacker xâm nhập


