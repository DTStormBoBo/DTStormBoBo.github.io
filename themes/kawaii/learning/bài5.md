---
title: "Buổi 5: Lập Trình Sockets TCP - Xây Dựng Kết Nối Tin Cậy"
date: 2025-12-27
draft: false
tags: ["Java", "Networking", "TCP", "Socket", "Client-Server"]
categories: ["Lập Trình Mạng"]
description: "Khám phá giao thức TCP, mô hình Client-Server và cách xây dựng ứng dụng mạng tin cậy bằng Java Socket."
---

## 1. Mở đầu: Tại sao DevOps cần hiểu TCP?

Trong Buổi 4, chúng ta đã học cách tìm địa chỉ nhà (IP/DNS). Hôm nay, chúng ta sẽ học cách **gõ cửa và nói chuyện** với chủ nhà thông qua giao thức TCP.

Trong thế giới DevOps, khi bạn debug lỗi "Connection Refused" hay cấu hình Load Balancer, bạn đang làm việc trực tiếp trên nền tảng của TCP.

### TCP là gì?
TCP (Transmission Control Protocol) là giao thức hướng kết nối, đảm bảo độ tin cậy cao.
* **Không mất dữ liệu:** Gói tin bị mất sẽ được gửi lại.
* **Đúng thứ tự:** Dữ liệu đến nơi theo đúng trình tự gửi.
* **Kiểm soát luồng:** Đảm bảo bên nhận không bị "ngộp" dữ liệu.


Để thiết lập kết nối, TCP sử dụng quy trình **Bắt tay 3 bước (Three-way handshake)**: SYN -> SYN-ACK -> ACK.

## 2. Mô hình Client - Server

Mọi ứng dụng mạng TCP đều hoạt động dựa trên mô hình này.


1.  **Server (Máy chủ):** Chạy trước, mở cổng (Port) và chờ đợi.
2.  **Client (Máy khách):** Chạy sau, chủ động kết nối tới IP và Port của Server.
3.  **Giao tiếp:** Hai bên truyền nhận dữ liệu qua luồng (Stream).

## 3. Lập trình TCP Socket trong Java

Java cung cấp 2 class chính trong gói `java.net` để xử lý TCP.

### 3.1. ServerSocket (Dành cho Server)
Class này dùng để tạo máy chủ và lắng nghe kết nối.

* **Khởi tạo:** `ServerSocket(int port)` - Mở cổng để nghe.
* **Chấp nhận:** `Socket accept()` - Chặn chương trình cho đến khi có Client kết nối. Trả về một đối tượng `Socket` để giao tiếp riêng với Client đó.

### 3.2. Socket (Dành cho Client & Giao tiếp)
Class này đại diện cho một đầu mối kết nối (endpoint).

* **Khởi tạo (Client):** `Socket(String host, int port)` - Kết nối tới Server.
* **Gửi dữ liệu:** `OutputStream getOutputStream()`.
* **Nhận dữ liệu:** `InputStream getInputStream()`.

## 4. Code Thực Chiến: Ứng dụng Echo Đơn Giản

Dưới đây là ví dụ cơ bản nhất: Client gửi lời chào, Server trả lời lại.

### Code Server

```java
import java.io.*;
import java.net.*;

public class SimpleServer {
    public static void main(String[] args) {
        try {
            // 1. Mở cổng 1234
            ServerSocket serverSocket = new ServerSocket(1234);
            System.out.println("Server đang lắng nghe tại cổng 1234...");

            // 2. Chờ Client kết nối (Blocking)
            Socket clientSocket = serverSocket.accept();
            System.out.println("Client đã kết nối!");

            // 3. Tạo luồng đọc/ghi
            BufferedReader in = new BufferedReader(new InputStreamReader(clientSocket.getInputStream()));
            PrintWriter out = new PrintWriter(clientSocket.getOutputStream(), true);

            // 4. Nhận tin và trả lời
            String message = in.readLine(); // Đọc tin từ Client
            System.out.println("Client nói: " + message);
            
            out.println("Xin chào Client, Server đã nhận được tin!"); // Gửi lại

            // 5. Đóng kết nối
            serverSocket.close();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

### Code Client

```java
import java.io.*;
import java.net.*;

