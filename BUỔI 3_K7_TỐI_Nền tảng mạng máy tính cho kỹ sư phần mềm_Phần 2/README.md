# 🌐 Mô Hình OSI & Hành Trình 8 Bước Truy Cập Trang Web

> Tài liệu tổng hợp kiến thức về mô hình 7 tầng OSI, sự khác biệt giữa TCP và UDP, cùng hành trình chi tiết của một request khi người dùng truy cập trang web.

---

## 🗺️ 1. Sơ Đồ Tư Duy Tổng Quan (Mindmap)

https://notebook.google.com/notebook/

---

## 📌 2. Nội Dung Chi Tiết

### 1. Mô Hình OSI: 7 Tầng Chuyển Giao Dữ Liệu
Khi bạn viết code Frontend gọi API hoặc Backend trả về một chuỗi JSON, dữ liệu không đi thẳng ra Internet. Nó đi qua **mô hình 7 tầng OSI (Open Systems Interconnection)** — một khung tư duy kinh điển giúp chúng ta hiểu cách dữ liệu di chuyển từ ứng dụng xuống mạng phần cứng, rồi lại mở ngược ra ở phía bên nhận.

> **Nguyên tắc quan trọng cần nhớ:** Càng lên cao thì càng gần ứng dụng, càng xuống thấp thì càng gần phần cứng và mạng lưới vật lý.

* **Tầng 7 - Application (Tầng ứng dụng):** Đây là tầng gần với lập trình viên và người dùng nhất. Khi bạn dùng trình duyệt, Postman, app mobile hay gọi các giao thức như HTTP, HTTPS, DNS, bạn đang tương tác trực tiếp với tầng này.
* **Tầng 6 - Presentation (Tầng biểu diễn):** Chịu trách nhiệm về cách dữ liệu được định dạng, mã hóa và nén. Hãy liên tưởng đến JSON, hoặc việc mã hóa dữ liệu qua SSL/TLS ở góc nhìn biểu diễn.
* **Tầng 5 - Session (Tầng phiên):** Quản lý và duy trì phiên giao tiếp giữa hai hệ thống.
* **Tầng 4 - Transport (Tầng giao vận):** Tầng cực kỳ quan trọng với Developer. Nó quản lý các giao thức truyền tải như TCP, UDP và các khái niệm về Port. Khi bạn nghe nói *"service listen ở port 8080"*, *"kết nối tới MySQL port 3306"* hay lỗi *"TCP timeout"*, đó chính là những chuyện đang diễn ra ở Tầng 4.
* **Tầng 3 - Network (Tầng mạng):** Chịu trách nhiệm định tuyến các gói tin qua các mạng khác nhau bằng địa chỉ IP (IPv4, IPv6) và các thiết bị Router.
* **Tầng 2 - Data Link (Tầng liên kết dữ liệu):** Xử lý giao tiếp trong cùng một mạng nội bộ thông qua địa chỉ MAC address và thiết bị Switch (bạn có thể kiểm tra qua lệnh `ipconfig -all`).
* **Tầng 1 - Physical (Tầng vật lý):** Môi trường vật lý thực sự truyền tải tín hiệu: dây cáp mạng, sóng WiFi, và các thiết bị truyền dẫn.

---

### 2. Mô Hình TCP/IP Và Cuộc Chiến Giữa TCP Và UDP
Dù mô hình OSI 7 tầng rất nổi tiếng trong giảng dạy để giúp xây dựng tư duy phân tầng, nhưng trên thực tế Internet hiện đại, **mô hình TCP/IP** mới là chuẩn mực sát nhất với cách các hệ thống thực vận hành.

Ở tầng giao vận (Transport), hai giao thức phổ biến nhất là TCP và UDP. Lựa chọn giao thức nào phụ thuộc vào việc bạn ưu tiên sự tin cậy hay tốc độ:

