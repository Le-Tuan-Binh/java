## Getting Started

`ArrayList` là một lớp trong Java thuộc gói `java.util` cung cấp một cấu trúc dữ liệu động, cho phép lưu trữ và quản lý các đối tượng một cách linh hoạt.

Khác với mảng thông thường có kích thước cố định, ArrayList có khả năng **thay đổi kích thước** khi cần thiết, giúp việc thêm, xóa phần tử trở nên dễ dàng hơn.

## Getting Involved

#### 1. Khai báo

Để sử dụng ArrayList, bạn cần import gói `java.util.ArrayList` vào chương trình của mình.

```java
List<dataType> arr = new ArrayList<>();
ArrayList<dataType> arr = new ArrayList<>();
```

**Chú ý:** ArrayList chỉ lưu được các **object**, **không thể** lưu được các **kiểu dữ liệu nguyên thủy** như int, long, float, double... Thay vì đó ta sử dụng lớp wrapper của kiểu dữ liệu đó là Integer, Long, Float, Double...

#### 2. Thêm một phần tử vào ArrayList

Một trong những thao tác quan trọng và thường xuyên nhất khi làm việc với ArrayList là thêm phần tử vào danh sách. Trong phần này, chúng ta sẽ tìm hiểu chi tiết về cách thêm phần tử vào ArrayList và các khía cạnh liên quan.

Có rất nhiều cách thêm phần tử vào ArrayList, tuy nhiên ở bài blog này chúng ta sẽ đề cập tới một số phương thức chính.

**add(DataType dataType)**

Hàm add dùng để thêm một phần tử vào cuối danh sách, đây là cách sử dụng hàm add một cách dễ dàng với ví dụ sau

```java
public static void main(String[] args) {
	ArrayList<String> fruits = new ArrayList<>();

	fruits.add("Apple");
	fruits.add("Banana");
	fruits.add("Cherry");

	System.out.println("Danh sách trái cây: " + fruits);
}
```
