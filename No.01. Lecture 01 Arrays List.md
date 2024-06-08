## Getting Started

`ArrayList` là một lớp trong Java thuộc gói `java.util` cung cấp một cấu trúc dữ liệu động, cho phép lưu trữ và quản lý các đối tượng một cách linh hoạt.

Khác với mảng thông thường có kích thước cố định, ArrayList có khả năng **thay đổi kích thước** khi cần thiết, giúp việc thêm, xóa phần tử trở nên dễ dàng hơn.

## Getting Involved

### 1. Khai báo

Để sử dụng ArrayList, bạn cần import gói `java.util.ArrayList` vào chương trình của mình.

```java
List<dataType> arr = new ArrayList<>();
ArrayList<dataType> arr = new ArrayList<>();
ArrayList<String> fruits = new ArrayList<>(<initialSize>);
ArrayList<String> fruits = new ArrayList<>(Arrays.asList(value1, value2));
```

**Chú ý:** ArrayList chỉ lưu được các **object**, **không thể** lưu được các **kiểu dữ liệu nguyên thủy** như int, long, float, double... Thay vì đó ta sử dụng lớp wrapper của kiểu dữ liệu đó là Integer, Long, Float, Double...

### 2. Thêm một phần tử vào ArrayList

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

**add(int index, DataType dataType)**

Đôi khi, bạn cần thêm phần tử vào một vị trí cụ thể trong danh sách. Bạn có thể sử dụng phương thức add(int index, E element) để thực hiện điều này.

```java
public static void main(String[] args) {
	ArrayList<String> fruits = new ArrayList<>();

	fruits.add("Apple");
	fruits.add("Banana");
	fruits.add("Cherry");

	// Thêm vào trước Banana (index = 1)
	fruits.add(1, "Blueberry");

	System.out.println("Danh sách trái cây: " + fruits);
}
```

**addAll(Collection<? extends E> c)**

Phương thức `addAll(Collection<? extends E> c)` cho phép bạn thêm tất cả các phần tử từ một Collection khác vào ArrayList.

Điều này rất hữu ích khi bạn muốn hợp nhất hai danh sách hoặc sao chép các phần tử từ một danh sách vào một danh sách khác.

```java
public static void main(String[] args) {
	ArrayList<String> fruits = new ArrayList<>();
	fruits.add("Apple");
	fruits.add("Banana");

	List<String> moreFruits = new ArrayList<>();
	moreFruits.add("Cherry");
	moreFruits.add("Dragon");

	fruits.addAll(moreFruits);

	System.out.println("Danh sách trái cây: " + fruits);
}
```

**addAll(int index, Collection<? extends E> c)**

Phương thức `addAll(int index, Collection<? extends E> c)` cho phép bạn thêm tất cả các phần tử từ một Collection khác vào ArrayList tại một vị trí cụ thể.

```java
public static void main(String[] args) {
	ArrayList<String> fruits = new ArrayList<>();
	fruits.add("Apple");
	fruits.add("Banana");

	List<String> moreFruits = new ArrayList<>();
	moreFruits.add("Cherry");
	moreFruits.add("Date");

	// Thêm tất cả các phần tử từ moreFruits vào vị trí thứ hai (index = 1) trong fruits
	fruits.addAll(1, moreFruits);

	System.out.println("Danh sách trái cây: " + fruits);
}
```

**Collections.addAll(Collection<? super T> c, T... elements)**

Trong đó:

-   c: Collection đích, tức là ArrayList hoặc một Collection khác mà bạn muốn thêm các phần tử vào.

-   elements: Các phần tử cần thêm vào Collection. Đây là một danh sách các phần tử được truyền vào dưới dạng các tham số biến đổi (varargs).

```java
public static void main(String[] args) {
	ArrayList<String> fruits = new ArrayList<>();
	fruits.add("Apple");
	fruits.add("Banana");

	// Tạo một mảng các phần tử cần thêm
	String[] moreFruits = {"Cherry", "Date", "Elderberry"};

	// Thêm tất cả các phần tử từ mảng moreFruits vào fruits
	Collections.addAll(fruits, moreFruits);

	System.out.println("Danh sách trái cây: " + fruits);
}
```

Bạn cũng có thể thêm trực tiếp mà không cần qua một mảng

```java
 Collections.addAll(fruits, "Cherry", "Date", "Elderberry");
```

### 3. Truy cập đến một phần tử trong ArrayList

