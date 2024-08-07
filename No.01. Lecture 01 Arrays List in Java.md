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

#### 2.1 add(DataType dataType)

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

#### 2.2 add(int index, DataType dataType)

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

#### 2.3 addAll(Collection<? extends E> c)

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

#### 2.4 addAll(int index, Collection<? extends E> c)

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

#### 2.5 Collections.addAll(Collection<? super T> c, T... elements)

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

#### 4.1 Vòng lặp for

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

#### 4.2 Vòng lặp for-each

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

#### 4.3 Sử dụng Iterator

Iterator là một công cụ mạnh mẽ cho phép duyệt qua các phần tử của ArrayList một cách an toàn và có khả năng loại bỏ phần tử trong khi duyệt.

##### 4.3.1. Phương Thức Duyệt Qua

-   boolean hasNext(): Kiểm tra xem còn phần tử nào tiếp theo không.
-   E next(): Trả về phần tử tiếp theo và di chuyển con trỏ tới phần tử đó.

##### 4.3.2. Phương Thức Sửa Đổi

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

#### 4.4 Sử Dụng ListIterator

`ListIterator` là một phiên bản nâng cao của `Iterator`, cho phép duyệt qua ArrayList theo cả hai hướng (`từ đầu đến cuối và từ cuối đến đầu`), cũng như cung cấp các phương thức để sửa đổi các phần tử.

Một số phương thức của `ListIterator`

##### 4.4.1. Phương Thức Duyệt Qua

-   boolean hasNext(): Kiểm tra xem còn phần tử nào tiếp theo không.
-   E next(): Trả về phần tử tiếp theo và di chuyển con trỏ tới phần tử đó.
-   boolean hasPrevious(): Kiểm tra xem còn phần tử nào trước đó không.
-   E previous(): Trả về phần tử trước đó và di chuyển con trỏ lùi lại một bước.

##### 4.4.4.2. Phương Thức Sửa Đổi

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

#### 4.5 Sử dụng Stream API

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
-   Consumer: Một Functional Interface đại diện cho một hoạt động cần được thực hiện. Nó có thể được sử dụng như mục tiêu gán cho một biểu thức lambda hoặc tham chiếu đến một phương thức nào.
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

#### 6.5 Hàm toArray()

Phương thức `.toArray()` của lớp ArrayList là một phương thức phổ biến trong Java để chuyển đổi một ArrayList thành một mảng và trả về mảng vừa tạo. Mảng trả về chứa tất cả các phần tử trong ArrayList theo đúng thứ tự.

    <T> T[] toArray(T[] array)

Trong ví dụ bên dưới, phương thức `.toArray()` được sử dụng để chuyển đổi một ArrayList có tên FruitList chứa các chuỗi thành một mảng các chuỗi. Sau khi được chuyển đổi, mảng kết quả có tên FruitArray sẽ được in ra.

```java
public static void main(String[] args) {
	ArrayList<String> fruitsList = new ArrayList<>();
	fruitsList.add("Apple");
	fruitsList.add("Banana");
	fruitsList.add("Orange");

	String[] fruitsArray = (String[]) fruitsList.toArray();
	System.out.println("Fruits Array: " + Arrays.toString(fruitsArray));
}
```

Trong ví dụ này, phương thức `.toArray()` được sử dụng để chuyển đổi một ArrayList có tên là colorList chứa các chuỗi thành một mảng đối tượng. Sau khi được chuyển đổi, mảng kết quả có tên colorArray sẽ được in ra.

```java
 public static void main(String[] args) {
	ArrayList<String> colorsList = new ArrayList<>();
	colorsList.add("Red");
	colorsList.add("Green");
	colorsList.add("Blue");

	Object[] colorsArray = colorsList.toArray();
	System.out.println("Colors Array: " + Arrays.toString(colorsArray));
}
```

#### 6.6 Hàm set()

