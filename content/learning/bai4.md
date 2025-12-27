---
title: "Bài 4: Quản lý địa chỉ kết nối mạng trong Java"
date: 2025-12-18
weight: 4
draft: false
tags: ["Java", "Socket", "File Transfer"]
summary: "Tìm hiểu cách Java quản lý địa chỉ mạng thông qua InetAddress, URL, URLConnection và DNS."
---

## BUỔI 4: QUẢN LÝ ĐỊA CHỈ KẾT NỐI MẠNG

### Nội dung chính:
1. **Khởi động đầu giờ**  
2. **Bài tập mẫu**  
3. **Quản lý địa chỉ kết nối mạng**  
4. **Bài tập tại lớp**  
5. **Trắc nghiệm ôn tập**  
6. **Thuyết trình**  
7. **Hỏi & Đáp**  

---

## 2. BÀI TẬP MẪU

### Ví dụ: **Web Crawler**
Viết một chương trình Web Crawler đơn giản để lấy danh sách các URL từ một trang web ban đầu.  

#### Yêu cầu chức năng:
1. **Lập danh sách URL cần crawl:**
   - Người dùng nhập địa chỉ trang web ban đầu.
   - Người dùng cung cấp độ sâu tìm kiếm.
   - Chương trình chạy và lập danh sách các đường link cần crawl và lưu vào file.

2. **Hiển thị danh sách các URL đã lấy được:**
   - Chương trình cho phép người dùng chọn menu hiển thị danh sách các URL đã lấy được từ trang web ban đầu.

3. **Kết thúc chương trình.**

---

## 3. QUẢN LÝ ĐỊA CHỈ KẾT NỐI MẠNG

### **Lớp URL** | Ví dụ 4.1

#### Nội dung:
- **Thư viện:** `import java.net.URL;`  
- **Khởi tạo:**
  ```java
  URL url = new URL("https://www.example.com");
  ```
- **Thuộc tính cơ bản:**
  ```java
  String protocol = url.getProtocol();
  String host = url.getHost();
  int port = url.getPort();
  String path = url.getPath();
  String query = url.getQuery();
  ```
- **Cách sử dụng:**
  ```java
  InputStream inputStream = url.openStream();
  BufferedReader reader = new BufferedReader(new InputStreamReader(inputStream));
  String line;
  while ((line = reader.readLine()) != null) {
      // Xử lý dữ liệu
  }
  reader.close();
  ```

---

### **Giao diện Iterator** | Ví dụ 4.2

#### Nội dung:
- **Mục đích:** Duyệt qua một tập hợp phần tử mà không cần biết cấu trúc bên trong.  
- **Thư viện:** `import java.util.Iterator;`  
- **Khai báo:**
  ```java
  Iterator<T> iterator = collection.iterator();
  ```
- **Phương thức cơ bản:**
  - `boolean hasNext()`: Kiểm tra xem có phần tử tiếp theo không.  
  - `T next()`: Trả về phần tử tiếp theo.  
  - `void remove()`: Xóa phần tử hiện tại.  

- **Cách sử dụng:**
  ```java
  List<String> names = new ArrayList<>();
  names.add("John");
  names.add("Mary");
  names.add("Alice");
  Iterator<String> iterator = names.iterator();
  while (iterator.hasNext()) {
      String name = iterator.next();
      System.out.println(name);
  }
  ```

---

### **Lớp Matcher & Pattern** | Ví dụ 4.3

#### Nội dung:
- **Mục đích:** Làm việc với dữ liệu và thực hiện các tác vụ như duyệt qua, so khớp và trích xuất thông tin từ các chuỗi.  
- **Thư viện:**
  ```java
  import java.util.regex.Pattern;
  import java.util.regex.Matcher;
  ```
- **Khai báo:**
  ```java
  Pattern pattern = Pattern.compile("regex");
  Matcher matcher = pattern.matcher("input");
  ```
- **Phương thức cơ bản:**
  - `boolean find()`: Tìm kiếm một phần tử khớp với regex.  
  - `String group()`: Trả về phần tử khớp hiện tại.  
  - `int start()`: Vị trí bắt đầu của phần tử khớp.  
  - `int end()`: Vị trí kết thúc của phần tử khớp.  