Để truy cập vào các phần tử trong array list, ta truy cập thông qua chỉ số tương tự như mảng.

Tuy nhiên có một số sự khác biệt, để truy cập các phần tử trong ArrayList, bạn sử dụng phương thức get(). Phương thức này trả về giá trị của phần tử tại chỉ số (index) được chỉ định.

```java
import java.util.ArrayList;

 public static void main(String[] args) {
	ArrayList<String> fruits = new ArrayList<>();
	fruits.add("Apple");
	fruits.add("Banana");
	fruits.add("Cherry");
	String fruit = fruits.get(1);
	System.out.println("Phần tử tại chỉ số 1: " + fruit);
}
```

### 4. Duyệt qua các phần tử trong danh sách

Java cung cấp nhiều cách hiện đại và tiện lợi để duyệt qua các phần tử trong ArrayList. Ngoài các phương thức truyền thống như sử dụng `vòng lặp for` và `while`, Java 8 và các phiên bản mới hơn đã giới thiệu một số tính năng mới như `for-each`, `Iterator`, `ListIterator`, và đặc biệt là `Stream API`. Dưới đây là chi tiết về các phương pháp hiện đại này.

**Vòng lặp for**

```java
public static void main(String[] args) {
	ArrayList<String> fruits = new ArrayList<>();
	fruits.add("Apple");
	fruits.add("Banana");
	fruits.add("Cherry");
	for(int i = 0; i < fruits.size(); i++){
		System.out.print(fruits.get(i) + " ");
	}
}
```

**Vòng lặp for-each**

```java
public static void main(String[] args) {
	ArrayList<String> fruits = new ArrayList<>();
	fruits.add("Apple");
	fruits.add("Banana");
	fruits.add("Cherry");

	for (String fruit : fruits) {
		System.out.println("Trái cây: " + fruit);
	}
}
```

**Sử dụng Iterator**

Iterator là một công cụ mạnh mẽ cho phép duyệt qua các phần tử của ArrayList một cách an toàn và có khả năng loại bỏ phần tử trong khi duyệt.

**1. Phương Thức Duyệt Qua**

-   boolean hasNext(): Kiểm tra xem còn phần tử nào tiếp theo không.
-   E next(): Trả về phần tử tiếp theo và di chuyển con trỏ tới phần tử đó.

**2. Phương Thức Sửa Đổi**

-   void remove(): Xóa phần tử cuối cùng được trả về bởi next() hoặc previous(). Phương thức này chỉ có thể được gọi một lần cho mỗi lần gọi next() hoặc previous().

```java
public static void main(String[] args) {
	ArrayList<String> fruits = new ArrayList<>();
	fruits.add("Apple");
	fruits.add("Banana");
	fruits.add("Cherry");

	Iterator<String> iterator = fruits.iterator();
	while (iterator.hasNext()) {
		String fruit = iterator.next();
		System.out.println("Trái cây: " + fruit);
	};
}
```

**Sử Dụng ListIterator**

`ListIterator` là một phiên bản nâng cao của `Iterator`, cho phép duyệt qua ArrayList theo cả hai hướng (`từ đầu đến cuối và từ cuối đến đầu`), cũng như cung cấp các phương thức để sửa đổi các phần tử.

Một số phương thức của `ListIterator`

**1. Phương Thức Duyệt Qua**

-   boolean hasNext(): Kiểm tra xem còn phần tử nào tiếp theo không.
-   E next(): Trả về phần tử tiếp theo và di chuyển con trỏ tới phần tử đó.
-   boolean hasPrevious(): Kiểm tra xem còn phần tử nào trước đó không.
-   E previous(): Trả về phần tử trước đó và di chuyển con trỏ lùi lại một bước.

**2. Phương Thức Sửa Đổi**

-   void remove(): Xóa phần tử cuối cùng được trả về bởi next() hoặc previous(). Phương thức này chỉ có thể được gọi một lần cho mỗi lần gọi next() hoặc previous().
-   void set(E e): Thay thế phần tử cuối cùng được trả về bởi next() hoặc previous() bằng phần tử được chỉ định.
-   void add(E e): Chèn phần tử được chỉ định vào danh sách ngay trước phần tử sẽ được trả về bởi lần gọi next() tiếp theo và sau phần tử sẽ được trả về bởi lần gọi previous() tiếp theo.

