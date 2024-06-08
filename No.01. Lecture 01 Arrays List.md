## Getting Started

`ArrayList` là một lớp trong Java thuộc gói `java.util` cung cấp một cấu trúc dữ liệu động, cho phép lưu trữ và quản lý các đối tượng một cách linh hoạt.

Khác với mảng thông thường có kích thước cố định, ArrayList có khả năng **thay đổi kích thước** khi cần thiết, giúp việc thêm, xóa phần tử trở nên dễ dàng hơn.

## Getting Involved

#### 1. Khai báo

Để sử dụng ArrayList, bạn cần import gói `java.util.ArrayList` vào chương trình của mình.

**Khai báo**

```java
List<dataType> arr = new ArrayList<>();
ArrayList<dataType> arr = new ArrayList<>();
```

**Chú ý:** ArrayList chỉ lưu được các **object**, **không thể** lưu được các **kiểu dữ liệu nguyên thủy** như int, long, float, double... Thay vì đó ta sử dụng lớp wrapper của kiểu dữ liệu đó là Integer, Long, Float, Double...
