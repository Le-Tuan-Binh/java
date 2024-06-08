## Getting Started

`ArrayList` là một lớp trong Java thuộc gói `java.util` cung cấp một cấu trúc dữ liệu động, cho phép lưu trữ và quản lý các đối tượng một cách linh hoạt.

Khác với mảng thông thường có kích thước cố định, ArrayList có khả năng **thay đổi kích thước** khi cần thiết, giúp việc thêm, xóa phần tử trở nên dễ dàng hơn.

## Getting Involved

### Initializing and Using ArrayList

Để sử dụng ArrayList, bạn cần import gói `java.util.ArrayList` vào chương trình của mình.

Dưới đây là một số ví dụ cơ bản về cách khởi tạo và sử dụng ArrayList trong Java.

```java
import java.util.ArrayList;

public class ArrayList {
	public static void main(String[] args) {

		// Khởi tạo một ArrayList chứa các phần tử kiểu String
		ArrayList<String> fruits = new ArrayList<>();

		// Thêm các phần tử vào ArrayList
		fruits.add("Apple");
		fruits.add("Banana");
		fruits.add("Cherry");

		// Hiển thị các phần tử của ArrayList
		System.out.println("Các loại trái cây: " + fruits);
	}
}
```

**Chú ý:** ArrayList chỉ lưu được các **object**, **không thể** lưu được các **kiểu dữ liệu nguyên thủy** như int, long, float, double... Thay vì đó ta sử dụng lớp wrapper của kiểu dữ liệu đó là Integer, Long, Float, Double...