```java
public static void main(String[] args) {
	ArrayList<String> fruits = new ArrayList<>();
	fruits.add("Apple");
	fruits.add("Banana");
	fruits.add("Cherry");

	ListIterator<String> listIterator = fruits.listIterator();

	System.out.println("Duyệt thuận chiều:");
	while (listIterator.hasNext()) {
		String fruit = listIterator.next();
		System.out.println("Trái cây: " + fruit);
	}

	System.out.println("Duyệt ngược lại:");
	while (listIterator.hasPrevious()) {
		String fruit = listIterator.previous();
		System.out.println("Trái cây: " + fruit);
	}
}
```

**Sử dụng Stream API**

`Stream API` được giới thiệu trong Java 8, cung cấp một cách `hiện đại` và `linh hoạt` để xử lý các tập hợp dữ liệu. Bạn có thể sử dụng Stream để duyệt qua các phần tử, áp dụng các phép biến đổi, và thực hiện các phép tính trên ArrayList.

```java
public static void main(String[] args) {
	ArrayList<String> fruits = new ArrayList<>();
	fruits.add("Apple");
	fruits.add("Banana");
	fruits.add("Cherry");

	// Sử dụng for each để duyệt qua các phần tử và in ra màn hình
	fruits.forEach(fruit -> System.out.println("Trái cây: " + fruit));

	// Sử dụng Stream API để lọc các phần tử bắt đầu bằng chữ "B" và in ra màn hình
	List<String> filteredFruits = fruits.stream()
			.filter(fruit -> fruit.startsWith("B"))
			.toList();
	System.out.println("Trái cây bắt đầu bằng chữ B: " + filteredFruits);

	// Sử dụng Stream API để chuyển đổi các phần tử sang chữ in hoa
	List<String> upperCaseFruits = fruits.stream()
			.map(String::toUpperCase)
			.toList();
	System.out.println("Trái cây in hoa: " + upperCaseFruits);
}
```

### 5. Nhập danh sách từ bàn phím

```java
public static void main(String[] args) {
	// Khởi tạo một đối tượng Scanner để nhập từ người dùng
	Scanner scanner = new Scanner(System.in);

	// Khai báo một ArrayList để lưu trữ các số nguyên
	ArrayList<Integer> numbers = new ArrayList<>();

	// Nhập số lượng phần tử của mảng từ người dùng
	System.out.print("Nhập số lượng phần tử của mảng: ");
	int n = scanner.nextInt();

	// Nhập các phần tử của mảng từ người dùng và lưu vào ArrayList
	System.out.println("Nhập các phần tử của mảng:");
	for (int i = 0; i < n; i++) {
		int num = scanner.nextInt();
		numbers.add(num);
	}

	// In ra mảng đã nhập
	System.out.println("Mảng đã nhập: " + numbers);
}
```

### 6. Một số phương thức của ArrayList

#### 6.1 Hàm contains()

Phương thức `.contains()` được khai báo trong interface `List` và được triển khai trong class `ArrayList`.

    arrayList.contains(obj);

Nó được sử dụng để kiểm tra xem phần tử có trong ArrayList được chỉ định hay không. Hàm trả về giá trị boolean là `true` nếu phần tử có mặt và `false` nếu không.

```java
public static void main(String[] args) {

	ArrayList<String> fruitList = new ArrayList<String>();

	fruitList.add("Mangos");
	fruitList.add("Bananas");
	fruitList.add("Watermelons");
	fruitList.add("Grapes");

	boolean areOrangesPresent = fruitList.contains("Oranges");
	boolean areBananasPresent = fruitList.contains("Bananas");

	System.out.println("Fruit list contains oranges: "+ areOrangesPresent);
	System.out.println("Fruit list contains bananas: "+ areBananasPresent);
}
```

#### 6.2 Hàm forEach()

Phương thức `.forEach()` thực hiện một hành động được chỉ định trên từng phần tử trong ArrayList. Phương thức này duyệt qua từng phần tử trong ArrayList cho đến khi tất cả các phần tử đã được xử lý hoặc một ngoại lệ được đưa ra từ hành động.

    arrayList.forEach(Consumer<E> action);

Trong đó:

-   arrayList: Tên biến của danh sách ArrayList
-   Consumer: Một giao diện hàm (functional interface) đại diện cho một hoạt động cần được thực hiện. Nó có thể được sử dụng như mục tiêu gán cho một biểu thức lambda hoặc tham chiếu đến một phương thức nào.
-   action: Hoạt động nhận một phần tử của kiểu E trong ArrayList làm đối số duy nhất của nó và không trả về bất kỳ giá trị nào.