public class SimpleClient {
    public static void main(String[] args) {
        try {
            // 1. Kết nối tới Server tại localhost:1234
            Socket socket = new Socket("localhost", 1234);

            // 2. Tạo luồng đọc/ghi
            BufferedReader in = new BufferedReader(new InputStreamReader(socket.getInputStream()));
            PrintWriter out = new PrintWriter(socket.getOutputStream(), true);

            // 3. Gửi tin nhắn tới Server
            out.println("Xin chào Server!");

            // 4. Nhận phản hồi từ Server
            String response = in.readLine();
            System.out.println("Server trả lời: " + response);

            // 5. Đóng kết nối
            socket.close();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

## 5. Bài Tập Tại Lớp: Oẳn Tù Tì v3

### Yêu cầu:
1. Viết tiếp chương trình **Oẳn Tù Tì v2** để hỗ trợ **3 người chơi đồng thời**.
2. Sửa lỗi "Null" khi không có đủ người chơi hoặc khi kết nối bị gián đoạn.
3. Cập nhật điểm số của từng người chơi sau mỗi lượt chơi.
4. Hiển thị kết quả chi tiết của từng lượt chơi trên cả **Server** và **Client**.

### Gợi ý triển khai:
- **Server**:
  - Sử dụng **Thread** để xử lý đồng thời kết nối từ 3 Client.
  - Quản lý trạng thái của từng người chơi (tên, điểm số, lựa chọn).
  - Xác định kết quả của mỗi lượt chơi và gửi thông báo đến từng Client.
- **Client**:
  - Kết nối đến Server và gửi lựa chọn (Kéo, Búa, Bao).
  - Nhận kết quả từ Server và hiển thị trên màn hình.

---

## 6. Trắc Nghiệm Ôn Tập

### Câu hỏi:
1. **TCP** là giao thức hướng kết nối. Điều này có nghĩa là gì?
   - A. Dữ liệu được truyền đi mà không cần xác nhận.
   - B. Kết nối phải được thiết lập trước khi truyền dữ liệu.
   - C. Dữ liệu được truyền đi theo từng gói nhỏ không theo thứ tự.
   - D. Không có cơ chế kiểm soát lỗi.

   **Đáp án:** B

2. Phương thức nào trong lớp `ServerSocket` được sử dụng để chấp nhận kết nối từ Client?
   - A. `connect()`
   - B. `accept()`
   - C. `listen()`
   - D. `bind()`

   **Đáp án:** B

3. Trong mô hình Client-Server, vai trò của Client là gì?
   - A. Lắng nghe kết nối từ Server.
   - B. Gửi yêu cầu dịch vụ đến Server.
   - C. Xử lý yêu cầu và trả kết quả.
   - D. Đóng kết nối khi không sử dụng.

   **Đáp án:** B

---

## 7. Thuyết Trình

### Chủ đề:
- **Ứng dụng thực tế của TCP trong lập trình mạng.**
- **So sánh TCP và UDP: Khi nào nên sử dụng?**
- **Thách thức và giải pháp khi lập trình ứng dụng mạng với TCP.**

---

## 8. Hỏi & Đáp

### Một số câu hỏi gợi ý:
1. Làm thế nào để xử lý lỗi "Connection Refused" khi kết nối TCP?
2. Tại sao cần sử dụng `try-catch` khi làm việc với `Socket` và `ServerSocket`?
3. Làm thế nào để tối ưu hiệu suất khi xử lý nhiều kết nối đồng thời trên Server?

---

## Enjoy Learning!

Hãy tiếp tục khám phá và thực hành để nắm vững kiến thức về lập trình mạng. Chúc các bạn học tốt và thành công!