Phương thức `.set()` thay thế một phần tử tại một vị trí được chỉ định bằng một phần tử hoặc giá trị khác . Sau khi thực hiện, phần tử được thay thế sẽ được trả về.

    set(int index, E element)

Lưu ý: Phần tử mới phải có cùng kiểu dữ liệu với các phần tử còn lại trong đối tượng arrayList. Nếu không, sẽ xảy ra lỗi.

#### 6.7 Hàm size()

Phương thức .size() của lớp ArrayList trả về số phần tử trong danh sách.

```java
public static void main(String[] args) {
    // Create an ArrayList of Strings
	ArrayList<String> list = new ArrayList<>();

	// Add some elements to the list
	list.add("Apple");
	list.add("Banana");
	list.add("Orange");

	// Get the size of the list
	int size = list.size();

	// Print the size of the list
	System.out.println("Size of list: " + size);
}
```

```java
public static void main(String[] args) {
	List<String> colors = new ArrayList<>();
	colors.add("Red");
	colors.add("Green");
	colors.add("Blue");

	// In danh sách trước khi thay đổi
	System.out.println("Danh sách ban đầu: " + colors);

	// Thay đổi giá trị của phần tử ở chỉ số 1 thành "Yellow"
	colors.set(1, "Yellow");

	// In danh sách sau khi thay đổi
	System.out.println("Danh sách sau khi thay đổi: " + colors);
}
```

### 7. Xóa phần tử ra khỏi danh sách

Khi làm việc với danh sách trong Java, có một số phương thức quan trọng để loại bỏ phần tử khỏi danh sách. Dưới đây là một số phương thức phổ biến mà bạn có thể sử dụng như remove(), removeAll(), removeIf(), clear()...

#### 7.1 Hàm remove()

Phương thức `.remove()` được sử dụng để xóa các phần tử đã chỉ định khỏi các đối tượng của lớp `ArrayList`.

Một phần tử có thể được loại bỏ khỏi đối tượng của ArrayList bằng cách truyền vào phương thức `.remove()`. Nó có thể được tham chiếu theo giá trị hoặc vị trí của phần tử đó.

    arrayList.remove(elementValue/elementIndex);

Loại bỏ phần tử đầu tiên trong danh sách có giá trị bằng với đối tượng được chỉ định. Chỉ loại bỏ một phần tử mỗi lần gọi phương thức.

Trả về true nếu phần tử đã được loại bỏ và false nếu không tìm thấy phần tử trong danh sách.

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

#### 7.2 Hàm removeAll()

Phương thức `.removeAll()` được sử dụng để xóa nhiều phần tử khỏi các đối tượng của lớp ArrayList.

    arrayList.removeAll(Collection<?> c)

Phương thức này loại bỏ tất cả giá trị có cùng giá trị cần loại bỏ, khác với remove, phương thức này loại bỏ tất cả các phần tử trong danh sách mà cũng có trong collection được chỉ định.

Trả về true nếu bất kỳ phần tử nào được loại bỏ và false nếu không có phần tử nào được loại bỏ từ danh sách.

```java
public static void main(String[] args) {
	List<Integer> arr = new ArrayList<>();
	int a[] = {1, 2, 2, 2, 3, 3, 5};

	// Thêm các phần tử của mảng a vào danh sách arr
	for(int x : a) {
		arr.add(x);
	}

	// Loại bỏ tất cả các phần tử có giá trị là 2 hoặc 3
	List<Integer> elementsToRemove = new ArrayList<>();
	elementsToRemove.add(2);
	elementsToRemove.add(3);
	arr.removeAll(elementsToRemove);

	// In các phần tử còn lại trong danh sách
	for(int x : arr) {
		System.out.print(x + " ");
	}
}
```

#### 7.3 Hàm removeIf()

Phương thức `.removeIf()` loại bỏ tất cả các phần tử của ArrayList thỏa mãn một yêu cầu nào đó. Bất kỳ lỗi hoặc ngoại lệ thời gian chạy nào được đưa ra trong quá trình lặp hoặc kiểm tra điều kiện đều được chuyển tiếp đến người dùng.

