---
title: "Lập trình Đa tuyến và Xử lý Đồng thời trong Java"
date: 2025-12-27T16:50:00+07:00
draft: false
categories: ["Lập trình mạng", "Java", "Concurrency"]
tags: ["Multi-threading", "Socket", "Race Condition", "Deadlock"]
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

## BUỔI 7: LẬP TRÌNH ĐA TUYẾN & XỬ LÝ ĐỒNG THỜI  

### NỘI DUNG CHÍNH  
1. **Bài tập ví dụ**  
2. **Lập trình đa tuyến**  
3. **Xử lý đồng thời**  
4. **Thuyết trình**  
5. **Hỏi & Đáp**  

---

## 1. BÀI TẬP VÍ DỤ  

### Ví dụ 1: Ứng dụng Chat đa tuyến  
**Đề bài:** Xây dựng một ứng dụng chat đa tuyến giữa nhiều client và một server.  
Ứng dụng cho phép nhiều client kết nối đồng thời với server và gửi tin nhắn cho nhau.  

#### Yêu cầu chức năng:  
- **Server:**  
  - Chấp nhận kết nối từ nhiều client cùng lúc.  
  - Hiển thị tên client trong mỗi tin nhắn gửi tới các client khác.  
  - Ghi log tin nhắn vào file `chat_log.txt`.  
- **Client:**  
  - Kết nối tới server qua IP và nhập tên định danh.  
  - Gửi và nhận tin nhắn từ các client khác.  
  - Thoát chương trình bằng từ khóa `exit`.  

#### Cách chạy:  
1. **Chia nhóm:** 1 Server + (n-1) Client.  
2. **Trên máy server:** Chạy `Chat_Server3` và cung cấp địa chỉ IP cho các client.  
3. **Trên máy client:** Chạy `Chat_Client3`, nhập IP và tên để kết nối.  
4. **Chat:** Nhập nội dung tin nhắn.  
5. **Quan sát:** Kiểm tra log trên server và tin nhắn hiển thị trên client.  

---

### Ví dụ 2: Tải file đa tuyến  
**Đề bài:** Viết chương trình tải file từ Internet sử dụng đa tuyến.  

#### Yêu cầu chức năng:  
1. Tải file không đồng bộ (asynchronous) bằng `ExecutorService`.  
2. Tải file tuần tự (synchronous) bằng vòng lặp.  
3. Tự động tạo thư mục `Syn` và `Asyn` nếu chưa tồn tại.  

---

## 2. LẬP TRÌNH ĐA TUYẾN  

### Khái niệm về Thread  
- **Thread:** Một dòng điều khiển tuần tự bên trong chương trình.  
- **Lý do sử dụng thread:**  
  - Tăng hiệu suất và khả năng đáp ứng.  
  - Giải phóng thời gian chờ đợi.  
  - Phân chia tác vụ lớn thành các tác vụ nhỏ hơn.  

### Vòng đời của Thread  
1. **NEW:** Thread được tạo nhưng chưa chạy.  
2. **RUNNABLE:** Thread sẵn sàng hoặc đang chạy.  
3. **NOT-RUNNABLE:** Thread bị chặn hoặc đang chờ.  
4. **TERMINATED:** Thread kết thúc.  

---

## 3. XỬ LÝ ĐỒNG THỜI  

### Race Condition (Điều kiện tranh đua)  
- Xảy ra khi nhiều thread cùng truy cập tài nguyên chung mà không đồng bộ.  

### Deadlock (Khóa chết)  
- Hai thread chờ nhau giải phóng tài nguyên mãi mãi.  

### Giải pháp đồng bộ hóa  
- **`synchronized` keyword:** Đảm bảo chỉ một thread truy cập tài nguyên tại một thời điểm.  
- **Atomic Variables:** Biến nguyên tử giúp thực hiện các phép toán thread-safe.  
- **Locks:** Sử dụng `ReentrantLock` để quản lý khóa linh hoạt.  

---

## 4. THUYẾT TRÌNH  
Học viên trình bày các bài tập và giải pháp của mình.  

---

## 5. HỎI & ĐÁP  
Giải đáp các thắc mắc và thảo luận về các vấn đề trong bài học.  

---

**Enjoy Learning!**