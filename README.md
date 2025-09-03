# HIỆU CHỈNH TỐI ƯU MÔ HÌNH
<img width="1612" height="1088" alt="image" src="https://github.com/user-attachments/assets/6052cc42-db26-4b95-8b35-dc1940ad9fcb" />

## Mục tiêu
Bài lab này nhằm triển khai và tối ưu mô hình mạng doanh nghiệp với các cơ chế dự phòng (redundancy) và cân bằng tải (load balancing), kết hợp định tuyến tĩnh và quản lý VLAN tập trung.

##  Thành phần chính
1. **HSRP (Hot Standby Router Protocol)**
   - CORE251 là **Active Router** cho VLAN 10, VLAN 20.  
   - CORE252 là **Active Router** cho VLAN 30, VLAN 40.  

2. **STP (Spanning Tree Protocol)**
   - CORE251 là **Root Switch** cho VLAN 10, VLAN 20.  
   - CORE252 là **Root Switch** cho VLAN 30, VLAN 40.  

3. **Static Route trên WAN-R**
   - Lưu lượng về VLAN 10, 20 đi qua CORE251.  
   - Lưu lượng về VLAN 30, 40 đi qua CORE252.  

4. **VTP (VLAN Trunking Protocol)**
   - VTP Server: CORE251.  
   - Các switch khác hoạt động ở chế độ VTP Client để đồng bộ VLAN.

## 🖧 VLAN triển khai
| VLAN | Subnet            | Virtual IP        |
|------|-------------------|-------------------|
| 10   | 192.168.10.0/24   | 192.168.10.254    |
| 20   | 192.168.20.0/24   | 192.168.20.254    |
| 30   | 192.168.30.0/24   | 192.168.30.254    |
| 40   | 192.168.40.0/24   | 192.168.40.254    |

##  Kết quả mong đợi
- Các VLAN được quản lý tập trung bằng VTP.  
- Redundancy đảm bảo **HSRP** và **STP** duy trì tính sẵn sàng cao.  
- WAN-R định tuyến đúng theo phân bổ CoreSW.  
- Người dùng trong mỗi VLAN truy cập được ra ngoài mạng WAN thông qua Virtual IP.  

---