Nếu bất kỳ phần tử nào bị loại bỏ, phương thức này trả về true. Nếu không, nó trả về sai.

    arrayList.removeIf(Predicate<T> filter);

Trong đó

-   arrayList: Tên của danh sách.
-   Predicate<T>: Function Interface đại diện cho một điều kiện nào đó với kiểu Template T
-   filter: Điều kiện cần kiểm tra

```java
public static void main(String[] args) {
	ArrayList<Integer> nums = new ArrayList<Integer>();
	nums.add(10);
	nums.add(15);
	nums.add(20);
	nums.add(30);
	nums.removeIf(n -> (n % 2 == 0));
	System.out.println(nums);
}
```

#### 7.4 Hàm clear()

Phương thức clear() trong Java được sử dụng để xóa tất cả các phần tử từ một danh sách (ArrayList), làm cho danh sách trở thành rỗng.

Gọi phương thức clear() trên đối tượng danh sách (ArrayList) mà bạn muốn xóa các phần tử.

```java
public static void main(String[] args) {
	// Khởi tạo một ArrayList
	List<String> colors = new ArrayList<>();
	colors.add("Red");
	colors.add("Green");
	colors.add("Blue");
	// In danh sách ban đầu
	System.out.println("Danh sách ban đầu: " + colors);

	// Xóa tất cả các phần tử từ danh sách
	colors.clear();

	// In danh sách sau khi xóa
	System.out.println("Danh sách sau khi xóa: " + colors);
}
```

### 8. Sắp xếp danh sách

**Cách hoạt động của Comparator trong hàm sắp xếp**

Phương thức `compare` trong interface `Comparator` quyết định thứ tự của hai đối tượng bằng cách trả về một số nguyên. Kết quả trả về của phương thức compare sẽ quyết định xem liệu hai đối tượng có cần hoán đổi vị trí với nhau hay không trong quá trình sắp xếp.

Dưới đây là cách mà phương thức compare hoạt động:

-   Trả về một số âm: Vị trí của o1 và o2 không cần hoán đổi.
-   Trả về số 0: o1 và o2 đã đúng vị trí và vị trí của chúng có thể không thay đổi.
-   Trả về một số dương: Vị trí của o1 và o2 cần hoán đổi

#### 8.1 Hàm .sort()

Phương thức `.sort()` được sử dụng để sắp xếp **mảng gồm các kiểu và đối tượng nguyên thủy**. Việc sắp xếp được thực hiện theo thứ tự tăng dần theo mặc định, nhưng nó có thể được tùy chỉnh cho các đối tượng bằng cách triển khai interface Comparable hoặc dùng Comparator.

    Arrays.sort(array, comparator);


    ArraysName.sort(compartor)

Comparator là một đối tượng thực hiện việc so sánh, xác định logic so sánh cho các phần tử trong mảng.

Ví dụ sort cho một `Arraylist`

```java
public static void main(String[] args) {

	List<String> strings = new ArrayList<>();
	strings.add("banana");
	strings.add("apple");
	strings.add("orange");
	strings.add("grape");

	// Sắp xếp mảng các chuỗi theo thứ tự từ điển tăng dần
	strings.sort(new Comparator<String>() {
		@Override
		public int compare(String s1, String s2) {
			return s1.compareTo(s2);
		}
	});

	strings.forEach((str) -> System.out.print(str + " "));
}
```

Ví dụ sort cho một `mảng 1 chiều`

```java
public static void main(String[] args) {
	String[] strings = {"banana", "apple", "orange", "grape"};

	// Sắp xếp mảng các chuỗi theo thứ tự từ điển tăng dần
	Arrays.sort(strings, new Comparator<String>() {
		@Override
		public int compare(String s1, String s2) {
			return s1.compareTo(s2);
		}
	});

	for (String str : strings) {
		System.out.print(str + " ");
	}
}
```

#### 8.2 Hàm Collection.sort()

