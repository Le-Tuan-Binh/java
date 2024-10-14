## Giới Thiệu về Stream trong Java

Java 8 đã giới thiệu khái niệm Stream API, giúp đơn giản hóa việc xử lý dữ liệu theo cách thức functional programming. Stream cho phép thao tác với các tập dữ liệu một cách dễ dàng và hiệu quả, giúp mã trở nên ngắn gọn hơn so với cách tiếp cận truyền thống.

### 1. Stream là gì?

**Stream** trong Java là một chuỗi các phần tử được hỗ trợ bởi các thao tác như **filter**, **map**, **reduce**, **collect**, và nhiều thao tác khác. 

Stream không lưu trữ dữ liệu, mà chỉ là các tập hợp các thao tác trên dữ liệu. Dữ liệu chỉ được xử lý khi có các phép toán kết thúc.

**Các đặc điểm chính của Stream**

- **Lazy Evaluation**: Stream không thực sự thực hiện các thao tác cho đến khi cần kết quả đầu ra.

- **Non-Interference**: Stream không thay đổi nguồn dữ liệu gốc của nó.

- **Stateless**: Mỗi thao tác trên Stream đều không phụ thuộc vào các thao tác trước đó.

### 2. Các cách tạo Stream trong Java

### 2.1 Từ `Collection`

```java
List<String> names = Arrays.asList("John", "Jane", "Jack");
Stream<String> stream = names.stream();
```

### 2.2 Từ `Arrays`

```java
int[] numbers = {1, 2, 3, 4, 5};
IntStream intStream = Arrays.stream(numbers);
```

### 2.3 Từ `Stream.of()`

```java
Stream<String> stream = Stream.of("Java", "C++", "Python");
```

### 3. Các thao tác trên Stream

Stream API hỗ trợ nhiều phương thức giúp bạn thao tác với dữ liệu một cách hiệu quả. Các thao tác này được chia thành 2 nhóm chính: Intermediate Operations - Các thao tác trung gian và Terminal Operations - Các thao tác kết thúc.

### 3.1 Intermediate Operations

### 3.1.1 filter(Predicate)

Dùng để lọc các phần tử thõa mãn một điều kiện nào đó

```bash
Stream<T> filter(Predicate<? super T> predicate)
```

```java
List<String> names = Arrays.asList("John", "Jane", "Jack");
names.stream()
		.filter(name -> name.startsWith("J"))
		.forEach(System.out::println);
```

Lọc các điều kiện phức tạp trong Java Stream có thể được thực hiện bằng cách sử dụng nhiều biểu thức điều kiện trong phương thức filter(). Bạn có thể kết hợp các điều kiện bằng cách sử dụng các toán tử logic như:

- **&&** Tất cả các điều kiện phải đúng.
- **||** Một trong các điều kiện đúng là đủ.
- **!** Đảo ngược giá trị của điều kiện.

Hoặc bạn có thể viết 1 phương thức trả về **boolean** hoặc **Predicate<T>** để truyền vào `filter()`

```java
public class Main {
	public static boolean isEligible(Person person) {
		return person.name.startsWith("J") && person.age > 20;
	}

	public static void main(String[] args) {
		List<Person> people = Arrays.asList(
			new Person("John", 25),
			new Person("Jane", 15),
			new Person("Tom", 35),
			new Person("Jerry", 30),
			new Person("Lucy", 22)
		);
		people.stream()
			.filter(Main::isEligible) 
			.forEach(System.out::println);
	}
}
```

Hoặc trả về `Predicate<T>` như bên dưới

```java
class Person {
	String name;
	int age;
	public Person(String name, int age) {
		this.name = name;
		this.age = age;
	}
	@Override
	public String toString() {
		return name + " (" + age + ")";
	}
}
```

```java
import java.util.function.Predicate;
public class Main {
	public static Predicate<Person> filterByNameAndAge() {
		return person -> person.name.startsWith("J") && person.age > 20;
	}
	public static void main(String[] args) {
		List<Person> people = Arrays.asList(
			new Person("John", 25),
			new Person("Jane", 15),
			new Person("Tom", 35),
			new Person("Jerry", 30),
			new Person("Lucy", 22)
		);
		people.stream()
			.filter(filterByNameAndAge())
			.forEach(System.out::println);
	}
}
```

### 3.1.2 map(Function)

Dùng để chuyển đổi mỗi phần tử của Stream sang dạng khác.

```bash
<R> Stream<R> map(Function<? super T, ? extends R> mapper)
```

**Trong đó:**

- **T** là kiểu dữ liệu của các phần tử hiện tại trong Stream.
- **R** là kiểu dữ liệu của kết quả sau khi áp dụng hàm Function.
- **Function<? super T, ? extends R>** là một interface chức năng với phương thức duy nhất apply() dùng để chuyển đổi phần tử từ kiểu T sang kiểu R.

