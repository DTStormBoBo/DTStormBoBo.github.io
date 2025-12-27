---
title: "Bài 2: Kiến thức nền tảng?"
date: 2025-12-16
weight: 2
draft: false
tags: ["Network", "Theory"]
summary: "MẠNG MÁY TÍNH & INTERNET."
---

## BUỔI 2: KIẾN THỨC NỀN TẢNG

### NỘI DUNG CHÍNH
1. **Khởi động đầu giờ**
2. **Mạng máy tính & Internet**
3. **Truyền cảm hứng**
4. **Các ứng dụng mạng**
5. **Ngôn ngữ Java**
6. **Tóm tắt nội dung**
7. **Hỏi đáp**

---

## 1. KHỞI ĐỘNG ĐẦU GIỜ

- **Câu hỏi:** Internet có khoảng bao nhiêu thiết bị kết nối (End-Devices) vào năm 2022?  
  **Trả lời:** 15 tỷ thiết bị (4,66 tỷ người dùng x 3,2 thiết bị/người).

- **Câu hỏi:** Kỷ lục tốc độ mạng lõi (Core Network) là bao nhiêu?  
  **Trả lời:** 44,8 Tbps (2020) trên 1000 km cáp quang giữa Tokyo và Osaka (NTT Japan).

- **Câu hỏi:** Ứng dụng nào yêu cầu độ trễ thấp nhất?  
  **Trả lời:** High-frequency trading, Self-driving cars, Virtual reality, Online gaming, Medical imaging.

---

## 2. MẠNG MÁY TÍNH & INTERNET

### Chuyển mạch gói (Packet Switching)
- **Tại sao chuyển mạch gói thành công?**
  - Hiệu quả: Các gói dữ liệu được định tuyến độc lập, chia sẻ mạng hiệu quả.
  - Khả năng mở rộng: Dễ dàng đáp ứng nhiều thiết bị và lưu lượng.
  - Linh hoạt: Dữ liệu có thể đi qua nhiều đường khác nhau và lắp ráp lại tại đích.
  - Đa ứng dụng: Truyền tải văn bản, hình ảnh, âm thanh, video.

- **Thách thức của chuyển mạch gói:**
  - Mất gói: Do tắc nghẽn mạng hoặc lỗi.
  - Độ trễ: Biến đổi do xử lý gói, xếp hàng.
  - Chất lượng dịch vụ (QoS): Khó đáp ứng các ứng dụng yêu cầu QoS khác nhau.
  - Tắc nghẽn mạng: Khi lưu lượng vượt quá khả năng mạng.

### Bộ giao thức TCP/IP
- **Các tầng giao thức:**
  1. **Application Layer (Tầng ứng dụng):** HTTP, FTP, SMTP, DNS.
  2. **Transport Layer (Tầng giao vận):** TCP (tin cậy), UDP (nhanh, không tin cậy).
  3. **Internet Layer (Tầng liên mạng):** Định tuyến IP.
  4. **Network Interface Layer (Tầng giao diện mạng):** Ethernet, WiFi.

- **Quá trình đóng gói dữ liệu (Encapsulation):**
  `Data` → `Segment` (Transport) → `Packet` (Internet) → `Frame` (Network Interface).

---

## 3. TRUYỀN CẢM HỨNG

- **Câu hỏi:** Công nghệ nào là nền tảng của Internet?  
  **Trả lời:** Chuyển mạch gói (Packet Switching, 1961).

- **Câu hỏi:** Cha đẻ của World Wide Web là ai?  
  **Trả lời:** Tim Berners-Lee.

---

## 4. CÁC ỨNG DỤNG MẠNG

### HTTP (Hypertext Transfer Protocol)
- **HTTP/1.0:** Kết nối không duy trì (Non-persistent).
- **HTTP/1.1:** Kết nối duy trì (Persistent).
- **Cookies:** Quản lý phiên người dùng.
- **Web caching (Proxy server):** Tăng tốc độ truy cập.

### DNS (Domain Name System)
- **Chức năng:** Chuyển đổi tên miền (e.g., `google.com`) thành địa chỉ IP.
- **Cấu trúc:** Root → TLD → Authoritative.

### Email
- **SMTP:** Gửi thư (Push).
- **POP3/IMAP:** Nhận thư (Pull).

### FTP (File Transfer Protocol)
- **Cổng 21:** Điều khiển.
- **Cổng 20:** Truyền dữ liệu.

---

## 5. NGÔN NGỮ JAVA

### Tại sao chọn Java?
1. **Độc lập nền tảng:** "Write Once, Run Anywhere" nhờ JVM.
2. **Thư viện mạnh mẽ:** Hỗ trợ Socket, Multithreading, Security.
3. **Cộng đồng lớn:** Dễ dàng tìm kiếm hỗ trợ và tài liệu.

### Lập trình hướng đối tượng (OOP)
- **Encapsulation (Đóng gói):** Bảo vệ dữ liệu bằng `private`, truy cập qua `getter/setter`.
- **Inheritance (Kế thừa):** Tái sử dụng code từ lớp cha.
- **Polymorphism (Đa hình):** Một hành động có thể hoạt động khác nhau trên các đối tượng khác nhau.
- **Abstraction (Trừu tượng):** Ẩn chi tiết phức tạp, chỉ hiển thị tính năng cần thiết.

### Xử lý ngoại lệ (Exception Handling)
- **Cách sử dụng:**
  ```java
  try {
      connectToServer();
  } catch (IOException e) {
      System.out.println("Lỗi kết nối: " + e.getMessage());
  }
  ```

---

## 6. TÓM TẮT NỘI DUNG

1. **Mạng máy tính:**
   - Vai trò của Internet.
   - Công nghệ chuyển mạch gói.
   - Bộ giao thức TCP/IP.
2. **Các ứng dụng mạng:**
   - HTTP, DNS, SMTP, FTP.
3. **Ngôn ngữ Java:**
   - OOP và các nguyên lý cơ bản.
   - Xử lý ngoại lệ.

---

## 7. HỎI ĐÁP

- **Câu hỏi:** Bạn có thắc mắc gì về nội dung bài học hôm nay?  
- **Gợi ý:** Hãy chuẩn bị câu hỏi cho buổi học tiếp theo.

---

**Enjoy Learning!**