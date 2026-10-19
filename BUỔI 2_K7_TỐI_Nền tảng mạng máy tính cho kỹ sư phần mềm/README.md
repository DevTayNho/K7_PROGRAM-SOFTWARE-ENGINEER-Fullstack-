# 🌐 Nền Tảng Mạng Máy Tính Dành Cho Lập Trình Viên: Từ Địa Chỉ IP Đến Hành Trình Truy Cập Web

> Tài liệu tổng hợp kiến thức nền tảng về mạng máy tính dành riêng cho Software Engineer: Từ cách phân giải địa chỉ, giao thức truyền tải cho đến luồng dữ liệu web và ứng dụng thực tế.

---

## 🗺️ 1. Sơ Đồ Tư Duy Tổng Quan (Mindmap)

file:///D:/workspace/DBI202/ASSIGNMENT/Gi%E1%BA%A3i_M%C3%A3_Ki%E1%BA%BFn_Tr%C3%BAc_Internet.pdf

---

## 📌 2. Nội Dung Chi Tiết

### 1. Địa Chỉ IP - "Số nhà" trong Thế giới Số (IPv4, IPv6, Public & Private)
Để gửi một món quà cho bạn bè ở đời thực, bạn bắt buộc phải biết địa chỉ nhà của họ. Trong mạng máy tính, điều này cũng tương tự: muốn hai máy tính truyền dữ liệu cho nhau, hoặc điện thoại xem được video, hệ thống phải biết chính xác dữ liệu cần đi tới đâu. Cái "đâu" đó chính là **Địa chỉ IP (Internet Protocol Address)**.

Địa chỉ IP được chia thành hai phạm vi hoạt động chính:
* **IP Public:** Địa chỉ IP dùng ngoài Internet công cộng. Đây là loại địa chỉ mà các thiết bị ngoài Internet có thể tìm thấy và truy cập trực tiếp. Bạn sẽ gặp IP Public ở các máy chủ Web, dịch vụ Cloud (AWS, VPS), hoặc các Public API.
* **IP Private:** Địa chỉ IP dùng nội bộ trong một mạng đóng (như WiFi gia đình, mạng công ty, mạng nội bộ Docker hay Cloud). Nó không thể truy cập trực tiếp từ Internet công cộng. Các dải IP Private chuẩn bao gồm: `10.x.x.x`, `172.16.x.x` đến `172.31.x.x`, và `192.168.x.x`.

Bên cạnh phạm vi, địa chỉ IP còn có sự tiến hóa về phiên bản công nghệ:
* **IPv4:** Phiên bản truyền thống, viết dưới dạng 4 cụm số phân tách bằng dấu chấm (mỗi cụm từ 0 đến 255, ví dụ: `192.168.51.101` hoặc `8.8.8.8`). Vì chỉ sử dụng cấu trúc 32-bit, tổng số lượng địa chỉ IPv4 chỉ có hơn 4 tỷ — con số đã cạn kiệt trước sự bùng nổ của thiết bị thông minh.
* **IPv6:** Thế hệ địa chỉ mới sử dụng 128-bit biểu diễn dưới dạng chuỗi Hexadecimal (ví dụ: `2026:0db8:1234:85a3:0000:1111:8a2e:0370`). IPv6 ra đời nhằm giải quyết triệt để vấn đề thiếu hụt địa chỉ của IPv4 và đang ngày càng phổ biến trong hạ tầng hiện đại.

---

### 2. Domain, DNS và Port - Từ Tên dễ nhớ đến "Số phòng" Dịch vụ
Mặc dù máy tính kết nối với nhau bằng các con số IP khô khan, con người lại giỏi ghi nhớ chữ viết hơn. Đó là lý do khái niệm Domain (Tên miền) ra đời.

* **Domain và DNS:** Domain như `facebook.com` hay `hotrodoan.vn` chỉ là tên gợi nhớ dành cho con người. Khi bạn gõ một tên miền vào trình duyệt, trình duyệt không thể kết nối trực tiếp tới dòng chữ đó mà phải nhờ tới **DNS (Domain Name System)**. DNS đóng vai trò như một "quyển sổ danh bạ", giúp tra cứu xem tên miền đó tương ứng với địa chỉ IP vật lý nào để tiếp tục kết nối.
* **Port (Cổng dịch vụ):** Nếu địa chỉ IP giống như số nhà của một tòa chung cư, thì Port chính là số phòng cụ thể trong tòa nhà đó. Một máy chủ (1 IP) có thể chạy đồng thời rất nhiều dịch vụ khác nhau. Nếu không có Port để phân chia, hệ thống sẽ không biết người dùng muốn truy cập vào dịch vụ nào.

