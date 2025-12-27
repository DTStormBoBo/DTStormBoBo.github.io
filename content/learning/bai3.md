---
title: "Bài 3: Quản lý luồng nhập xuất trong Java"
date: 2025-12-17
weight: 3
draft: false
tags: ["JavaScript", "Async"]
summary: "Tổng quan về Input/Output Streams trong Java – nền tảng cho xử lý file, console và lập trình mạng."
---
## **Buổi 3: Quản Lý Luồng Nhập Xuất**  

### **Nội dung chính:**  
1. Bài tập mẫu  
2. Luồng nhập xuất | Bài tập mẫu  
3. Truyền cảm hứng  
4. Quản lý luồng nhập xuất  
5. Bài tập tại lớp  
6. Thuyết trình nhóm  
7. Hỏi & Đáp  

---

## **1. Bài Tập Mẫu: Quản Lý Sinh Viên**  
Viết chương trình Java để quản lý danh sách sinh viên.  

### **Yêu cầu:**  
1. Thông tin mỗi sinh viên bao gồm:  
   - Mã sinh viên  
   - Họ và tên  
   - Ngày sinh  
   - Điểm trung bình  
2. Chương trình cho phép:  
   - Nhập thông tin sinh viên từ bàn phím và lưu vào file.  
   - Đọc thông tin sinh viên từ file và hiển thị ra màn hình.  
   - Sắp xếp danh sách sinh viên theo điểm trung bình từ cao đến thấp và hiển thị danh sách đã sắp xếp.  

---

## **2. Luồng Nhập Xuất | Tổng Quan**  

### **Luồng Nhập Xuất là gì?**  
- Khi đọc/ghi, dữ liệu được di chuyển thành dòng gọi là **luồng**.  
- Luồng chuyển dữ liệu từ **nguồn** tới **đích**: tập tin, thiết bị, socket, hoặc mảng.  
- Dữ liệu trong luồng có 2 dạng: **byte** và **ký tự**.  

### **Phân loại luồng dữ liệu trong Java:**  
1. **Theo loại dữ liệu:**  
   - **Luồng byte (Byte Stream):** Dữ liệu truyền dạng nhị phân.  
   - **Luồng ký tự (Character Stream):** Dữ liệu Unicode.  
2. **Theo thao tác:**  
   - **Input (đọc):** `InputStream` (byte), `Reader` (ký tự).  
   - **Output (ghi):** `OutputStream` (byte), `Writer` (ký tự).  

---

## **3. Luồng Byte (Byte Stream)**  

### **Luồng Byte Đọc (InputStream):**  
- **Lớp cơ sở:** `InputStream`  
- **Các lớp hiện thực:**  
  - `FileInputStream`: Đọc byte từ tập tin.  
  - `ByteArrayInputStream`: Đọc byte từ mảng byte.  
  - `PipedInputStream`: Đọc byte từ piped output stream.  

#### **Ví dụ 3.1: Đọc dữ liệu từ file bằng `FileInputStream`**  
```java
FileInputStream fis = new FileInputStream("data.txt");
int byteData;
while ((byteData = fis.read()) != -1) {
    System.out.print((char) byteData); // Hiển thị ký tự
}
fis.close();
```

---

### **Luồng Byte Ghi (OutputStream):**  
- **Lớp cơ sở:** `OutputStream`  
- **Các lớp hiện thực:**  
  - `FileOutputStream`: Ghi byte vào tập tin.  
  - `ByteArrayOutputStream`: Ghi byte vào mảng byte.  
  - `PipedOutputStream`: Ghi byte vào piped input stream.  

#### **Ví dụ 3.4: Ghi dữ liệu vào file bằng `FileOutputStream`**  
```java
FileOutputStream fos = new FileOutputStream("output.txt");
String data = "Hello, Java IO!";
fos.write(data.getBytes());
fos.close();
```

---

## **4. Luồng Ký Tự (Character Stream)**  