```java
List<String> names = Arrays.asList("John", "Jane", "Jack");
names.stream()
	.map(String::toUpperCase)
	.forEach(System.out::println);
```

Bạn cũng có thể truyền 1 hàm vào trong `map()` để thực hiện chuyển đổi thông qua việc sử dụng method references hoặc lambda expressions. 

```java
public class Main {
	public static String convertToUpperCase(String s) {
		return s.toUpperCase();
	}
	public static void main(String[] args) {
		List<String> names = Arrays.asList("John", "Jane", "Jack");
		names.stream()
			.map(Main::convertToUpperCase) 
			.forEach(System.out::println);
	}
}
```

Hoặc sử dụng **lambda expression** như đoạn mã bên dưới

```java
List<String> names = Arrays.asList("John", "Jane", "Jack");
names.stream()
	.map(name -> name.toUpperCase()) 
	.forEach(System.out::println);
```

### 3.1.3 sorted()

Sắp xếp các phần tử theo thứ tự tự nhiên hoặc theo comparator.

Phương thức sorted() trong Java Stream API được sử dụng để sắp xếp các phần tử trong Stream. 

Nó có hai phiên bản:

**sorted()**: Sắp xếp các phần tử theo thứ tự tự nhiên (Natural Order). Điều này chỉ hoạt động với các phần tử có kiểu dữ liệu triển khai giao diện Comparable (ví dụ: String, Integer, Double...).

**sorted(Comparator<T> comparator)**: Sắp xếp các phần tử theo thứ tự do bạn định nghĩa bằng cách truyền vào một đối tượng Comparator.

Đây là ví dụ về **sort()** không có comparator

```java
List<String> names = Arrays.asList("John", "Jane", "Jack");
names.stream()
	.sorted()
	.forEach(System.out::println);
```

Nếu bạn muốn sắp xếp theo một tiêu chí khác, bạn có thể sử dụng phiên bản **sorted(Comparator<T> comparator)**. 

Bạn có thể truyền vào một đối tượng Comparator để định nghĩa thứ tự sắp xếp theo mong muốn của mình.

**Sắp xếp các số lẻ đứng trước và số chẵn đứng sau**

```java
import java.util.Arrays;
import java.util.List;
import java.util.Comparator;

public class Main {
	public static void main(String[] args) {
		List<Integer> numbers = Arrays.asList(3, 1, 4, 5, 2, 7, 8, 6);
		numbers.stream()
			.sorted(new Comparator<Integer>() {
				@Override
				public int compare(Integer n1, Integer n2) {
					int mod1 = n1 % 2;
					int mod2 = n2 % 2;
					if (mod1 != mod2) {
						return mod1 - mod2;
					} else {
						return n1 - n2; 
					}
				}
			})
			.forEach(System.out::println);
	}
}
```

Bên cạnh đó bạn có thể sử dụng lamda expression để làm gọn mã nguồn như bên dưới

```java
List<Integer> numbers = Arrays.asList(3, 1, 4, 5, 2, 7, 8, 6);
numbers.stream()
	.sorted((n1, n2) -> {
		int mod1 = n1 % 2;
		int mod2 = n2 % 2;
		if (mod1 != mod2) {
			return mod1 - mod2; 
		} else {
			return n1 - n2;
		}
	})
	.forEach(System.out::println);
```


### 3.2 Terminal Operations

Các thao tác này kết thúc Stream và trả về một giá trị cụ thể hoặc thực hiện một hành động.

### 3.2.1 forEach(Consumer)

Dùng để lặp qua các phần tử và thực hiện một hành động nào đó.

```bash
void forEach(Consumer<? super T> action)
```

**Consumer<T>** là một functional interface trong Java, đại diện cho một hàm nhận vào một đối tượng và thực hiện một hành động nào đó với đối tượng đó mà không trả về giá trị. `forEach()` nhận một Consumer làm tham số.

```java
List<String> names = Arrays.asList("John", "Jane", "Jack");
names.stream()
	.forEach(System.out::println);
```

Bạn cũng có thể viết một `Consumer<T>` như bên dưới

```java
import java.util.List;
import java.util.function.Consumer;

public class Main {

	public static void main(String[] args) {
		List<String> names = List.of("John", "Jane", "Jack");
		names.stream().forEach(uppercaseCheckAndPrint());
	}
	public static Consumer<String> uppercaseCheckAndPrint() {
		return name -> {
			if (name.equals(name.toUpperCase())) {
					System.out.println(name + " is already in uppercase");
			} else {
					System.out.println(name.toUpperCase());
			}
		};
	}
}
```

Hoặc có thể viết dạng lamda expression như bên dưới

```java
import java.util.List;

public class Main {

	public static void main(String[] args) {
		List<String> names = List.of("John", "Jane", "Jack");
		names.stream().forEach(name -> {
			if (name.equals(name.toUpperCase())) {
					System.out.println(name + " is already in uppercase");
			} else {
					System.out.println(name.toUpperCase());
		}
	});
}
}
```