1. **Giao thức TCP (Transmission Control Protocol):**
   * Là giao thức truyền dữ liệu tin cậy. 
   * Trước khi truyền dữ liệu, hai bên phải thiết lập kết nối rõ ràng. 
   * TCP đảm bảo dữ liệu đến đúng thứ tự và có cơ chế kiểm tra lỗi, gửi lại gói tin nếu bị mất trong quá trình truyền tải. 
   * **Ứng dụng:** Các dịch vụ không thể chấp nhận mất mát dữ liệu như HTTP/HTTPS (Web), API, MySQL, SSH.

2. **Giao thức UDP (User Datagram Protocol):**
   * Hoạt động theo phương châm nhanh và nhẹ. 
   * UDP gửi dữ liệu đi mà không cần thiết lập kết nối trước, không đảm bảo thứ tự và không gửi lại nếu bị rớt gói tin. 
   * **Ứng dụng:** Các tình huống cần tốc độ thời gian thực và chấp nhận mất một ít dữ liệu nhỏ (Livestream, Video Call, Game Online).

---

### 3. Hành Trình Thực Tế: 8 Bước Khi Truy Cập Một Trang Web
Để gắn liền lý thuyết với thực tế, hãy tưởng tượng một kịch bản đơn giản: Lập trình viên tên Kiên mở trình duyệt Cốc Cốc và gõ địa chỉ `2010.com`. Điều gì sẽ diễn ra đằng sau hậu trường?

* **Bước 1: Trình duyệt hỏi DNS.** Trình duyệt không biết `2010.com` ở đâu, nó phải truy vấn hệ thống phân giải tên miền (DNS) để lấy địa chỉ IP tương ứng của máy chủ.
* **Bước 2: Nhìn vào Protocol.** Trình duyệt xác định giao thức sử dụng là HTTPS, mặc định dữ liệu sẽ đi qua Port 443.
* **Bước 3: Kết nối tới IP và Port.** Trình duyệt khởi tạo kết nối mạng tới địa chỉ IP đã tìm được ở Bước 1 thông qua Port 443.
* **Bước 4: Bắt tay TLS (TLS Handshake).** Vì là HTTPS, một quá trình bắt tay bảo mật diễn ra để thỏa thuận phương thức mã hóa kết nối giữa trình duyệt và máy chủ.
* **Bước 5: Gửi HTTP Request.** Sau khi đường truyền mã hóa đã an toàn, trình duyệt gửi đi Request thực sự (ví dụ: phương thức GET, POST) đính kèm Header, Cookie hoặc Token.
* **Bước 6: Server nhận Request.** Yêu cầu tới máy chủ và được tiếp nhận bởi các Web Server như Nginx, Apache, Spring Boot...
* **Bước 7: Web App xử lý Logic.** Ứng dụng web đọc request, kiểm tra xác thực (Auth), truy vấn Database, thực hiện nghiệp vụ và đóng gói dữ liệu phản hồi (Response).
* **Bước 8: Trả Response về trình duyệt.** Máy chủ phản hồi dữ liệu gồm HTML, CSS, JS hoặc JSON về lại trình duyệt để hiển thị cho Kiên.

---

## 🎯 Tổng kết bài học
Hiểu rõ cách dữ liệu di chuyển qua các tầng mạng và chu trình của một request giúp lập trình viên chuyển mình từ người chỉ biết viết code ứng dụng đơn thuần thành người hiểu toàn diện hệ thống. Càng hiểu sâu về hạ tầng mạng, bạn càng tối ưu hiệu năng và xử lý sự cố ứng dụng tốt hơn.

**Bài học cốt lõi (Key Takeaways):**
* **Mô hình OSI:** Gồm 7 tầng (từ Physical đến Application). Tầng càng cao càng gần ứng dụng, tầng càng thấp càng gần phần cứng.
* **OSI vs TCP/IP:** OSI là mô hình tư duy học thuật; TCP/IP là mô hình vận hành thực tế của Internet.
* **TCP vs UDP:** TCP đảm bảo tính tin cậy, đúng thứ tự (dùng cho Web, DB, API); UDP ưu tiên tốc độ, chấp nhận mất gói tin (dùng cho Livestream, Game).
* **Luồng Request Web:** Trải qua đầy đủ các bước từ phân giải DNS, xác định Port, bắt tay TLS, gửi HTTP Request đến xử lý logic tại Server và nhận Response.