### **Luồng Ký Tự Đọc (Reader):**  
- **Lớp cơ sở:** `Reader`  
- **Các lớp hiện thực:**  
  - `FileReader`: Đọc ký tự từ tập tin.  
  - `BufferedReader`: Đọc ký tự có vùng đệm.  
  - `StringReader`: Đọc chuỗi ký tự.  

#### **Ví dụ 3.9: Đọc file văn bản bằng `FileReader`**  
```java
FileReader fr = new FileReader("data.txt");
int charData;
while ((charData = fr.read()) != -1) {
    System.out.print((char) charData); // Hiển thị ký tự
}
fr.close();
```

---

### **Luồng Ký Tự Ghi (Writer):**  
- **Lớp cơ sở:** `Writer`  
- **Các lớp hiện thực:**  
  - `FileWriter`: Ghi ký tự vào tập tin.  
  - `BufferedWriter`: Ghi ký tự có vùng đệm.  
  - `StringWriter`: Ghi chuỗi ký tự.  

#### **Ví dụ 3.11: Ghi dữ liệu vào file bằng `FileWriter`**  
```java
FileWriter fw = new FileWriter("output.txt");
fw.write("Xin chào, Java!");
fw.close();
```

---

## **5. Luồng Đệm (Buffered Stream)**  

### **Lợi ích của Buffered Stream:**  
- Tăng tốc độ đọc/ghi bằng cách sử dụng vùng đệm.  
- Giảm số lần truy xuất vật lý đến ổ cứng.  

### **Các lớp hỗ trợ:**  
- **Byte Stream:**  
  - `BufferedInputStream`, `BufferedOutputStream`  
- **Character Stream:**  
  - `BufferedReader`, `BufferedWriter`  

#### **Ví dụ 3.15: So sánh hiệu năng với và không có Buffered Stream**  
```java
BufferedOutputStream bos = new BufferedOutputStream(new FileOutputStream("buffered.txt"));
for (int i = 0; i < 100000; i++) {
    bos.write(("Line " + i + "\n").getBytes());
}
bos.close();
```

---

## **6. Luồng Lọc Dữ Liệu (Filtered Stream)**  

### **Các lớp hỗ trợ:**  
- `DataInputStream`, `DataOutputStream`: Đọc/ghi dữ liệu kiểu nguyên thủy (int, float, boolean, ...).  

#### **Ví dụ 3.14: Ghi và đọc dữ liệu kiểu nguyên thủy**  
```java
// Ghi dữ liệu
DataOutputStream dos = new DataOutputStream(new FileOutputStream("data.dat"));
dos.writeInt(42);
dos.writeDouble(3.14);
dos.close();

// Đọc dữ liệu
DataInputStream dis = new DataInputStream(new FileInputStream("data.dat"));
int intValue = dis.readInt();
double doubleValue = dis.readDouble();
dis.close();
```

---

## **7. Bài Tập Tại Lớp: Mã Caesar**  
Viết chương trình mã hóa chuỗi ký tự sử dụng thuật toán mã hóa Caesar.  

### **Gợi ý:**  
- Dịch chuyển mỗi ký tự trong chuỗi theo một số bước (key).  
- Ví dụ: Với key = 3, `A → D`, `B → E`, ...  

#### **Mã hóa Caesar: Code mẫu**  
```java
public class CaesarCipher {
    public static String encrypt(String text, int key) {
        StringBuilder result = new StringBuilder();
        for (char c : text.toCharArray()) {
            if (Character.isLetter(c)) {
                char base = Character.isLowerCase(c) ? 'a' : 'A';
                result.append((char) ((c - base + key) % 26 + base));
            } else {
                result.append(c);
            }
        }
        return result.toString();
    }

    public static void main(String[] args) {
        String text = "Hello, World!";
        int key = 3;
        System.out.println("Encrypted: " + encrypt(text, key));
    }
}
```

---

## **8. Hỏi & Đáp**  
Hãy đặt câu hỏi để làm rõ các khái niệm hoặc ví dụ chưa hiểu rõ.  

**Enjoy Learning!**