- **Cách sử dụng:**
  ```java
  String input = "Hello 123 Java";
  Pattern pattern = Pattern.compile("\\d+");
  Matcher matcher = pattern.matcher(input);
  while (matcher.find()) {
      String match = matcher.group();
      int start = matcher.start();
      int end = matcher.end();
      System.out.println("Match: " + match + " (Start: " + start + ", End: " + end + ")");
  }
  ```

---

### **Regular Expression (Regex)**

#### Mục đích:
Regex là một chuỗi ký tự đặc biệt được sử dụng để tìm kiếm, so khớp và xử lý các chuỗi ký tự theo một mẫu cụ thể.

#### Cú pháp cơ bản:
- `.`: Đại diện cho bất kỳ ký tự nào.  
- `[]`: Xác định một tập hợp các ký tự. Ví dụ `[aeiou]` tìm kiếm bất kỳ ký tự nguyên âm nào.  
- `*`: Xác định sự xuất hiện 0 hoặc nhiều lần của một mẫu trước đó.  
- `+`: Xác định sự xuất hiện ít nhất một lần của một mẫu trước đó.  
- `?`: Xác định sự xuất hiện 0 hoặc 1 lần của một mẫu trước đó.  
- `|`: Xác định sự tương đương logic "hoặc" giữa các mẫu.  

#### Ví dụ minh họa:
- Mẫu `a.b` sẽ tìm kiếm các chuỗi có chữ "a" sau đó là bất kỳ ký tự nào, và sau đó là chữ "b". Ví dụ: `acb`, `axb`, `azb`.  
- Mẫu `[0-9]+` sẽ tìm kiếm các chuỗi gồm ít nhất một chữ số từ 0 đến 9. Ví dụ: `123`, `0`, `99`.  
- Mẫu `[A-Za-z]+` sẽ tìm kiếm các chuỗi gồm ít nhất một chữ cái từ A đến Z hoặc từ a đến z. Ví dụ: `abc`, `Hello`, `XYZ`.  

---

### **Lớp HashSet** | Ví dụ 4.4

#### Nội dung:
- **Mục đích:** Lưu trữ tập hợp các phần tử duy nhất, không trùng lặp.  
- **Cách sử dụng:**
  ```java
  HashSet<String> set = new HashSet<>();
  set.add("apple");
  set.add("banana");
  set.add("orange");
  set.add("apple"); // Phần tử trùng lặp sẽ bị loại bỏ
  System.out.println(set); // Output: [apple, orange, banana]
  ```

---

### **Lớp HashMap** | Ví dụ 4.5

#### Nội dung:
- **Mục đích:** Lưu trữ và truy xuất dữ liệu dựa trên cặp khóa-giá trị.  
- **Cách sử dụng:**
  ```java
  HashMap<String, Integer> map = new HashMap<>();
  map.put("apple", 10);
  map.put("banana", 5);
  map.put("orange", 8);
  map.put("apple", 12); // Cập nhật giá trị cho khóa đã tồn tại
  System.out.println(map); // Output: {apple=12, orange=8, banana=5}
  ```

---

## 4. BÀI TẬP TẠI LỚP

### **Search Engine**
Viết một chương trình Search Engine đơn giản cho phép tìm kiếm từ khóa trên các trang web.  

#### Yêu cầu chức năng:
1. Nhập địa chỉ website ban đầu và độ sâu tìm kiếm.  
2. Nhập từ khóa cần tìm kiếm.  
3. Lập danh sách các đường link cần crawl từ website ban đầu theo độ sâu tìm kiếm.  
4. Tìm kiếm từ khóa trong danh sách các đường link và lưu các đường link có chứa từ khóa tìm kiếm, số lần xuất hiện từ khóa vào một file theo thứ tự số lần xuất hiện từ khóa giảm dần.  
5. Kết thúc chương trình.  

#### Gợi ý:
- Phát triển dựa trên phiên bản WebCrawler.  
- Sử dụng `HashMap` để lưu số lần từ khóa xuất hiện.  
- Sử dụng `TreeMap` và `Comparator` để sắp xếp các đường link theo thứ tự số lần xuất hiện từ khóa giảm dần.  

---

## 5. TRẮC NGHIỆM ÔN TẬP

...existing content...

---

## 6. THUYẾT TRÌNH

...existing content...

---

## 7. HỎI & ĐÁP

...existing content...

---

**ENJOY LEARNING!**