Trong Java, Collections là một lớp tiện ích cung cấp nhiều phương thức hữu ích để làm việc với các cấu trúc dữ liệu Collection. Trong đó, Collections.sort() là một phương thức được sử dụng để sắp xếp các phần tử trong một Collection.

    public static <T extends Comparable<? super T>> void sort(List<T> list)

**Tham số**

-   list: Danh sách cần sắp xếp.

**Mô tả**
Phương thức sort() của lớp Collections được sử dụng để sắp xếp các phần tử trong một danh sách (List) theo thứ tự tăng dần, dựa trên thứ tự tự nhiên của các phần tử hoặc theo thứ tự được xác định bởi phương thức compareTo() của interface Comparable.

```java
public static void main(String[] args) {
	List<Integer> arr = new ArrayList<>();
	int a[] = {3, 1, 0, 4, 2, 6, 5};
	for (int x : a) {
		arr.add(x);
	}

	// Sử dụng Collections.sort() với Comparator để sắp xếp theo thứ tự giảm dần
	Collections.sort(arr, new Comparator<Integer>() {
		@Override
		public int compare(Integer o1, Integer o2) {
			return o2 - o1;
		}
	});

	// In danh sách sau khi sắp xếp
	arr.forEach((n) -> System.out.print(n + " "));
}
```

### 9. So sánh giữa các ArrayList

Java cung cấp một phương thức để so sánh hai Danh sách mảng. `ArrayList.equals()` là phương thức được sử dụng để so sánh hai Danh sách mảng.

Nó so sánh các danh sách Mảng vì cả hai danh sách Mảng phải có `cùng kích thước` và `tất cả các cặp phần tử tương ứng trong hai danh sách Mảng đều bằng nhau`.

```java
public static void main(String[] args) {
    List<Integer> list1 = new ArrayList<>();
    List<Integer> list2 = new ArrayList<>();

    for (int i = 1; i <= 5; i++) {
        list1.add(i);
        list2.add(i);
    }

    boolean areEqual = list1.equals(list2);
    System.out.println("list1 equals list2: " + areEqual);
}
```

**Chú ý**

Có thể so sánh hai đối tượng thuộc các lớp tùy chỉnh với kiểu đối tượng trong Java. Tuy nhiên, chúng ta cần phải ghi đè các phương thức quan trọng như equals() và hashCode() của lớp đó.

**Phương thức equal()**

Phương thức `equals()` được sử dụng để xác định xem hai đối tượng **có bằng nhau hay không dựa trên nội dung của chúng**, không phải tham chiếu bộ nhớ. Theo **mặc định**, phương thức này trong Java **so sánh các tham chiếu đối tượng**, có nghĩa là hai đối tượng riêng biệt có cùng nội dung sẽ không được coi là bằng nhau.

Bất cứ khi nào chúng ta ghi đè phương thức equal(), chúng ta cũng phải ghi đè phương thức hashCode() để duy trì hợp đồng giữa hai phương thức này.

**Phương thức hashCode()**

Phương thức `hashCode()` trả về một giá trị số nguyên được sử dụng để xác định vị trí lưu trữ của đối tượng trong các cấu trúc dữ liệu dựa trên băm như HashMap, HashSet, v.v. Trong trường hợp của ArrayList, nó cũng được sử dụng khi bạn thêm một đối tượng vào danh sách.

Nếu bạn không ghi đè phương thức hashCode(), mặc định Java sẽ sử dụng phương thức hashCode() của lớp Object, và các đối tượng có thể có các giá trị hashCode() khác nhau cho cùng một nội dung, dẫn đến việc không nhất quán trong việc so sánh các đối tượng.

Hợp đồng tổng quát quy định rằng nếu hai đối tượng bằng nhau, mã băm của chúng cũng phải bằng nhau. Việc không ghi đè phương thức hashCode() có thể dẫn đến hành vi không nhất quán khi các đối tượng được sử dụng trong các bộ sưu tập dựa trên băm.

Ví dụ cho việc không ghi đè HashCode()