### 3.2.2 collect(Collector)


Phương thức collect() trong Stream API của Java là một trong những phương thức quan trọng nhất khi bạn muốn thu thập kết quả từ một Stream thành một kiểu dữ liệu khác, chẳng hạn như List, Set, Map, hoặc thậm chí là một chuỗi. Phương thức này sử dụng một Collector để thực hiện việc thu thập.

```bash
<R, A> R collect(Collector<? super T, A, R> collector);
```

**Trong đó**

**T**: kiểu của các phần tử trong Stream.

**A**: kiểu của bộ sưu tập trung gian (có thể là một List, Set, hoặc Map).

**R**: kiểu của kết quả thu được sau khi collect() được thực hiện.

**Các Collector thông dụng nhất trong Java bao gồm:**

**Collectors.toList()**: thu thập kết quả thành một List.

**Collectors.toSet()**: thu thập kết quả thành một Set.

**Collectors.toMap()**: thu thập kết quả thành một Map.

**Collectors.joining()**: nối các phần tử thành một chuỗi.

**Collectors.groupingBy()**: nhóm các phần tử theo một tiêu chí.

**Collectors.counting()**: Đếm số lượng phần tử trong Stream.

```java
List<String> names = Arrays.asList("John", "Jane", "Jack");
List<String> filteredNames = names.stream()
											.filter(name -> name.startsWith("J"))
											.collect(Collectors.toList());
```

**Collectors.joining() - Nối các phần tử thành một chuỗi.**

```java
List<String> names = Arrays.asList("John", "Jane", "Jack");
String result = names.stream()
						.collect(Collectors.joining(", "));
System.out.println(result); 
```

**Collectors.counting() - Đếm số lượng phần tử trong Stream.**

```java
List<String> names = Arrays.asList("John", "Jane", "Jack");
long count = names.stream()
                  .collect(Collectors.counting());
System.out.println(count); 
```

**Collectors.groupingBy() - Nhóm các phần tử theo một tiêu chí.**

```java
List<String> names = Arrays.asList("John", "Jane", "Jack", "Jill");
Map<Integer, List<String>> groupedByLength = names.stream()
						.collect(Collectors.groupingBy(String::length));
System.out.println(groupedByLength);
```

Bạn cũng có thể kết hợp các `Collector` để thực hiện các phép toán phức tạp hơn. 

Ví dụ, sử dụng `groupingBy()` cùng với `counting()` để đếm số lượng phần tử trong mỗi nhóm:

```java
List<String> names = Arrays.asList("John", "Jane", "Jack", "Jill", "Jake", "James");
Map<Integer, Long> lengthCount = names.stream()
					.collect(Collectors.groupingBy(String::length, Collectors.counting()));
System.out.println(lengthCount);
```
Ở đây, chúng ta nhóm các tên theo độ dài và đếm số lượng tên trong mỗi nhóm.

### 3.2.3 reduce(BinaryOperator)

Dùng để kết hợp các phần tử thành một giá trị duy nhất.

```bash
Optional<T> reduce(BinaryOperator<T> accumulator);
```

**BinaryOperator<T>**: Là một hàm nhận vào hai đối tượng cùng kiểu T và trả về một đối tượng của kiểu T. Hàm này được áp dụng lặp đi lặp lại trên các phần tử của Stream để kết hợp chúng thành một giá trị duy nhất.

**Phương thức này có thể có hai dạng:**

Có giá trị khởi tạo: **reduce(T identity, BinaryOperator<T> accumulator)** – Trong trường hợp này, bạn chỉ định một giá trị khởi tạo cho phép toán.

Không có giá trị khởi tạo: **reduce(BinaryOperator<T> accumulator)** – Ở đây, không có giá trị khởi tạo, và phương thức này trả về một Optional<T> vì Stream có thể là rỗng.

**Có giá trị khởi tạo**

> T reduce(T identity, BinaryOperator<T> accumulator);

**identity**: Giá trị khởi tạo, được sử dụng làm giá trị ban đầu cho phép toán. Ví dụ: với phép toán cộng, identity sẽ là 0.

**accumulator**: Là hàm nhị phân thực hiện phép toán với từng phần tử trong Stream.

Ví dụ bên dưới là tính tổng các số trong danh sách

```java
List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);
int sum = numbers.stream()
					.reduce(0, Integer::sum);
System.out.println(sum); 
```

Ví dụ tính tích các số trong danh sách

```java
import java.util.List;
import java.util.Arrays;

public class Main {
	public static void main(String[] args) {
		List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);
		int product = numbers.stream()
									.reduce(1, (a, b) -> a * b);

		System.out.println("Product: " + product);
	}
}
```

Ví dụ tìm số lớn nhất trong danh sách

```java
import java.util.List;
import java.util.Arrays;

public class Main {
	public static void main(String[] args) {
		List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);

		int max = numbers.stream()
								.reduce(Integer::max)
								
		System.out.println("Max: " + max);
	}
}
```