Một số **Port tiêu chuẩn** mà mọi lập trình viên đều cần biết:
* **Port 80:** Dùng cho giao thức HTTP (trang web không mã hóa).
* **Port 443:** Dùng cho giao thức HTTPS (trang web bảo mật SSL/TLS).
* **Port 22:** Dùng cho SSH (truy cập điều khiển máy chủ Linux từ xa).
* **Port 53:** Dùng cho dịch vụ phân giải tên miền DNS.
* **Port 3306:** Dùng cho cơ sở dữ liệu (Database MySQL).
* **Port 6379:** Dùng cho hệ thống lưu trữ đệm Redis.
* **Port 3000 / 8080:** Phổ biến cho các ứng dụng Frontend (ReactJS, NextJS) và Backend (Java, C#, Python).
* **Port 9090:** Thường gặp trong các hệ thống Giám sát an ninh (Monitoring).

---

### 3. Giải mã URL và Hành trình 6 bước Kết nối Mạng
Khi bạn truy cập vào một đường dẫn đầy đủ, được gọi là **URL (Uniform Resource Locator)**, các thành phần đã học sẽ kết hợp lại với nhau.

*Ví dụ với URL:* `https://hotrodoan.vn:443/login`
* **Protocol (Giao thức):** `https` (phương thức trao đổi dữ liệu an toàn).
* **Domain:** `hotrodoan.vn` (tên máy chủ đích).
* **Port:** `443` (cổng dịch vụ tiếp nhận).
* **Path (Đường dẫn):** `/login` (tài nguyên cụ thể trên máy chủ).

Dữ liệu sau đó được truyền qua các tầng của mô hình OSI (7 tầng) hoặc TCP/IP (4 tầng) bằng các giao thức Transport như **TCP** (tin cậy, có kết nối bắt tay) hoặc **UDP** (tốc độ cao, không kết nối).

#### Hành trình 6 bước kết nối khi gõ địa chỉ Web và bấm Enter:
1. **DNS phân giải:** Trình duyệt truy vấn DNS để đổi Domain thành địa chỉ IP thật.
2. **Xác định Protocol & Port:** Trình duyệt xác định giao thức (HTTP/HTTPS) và Port cần kết nối (80/443).
3. **Mở kết nối:** Thiết lập kết nối mạng tới địa chỉ IP và Port của máy chủ (thông qua bắt tay TCP).
4. **Gửi HTTP Request:** Trình duyệt gửi yêu cầu lấy dữ liệu tới máy chủ.
5. **Server xử lý:** Máy chủ tiếp nhận, xử lý yêu cầu và trả về dữ liệu (HTTP Response).
6. **Hiển thị kết quả:** Trình duyệt nhận phản hồi và dựng lên giao diện trang web cho người dùng.

---

## 🎯 Tổng kết bài học
Hiểu rõ cơ chế hoạt động của địa chỉ IP, hệ thống phân giải DNS, cổng dịch vụ Port và quy trình giao tiếp Web chính là nền tảng vững chắc giúp lập trình viên dễ dàng cấu hình máy chủ, làm việc với Docker, thiết lập Reverse Proxy và xử lý các sự cố kết nối trong thực tế.

**Tóm tắt các điểm cốt lõi:**
* **Địa chỉ IP:** Là địa chỉ định danh thiết bị trong mạng; phân loại thành Public (ngoài Internet) và Private (nội bộ).
* **IPv4 vs IPv6:** IPv4 (32-bit, 4 cụm số) đang dần được thay thế bởi IPv6 (128-bit, chuỗi Hex) do thiếu hụt không gian địa chỉ.
* **Domain & DNS:** Domain giúp con người dễ nhớ; DNS đóng vai trò "danh bạ" dịch tên miền thành IP cho máy tính.
* **Port:** Là "số phòng" giúp máy chủ phân loại và định tuyến lưu lượng truy cập đến đúng dịch vụ (Web, DB, SSH...).
* **Cấu trúc URL & Quy trình 6 bước:** URL kết hợp Protocol, Domain, Port và Path để tạo thành yêu cầu hoàn chỉnh, trải qua 6 bước từ tra cứu DNS, bắt tay TCP đến nhận phản hồi HTTP Response.
