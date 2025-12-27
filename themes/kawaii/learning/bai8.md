---
title: "Lập trình mạng: Multicast UDP và Java RMI"
date: 2025-12-27T16:47:00+07:00
draft: false
categories: ["Lập trình mạng", "Java"]
tags: ["UDP", "Multicast", "RMI", "Distributed Systems", "Network Programming"]
---

# LẬP TRÌNH MẠNG MÁY TÍNH  
**HUTECH - 11/2025**

## KHỞI ĐỘNG ĐẦU GIỜ  
### Nội dung khóa học  
- **Buổi 1:** Tổng quan khóa học  
- **Buổi 2:** Kiến thức nền tảng  
- **Buổi 3:** Quản lý các luồng nhập xuất  
- **Buổi 4:** Quản lý địa chỉ kết nối mạng  
- **Buổi 5:** Lập trình sockets TCP  
- **Buổi 6:** Lập trình socket UDP  
- **Buổi 7:** Đa tuyến và Xử lý đồng thời  
- **Buổi 8:** Multi-cast UDP & Java RMI  
- **Buổi 9:** Báo cáo đồ án học phần  
- **Buổi 10:** Báo cáo đồ án học phần  

---

## BUỔI 8: LẬP TRÌNH MULTICAST UDP & JAVA RMI  

### NỘI DUNG CHÍNH  
1. **Multicast UDP**  
2. **Java RMI**  
3. **Thuyết trình**  
4. **Đánh giá khóa học**  

---

## 1. MULTICAST UDP  

### 1.1. Tổng quan  
Multicast UDP là phương thức gửi dữ liệu từ một nguồn đến nhiều người nhận cùng một lúc (one-to-many).  

### 1.2. Tại sao nên dùng UDP Multicast?  
1. **Hiệu suất cao:** Giảm lưu lượng mạng và giảm tải cho server.  
2. **Đơn giản và nhanh chóng:** Giao thức "gửi và quên", không cần xác nhận.  
3. **Tối ưu hóa cho streaming media:** Phù hợp cho các ứng dụng video/audio streaming.  

### 1.3. Ứng dụng thực tế  
- Truyền phát multimedia trực tiếp.  
- Chat nhóm trực tuyến.  
- Cập nhật phần mềm đồng loạt trong mạng nội bộ.  
- Game đa người chơi.  

### 1.4. Cách thức hoạt động  
- **Địa chỉ Multicast:** Sử dụng dải địa chỉ IP lớp D (`224.0.0.0` đến `239.255.255.255`).  
- **Tham gia nhóm:** Client cần đăng ký tham gia vào một địa chỉ multicast group.  

#### Các bước gửi gói tin (Sender):  
1. Tạo `MulticastSocket`.  
2. Tham gia nhóm (`joinGroup`).  
3. Tạo `DatagramPacket` chứa dữ liệu.  
4. Gửi gói tin (`socket.send()`).  
5. Rời nhóm (`leaveGroup`).  

#### Ví dụ Code (Sender):  
```java
InetAddress group = InetAddress.getByName("224.0.0.1");
MulticastSocket socket = new MulticastSocket();
socket.joinGroup(group);
byte[] msg = "Hello".getBytes();
DatagramPacket packet = new DatagramPacket(msg, msg.length, group, 9876);
socket.send(packet);
socket.leaveGroup(group);
```

#### Các bước nhận gói tin (Receiver):  
1. Tạo `MulticastSocket` lắng nghe ở port tương ứng.  
2. Tham gia nhóm (`joinGroup`).  
3. Tạo gói `DatagramPacket` rỗng.  
4. Nhận gói tin (`socket.receive()`).  
5. Rời nhóm (`leaveGroup`).  

#### Ví dụ Code (Receiver):  
```java
InetAddress group = InetAddress.getByName("224.0.0.1");
MulticastSocket socket = new MulticastSocket(9876);
socket.joinGroup(group);
byte[] buffer = new byte[1000];
DatagramPacket packet = new DatagramPacket(buffer, buffer.length);
socket.receive(packet);
String message = new String(packet.getData(), 0, packet.getLength());
socket.leaveGroup(group);
```

---

## 2. JAVA RMI  

### 2.1. Tổng quan  
Java RMI (Remote Method Invocation) cho phép gọi phương thức từ xa giữa các ứng dụng Java.  

### 2.2. Tại sao dùng Java RMI?  
1. **Đơn giản và dễ sử dụng:** Tích hợp sẵn trong Java.  
2. **Hỗ trợ kiểu dữ liệu phức tạp:** Chuyển các đối tượng qua mạng.  
3. **Hiệu suất tốt:** Dựa trên giao thức TCP/IP.  

### 2.3. Các bước tạo RMI  
1. Định nghĩa giao diện.  
2. Phát triển đối tượng bằng cách cài đặt giao diện remote.  
3. Phát triển chương trình client và server.  
4. Biên dịch file Java.  
5. Tạo stub và skeleton.  
6. Khởi động RMI registry.  
7. Chạy server.  
8. Chạy client.  

#### Ví dụ: Chương trình tính tổng hai số  
- **Bước 1:** Định nghĩa giao diện.  
- **Bước 2:** Cài đặt giao diện remote.  
- **Bước 3:** Phát triển chương trình server.  
- **Bước 4:** Phát triển chương trình client.  

---

## 3. THUYẾT TRÌNH  
Học viên trình bày các bài tập và giải pháp của mình.  

---

## 4. ĐÁNH GIÁ KHÓA HỌC  
Tổng kết và đánh giá các nội dung đã học trong khóa học.  

---

**Enjoy Learning!**