Nó chỉ lặp qua các phần tử mà không sửa đổi ArrayList và không trả về bất kỳ giá trị nào.

```java
public static void main(String[] args) {
	ArrayList<String> students = new ArrayList<>();

	students.add("Lê Tuấn Bình");
	students.add("Bình Lê Tuấn");
	students.add("TBin");
	students.add("TBinT");

	students.forEach((s) -> System.out.println(s));
}
```

#### 6.3 Hàm indexOf()

Phương thức `.indexOf()` trả về vị trí lần xuất hiện đầu tiên của phần tử được chỉ định trong ArrayList. Nếu không tìm thấy phần tử, -1 được trả về.

    arrayList.indexOf(element);

Nếu tồn tại chỉ số của lần xuất hiện đầu tiên của phần tử sẽ được trả về, ngay cả khi giá trị là null. Nếu không tìm thấy phần tử, -1 sẽ được trả về.

```java
public static void main(String[] args) {
	ArrayList<String> animals = new ArrayList<>();

	animals.add("Lion");
	animals.add("Tiger");
	animals.add("Cat");
	animals.add("Dog");
	animals.add("Tiger");
	animals.add("Lion");
	animals.add("Tiger");

	System.out.println(animals.indexOf("Tiger"));
	System.out.println(animals.indexOf("Elephant"));
}
```

#### 6.4 Hàm isEmpty()

Hàm `.isEmpty()` kiểm tra xem ArrayList đã cho có trống hay không. Nó trả về `true` nếu ArrayList trống và trả về `false` nếu nó không trống.

```java
public static void main(String[] args) {
	ArrayList<String> fruits = new ArrayList<String>();

	System.out.println("Is fruits empty: " + fruits.isEmpty());

	fruits.add("kiwi");
	fruits.add("pineapple");
	fruits.add("mango");

	System.out.println("Is fruits empty: " + fruits.isEmpty());
}
```

### 7. Một số hàm liên quan đến xóa phần tử ra khỏi danh sách

Khi làm việc với danh sách trong Java, có một số phương thức quan trọng để loại bỏ phần tử khỏi danh sách. Dưới đây là một số phương thức phổ biến mà bạn có thể sử dụng như remove(), removeAll(), removeIf(), clear()...

#### 7.1 Hàm remove()

Phương thức `.remove()` được sử dụng để xóa các phần tử đã chỉ định khỏi các đối tượng của lớp `ArrayList`.

Một phần tử có thể được loại bỏ khỏi đối tượng của ArrayList bằng cách truyền vào phương thức `.remove()`. Nó có thể được tham chiếu theo giá trị hoặc vị trí của phần tử đó.

    arrayList.remove(elementValue/elementIndex);

Trong ví dụ bên dưới, một thể hiện `ArrayList` sinh viên trống được tạo và có thể chứa các phần tử kiểu Chuỗi.

Tiếp theo, một vài phần tử được thêm bằng phương thức `.add()`. Cuối cùng, hai sinh viên sẽ bị xóa khỏi ArrayList bằng `.remove()`

```java
 public static void main(String[] args) {

	ArrayList<String> studentList = new ArrayList<String>();

	studentList.add("Lê Tuấn Bình");
	studentList.add("Nguyễn Thị Minh Châu");
	studentList.add("Trần Lê Quốc Khánh");
	studentList.add("Bùi Thanh Tú");

	studentList.remove(0);
	studentList.remove("Nguyễn Thị Minh Châu");

	System.out.println(studentList);
}
```

Tuy nhiên đối với trường hợp mảng là một các số nguyên cần đảm bảo độ chính xác để chương trình phân biệt được giữa chỉ số và giá trị. Ta cần đảm bảo việc ép kiểu để chương trình có thể hoạt động chính xác.

```java
public static void main(String[] args) {
	List<Integer> arr = new ArrayList<>();
	int a[] = {1, 2, 2, 2, 3, 3, 5};

	// Thêm các phần tử của mảng a vào danh sách arr
	for(int x : a) {
		arr.add(x);
	}
	// Loại bỏ phần tử có chỉ số là 1 (tính từ 0)
	arr.remove(1);

	// Loại bỏ phần tử có giá trị là 3
	arr.remove((Object)(3));

	// In các phần tử còn lại trong danh sách
	for(int x : arr) {
		System.out.print(x + " ");
	}
}
```
