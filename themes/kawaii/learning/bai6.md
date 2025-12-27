---
title: "Buổi 6: Lập Trình Socket UDP - Tốc Độ Là Trên Hết"
date: 2025-12-28
draft: false
tags: ["Java", "Networking", "UDP", "DatagramSocket", "Performance"]
categories: ["Lập Trình Mạng"]
description: "Tìm hiểu giao thức UDP không kết nối, so sánh với TCP và cách truyền tải gói tin nhanh chóng bằng DatagramPacket."
---

## 1. Mở đầu: UDP - "Gửi rồi quên" (Fire and Forget)

Trong bài trước, chúng ta thấy TCP rất cẩn thận (bắt tay 3 bước). Nhưng sự cẩn thận đó sinh ra độ trễ (latency).
Trong thế giới Real-time (Livestream, Game Online) hoặc các dịch vụ hạ tầng mạng (DNS, DHCP), chúng ta cần tốc độ hơn là sự hoàn hảo. Đó là lúc **UDP** lên ngôi.

### So sánh nhanh TCP vs UDP

| Đặc điểm | TCP (Transmission Control Protocol) | UDP (User Datagram Protocol) |
| :--- | :--- | :--- |
| **Kết nối** | Có kết nối (Connection-oriented) | Không kết nối (Connectionless) |
| **Độ tin cậy** | Cao (đảm bảo nhận đủ, đúng thứ tự) | Thấp (có thể mất gói, sai thứ tự) |
| **Tốc độ** | Chậm hơn (do thủ tục kiểm tra) | Rất nhanh |
| **Dữ liệu** | Luồng (Stream) | Gói tin (Datagram) |
| **Ví dụ** | Web (HTTP), Email (SMTP), File (FTP) | Video Call, Game, DNS, Logs |

## 2. Cơ chế hoạt động của Socket UDP

Khác với TCP có `ServerSocket` và `Socket`, trong UDP Java chỉ dùng 2 lớp chính cho cả Client và Server:

1.  **`DatagramSocket`:** Giống như cái "hòm thư". Dùng để gửi và nhận thư.
2.  **`DatagramPacket`:** Chính là "bức thư" (gói tin). Chứa dữ liệu (`byte[]`) và địa chỉ người nhận.



> **Lưu ý:** Trong UDP, không có khái niệm "Client kết nối tới Server". Client chỉ đơn giản là đóng gói dữ liệu và ném về phía IP/Port của Server. Server chỉ việc mở cổng và hứng lấy bất cứ thứ gì bay tới.

## 3. Code Thực Chiến: Ứng dụng Chat UDP Đơn Giản

Chúng ta sẽ viết một chương trình: Client gửi tin nhắn, Server nhận và in ra màn hình.

### 3.1. Phía Server (Người hứng tin)

Server phải chạy trước để mở cổng chờ tin nhắn.

```java
import java.net.DatagramPacket;
import java.net.DatagramSocket;

public class UdpServer {
    public static void main(String[] args) {
        int port = 9876;
        try {
            // 1. Tạo Socket và lắng nghe tại cổng 9876
            DatagramSocket serverSocket = new DatagramSocket(port);
            System.out.println("UDP Server đang chạy tại cổng " + port + "...");

            // 2. Tạo mảng byte để chứa dữ liệu nhận được (Buffer)
            byte[] receiveData = new byte[1024]; // Tối đa 1024 bytes mỗi gói

            while (true) {
                // 3. Tạo gói tin rỗng để hứng dữ liệu
                DatagramPacket receivePacket = new DatagramPacket(receiveData, receiveData.length);

                // 4. Chờ nhận dữ liệu (Blocking)
                serverSocket.receive(receivePacket);

                // 5. Xử lý dữ liệu nhận được
                String message = new String(receivePacket.getData(), 0, receivePacket.getLength());
                
                // Lấy thông tin người gửi để có thể phản hồi sau này
                String clientIP = receivePacket.getAddress().getHostAddress();
                int clientPort = receivePacket.getPort();

                System.out.println("Nhận từ [" + clientIP + ":" + clientPort + "]: " + message);
            }
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
3.2. Phía Client (Người ném tin)
Client không cần connect. Chỉ cần gói ghém dữ liệu và gửi đi.

Java

import java.net.DatagramPacket;
import java.net.DatagramSocket;
import java.net.InetAddress;
import java.util.Scanner;

public class UdpClient {
    public static void main(String[] args) {
        try {
            // 1. Tạo Socket (Không cần port cụ thể, hệ thống tự cấp)
            DatagramSocket clientSocket = new DatagramSocket();
            InetAddress serverIP = InetAddress.getByName("localhost");
            int serverPort = 9876;
            
            Scanner scanner = new Scanner(System.in);
            System.out.println("Nhập tin nhắn để gửi (gõ 'exit' để thoát):");

            while (true) {
                System.out.print("Client > ");
                String message = scanner.nextLine();
                if ("exit".equalsIgnoreCase(message)) break;

                // 2. Chuyển chuỗi thành mảng byte
                byte[] sendData = message.getBytes();

                // 3. Đóng gói tin (Dữ liệu + IP Đích + Port Đích)
                DatagramPacket sendPacket = new DatagramPacket(sendData, sendData.length, serverIP, serverPort);

                // 4. Bắn gói tin đi
                clientSocket.send(sendPacket);
            }
            clientSocket.close();
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
4. Những vấn đề kỹ thuật cần lưu ý (Góc nhìn DevOps)
Khi làm việc với UDP, bạn sẽ gặp những tình huống "dở khóc dở cười" mà TCP không có:

Packet Loss (Mất gói): Nếu Server đang bận xử lý gói 1 mà Client bắn tiếp gói 2, gói 2 có thể bị Server (hoặc Router) vứt bỏ không thương tiếc. Code của bạn phải chấp nhận việc mất dữ liệu.

Giới hạn kích thước: Một gói UDP an toàn (safe payload) thường nhỏ hơn 512 bytes (để tránh bị phân mảnh - fragmentation - khi đi qua các router). Đừng cố gửi cả file ảnh qua một gói UDP duy nhất!

Bảo mật: UDP rất dễ bị làm giả địa chỉ IP nguồn (IP Spoofing), dẫn đến các cuộc tấn công DDoS (UDP Flood).