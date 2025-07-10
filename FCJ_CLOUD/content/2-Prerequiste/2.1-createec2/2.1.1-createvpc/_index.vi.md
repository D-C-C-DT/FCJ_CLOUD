---
title : "Tạo VPC"
date : "`r Sys.Date()`"
weight : 1
chapter : false
pre : " <b> 2.1.1 </b> "
---

#### Tạo một VPC với các Subnet và tài nguyên liên quan

1. Truy cập [bảng điều khiển quản lý dịch vụ VPC](https://console.aws.amazon.com/vpc/home)  
   + Nhấp vào **Your VPC**.  
   + Nhấp vào **Create VPC**.

![VPC](/images/vpc/001-createvpc.png)

2. Đối với **Resources to create**, chọn **VPC and more** để tạo một môi trường VPC hoàn chỉnh.

![VPC](/images/vpc/002-createvpc.png)

3. **Name tag auto-generation**:  
Cho phép AWS tự động gán tên nhất quán cho các tài nguyên VPC.

4. **IPv4 CIDR block**:  
Nhập phạm vi địa chỉ IP nội bộ cho VPC của bạn (ví dụ: 10.0.0.0/16).

5. **IPv6 CIDR block** (tùy chọn):  
Bật IPv6 nếu cần, sử dụng phạm vi địa chỉ được Amazon cung cấp.

6. **Tenancy**:

   **Default:** Các phiên bản EC2 sử dụng cài đặt mặc định – tiết kiệm chi phí.

   **Dedicated:** Các phiên bản EC2 chạy trên phần cứng dành riêng – sử dụng cho các yêu cầu tuân thủ hoặc giấy phép đặc biệt.

   💡 **Khuyến nghị**: Sử dụng **Default** trừ khi bạn có yêu cầu cụ thể để tiết kiệm chi phí.

7. **Availability Zones – AZs**:  
Chọn ít nhất 2 vùng AZ để đảm bảo mức độ sẵn sàng cao.

![VPC](/images/vpc/003-createvpc.png)  
![VPC](/images/vpc/004-createvpc.png)

9. **Số lượng subnet:**  
Chọn số lượng subnet công khai (public) và subnet riêng tư (private).  
Sử dụng các subnet riêng tư cho RDS để tăng cường bảo mật.

10. **Bảo mật 🔒:**  
Không đặt RDS vào các subnet công khai.  
Tạo NAT Gateway nếu các subnet riêng tư cần truy cập internet.

11. **NAT Gateway (tùy chọn):**  
Tạo một NAT Gateway cho mỗi vùng AZ để tránh sự phụ thuộc giữa các vùng (cross-AZ).

12. **Egress-only Internet Gateway (IPv6 – tùy chọn):**  
Sử dụng cho lưu lượng IPv6 outbound từ các subnet riêng tư.

13. **S3 Gateway Endpoint (tùy chọn):**  
Cho phép truy cập nội bộ đến Amazon S3 mà không cần sử dụng internet công cộng.

14. **Tùy chọn DNS**:  
DNS resolution và DNS hostnames được bật theo mặc định – khuyến nghị giữ nguyên cài đặt này.

15. **Gắn thẻ (Tagging):**  
Bạn có thể thêm các cặp key–value để quản lý tài nguyên dễ dàng hơn.

19. **Xem trước kiến trúc (Preview architecture):**  
Xem trước kiến trúc VPC trong phần Preview trước khi tạo.

20. **Tạo VPC:**  
Nhấp vào **“Create VPC”** để khởi tạo tất cả các tài nguyên đã cấu hình.

![VPC](/images/vpc/005-createvpc.png)

---

#### Cấu hình gán địa chỉ IP công cộng cho các subnet

Để thay đổi hành vi gán địa chỉ IP công cộng cho một subnet:

1. Mở bảng điều khiển Amazon VPC tại **https://console.aws.amazon.com/vpc/**  
2. Trong thanh điều hướng, chọn **Subnets**.  
3. Chọn subnet của bạn và nhấp **Actions**, sau đó **Edit subnet settings**.

![VPC](/images/vpc/006-createvpc.png)

4. Cấu hình thiết lập **Auto-assign public IPv4 address**:

   **Checked (Đã chọn):** Các phiên bản EC2 trong subnet sẽ tự động nhận một địa chỉ IPv4 công cộng.

   **Unchecked (Bỏ chọn):** Các phiên bản EC2 sẽ không nhận địa chỉ IPv4 công cộng trừ khi được chỉ định rõ ràng khi khởi tạo.

🔒 **Lưu ý bảo mật**: Đối với các subnet chứa các phiên bản RDS, không bật cài đặt này để tránh việc gán địa chỉ IP công cộng ngoài ý muốn.

5. Nhấp vào **“Save”** để áp dụng cấu hình.

![VPC](/images/vpc/007-createvpc.png)

⚠️ **Cảnh báo:** Các subnet mặc định có tính năng tự động gán địa chỉ IPv4 công cộng được bật theo mặc định. Luôn kiểm tra cài đặt này khi sử dụng subnet mặc định cho triển khai cơ sở dữ liệu.