```java
static class Person {
	private String name;
	private int age;
	public Person(String name, int age) {
		this.name = name;
		this.age = age;
	}
	@Override
	public boolean equals(Object o) {
		if (this == o) return true;
		if (o == null || getClass() != o.getClass()) return false;
		Person person = (Person) o;
		return age == person.age && name.equals(person.name);
	}
}
public static void main(String[] args) {
	Person person_one = new Person("John", 30);
	Person person_two = new Person("John", 30);
	HashMap<Person, String> hashMap = new HashMap<>();
	hashMap.put(person_one, "Value for person_one");
	boolean containsPersonTwo = hashMap.containsKey(person_two);
	System.out.println("HashMap contains person_two: " + containsPersonTwo);
}
```

```bash
HashMap contains person_two: false
```

Về mặt lý thuyết, chúng ta mong muốn person_one và person_two là như nhau, tuy nhiên về việc vận hành ứng dụng nếu không có đầy đủ các hàm overide equal() và hashCode() sẽ dẫn đến việc so sánh bị sai vì hai đối tượng có 2 địa chỉ khác nhau.

Dưới đây là đoạn code hoàn chỉnh đảm bảo sự nhất quán và các thuộc tính hashCode and equal trong lớp Person

```java
static class Person {
	private String name;
	private int age;
	public Person(String name, int age) {
		this.name = name;
		this.age = age;
	}
	@Override
	public boolean equals(Object o) {
		if (this == o) return true;
		if (o == null || getClass() != o.getClass()) return false;
		Person person = (Person) o;
		return age == person.age && Objects.equals(name, person.name);
	}
	@Override
	public int hashCode() {
		return Objects.hash(name, age);
	}
	@Override
	public String toString() {
		return name + " (" + age + ")";
	}
}
public static void main(String[] args) {
	Person person_one = new Person("John", 30);
	Person person_two = new Person("John", 30);
	HashMap<Person, String> hashMap = new HashMap<>();
	hashMap.put(person_one, "Value for person_one");
	boolean containsPersonTwo = hashMap.containsKey(person_two);
	System.out.println("HashMap contains person_two: " + containsPersonTwo);
}
```

```bash
HashMap contains person_two: true
```

**Time Complexity:** O(N), trong đó N là kích thước của ArrayList

### 10. Danh sách con và Dãy con

**Phương thức .subList()**

Trong Java, phương thức .subList() là một tính năng mạnh mẽ của List để lấy một phần danh sách dựa trên các chỉ mục được chỉ định. Phương pháp này cung cấp một cách thuận tiện để tạo danh sách con chứa các phần tử từ danh sách gốc.

    List<E> subList (int fromIndex, int toIndex)

Phương thức subList(int fromIndex, int toIndex) trả về một danh sách con chứa các phần tử từ chỉ số fromIndex (bao gồm) đến toIndex (không bao gồm). Điều này có nghĩa là nếu bạn gọi subList(1, 4), danh sách con sẽ chứa các phần tử từ chỉ số 1 đến chỉ số 3 của danh sách gốc.

```java
public static void main(String[] args) {
	List<String> fruits = new ArrayList<>();
	fruits.add("Apple");fruits.add("Banana");
	fruits.add("Cherry");fruits.add("Date");
	fruits.add("Elderberry");

	List<String> subList = fruits.subList(1, 4);

	System.out.println("Danh sách con: " + subList);

	subList.set(1, "Blueberry");

	System.out.println("Danh sách ban đầu sau khi thay đổi: " + fruits);
}
```

```bash
Danh sách con: [Banana, Cherry, Date]
Danh sách ban đầu sau khi thay đổi: [Apple, Banana, Blueberry, Date, Elderberry]
```

**Chú ý**

-   Mọi thay đổi trên danh sách con sẽ phản ánh trên danh sách gốc và ngược lại.

-   Bất Biến: Không thể thay đổi kích thước của danh sách con (không thể thêm hoặc xóa phần tử).
