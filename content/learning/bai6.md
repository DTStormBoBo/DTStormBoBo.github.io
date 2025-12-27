---
title: "Bài 6: Lập trình Socket UDP trong Java"
date: 2025-12-20
weight: 6
draft: false
tags: ["Java", "Theory"]
summary: "Giải thích giao thức UDP và cách Java lập trình Socket UDP – nền tảng cho truyền dữ liệu nhanh, không kết nối."
---

#Trong lập trình mạng, không phải lúc nào ứng dụng cũng cần **độ tin cậy tuyệt đối** như TCP.  
Trong nhiều trường hợp, điều quan trọng hơn là **tốc độ truyền nhanh** và **độ trễ thấp**.

Bài học này giới thiệu **UDP Socket** – cơ chế truyền dữ liệu **không kết nối**, được sử dụng rộng rãi trong các ứng dụng thời gian thực.

---

## UDP là gì?

**UDP (User Datagram Protocol)** là giao thức truyền thông **không hướng kết nối**.

Điều này có nghĩa là:

- Không thiết lập kết nối trước khi truyền
- Không đảm bảo dữ liệu đến nơi
- Không đảm bảo thứ tự gói tin
- Không tự động gửi lại gói tin bị mất

UDP gửi dữ liệu theo từng **datagram** (gói tin độc lập).

---

## So sánh TCP và UDP

| TCP | UDP |
|---|---|
| Có kết nối | Không kết nối |
| Đảm bảo dữ liệu | Không đảm bảo |
| Truyền theo luồng | Truyền theo gói |
| Độ trễ cao hơn | Độ trễ thấp |
| Phù hợp dữ liệu quan trọng | Phù hợp dữ liệu thời gian thực |

---

## Khi nào sử dụng UDP?

UDP được sử dụng khi:

- Cần **truyền nhanh**
- Có thể chấp nhận **mất gói tin**
- Dữ liệu được gửi liên tục

Ví dụ ứng dụng UDP:

- Truyền video, audio trực tuyến
- Game online thời gian thực
- Chat broadcast
- DNS
- Multicast, streaming

---

## UDP Socket trong Java

Java hỗ trợ UDP thông qua hai lớp chính:

- **DatagramSocket**: quản lý socket UDP
- **DatagramPacket**: đại diện cho gói dữ liệu UDP

UDP không phân biệt client hay server rõ ràng như TCP.  
Mỗi chương trình chỉ cần **một DatagramSocket để gửi và nhận dữ liệu**.

---

## DatagramPacket là gì?

DatagramPacket là **gói dữ liệu UDP**, bao gồm:

- Dữ liệu cần gửi
- Địa chỉ IP đích
- Số hiệu cổng

Mỗi lần gửi hoặc nhận dữ liệu, UDP làm việc với **một DatagramPacket riêng biệt**.

---

## Luồng dữ liệu trong UDP

UDP **không có luồng InputStream / OutputStream** như TCP.

Quy trình truyền dữ liệu UDP:

1. Tạo DatagramSocket
2. Tạo DatagramPacket chứa dữ liệu
3. Gửi packet đi
4. Nhận packet về
5. Đọc dữ liệu từ packet

Mỗi gói tin là **độc lập**, không liên quan đến các gói khác.

---

## Đặc điểm quan trọng của UDP

- Không kiểm soát lỗi
- Không kiểm soát luồng
- Không bắt tay kết nối
- Gửi nhanh, xử lý đơn giản
- Phù hợp truyền broadcast và multicast

Chính vì vậy, UDP thường được dùng khi **tốc độ quan trọng hơn độ chính xác tuyệt đối**.

---

## Ý nghĩa của lập trình Socket UDP

Nắm vững UDP giúp bạn:

- Hiểu bản chất truyền dữ liệu không kết nối
- Xây dựng ứng dụng thời gian thực
- Phân biệt rõ TCP và UDP trong thiết kế hệ thống
- Chuẩn bị cho các chủ đề nâng cao như:
  - Multicast UDP
  - Java RMI
  - Hệ thống phân tán

---

## Liên hệ với môn Lập trình Mạng máy tính

Trong học phần **Lập trình Mạng máy tính**, UDP được sử dụng trong:

- Socket UDP
- Multicast
- Ứng dụng truyền tin nhanh
- Game, streaming, broadcast

Hiểu UDP giúp bạn **chọn đúng giao thức** cho từng bài toán thực tế.

---

## Kết luận

Qua bài học này, bạn đã:

- Hiểu UDP là gì và cơ chế hoạt động
- Phân biệt được TCP và UDP
- Biết vai trò của DatagramSocket và DatagramPacket
- Hiểu cách truyền dữ liệu không kết nối
- Chuẩn bị nền tảng cho bài Multicast UDP & Java RMI tiếp theo