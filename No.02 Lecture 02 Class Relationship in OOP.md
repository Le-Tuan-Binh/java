## Getting Started

Trong lập trình hướng đối tượng (OOP), các lớp (class) không tồn tại độc lập mà thường có mối quan hệ với nhau. Hiểu rõ các loại quan hệ giữa các lớp là một phần quan trọng trong việc thiết kế phần mềm. Trong bài giảng này, chúng ta sẽ tìm hiểu về các loại quan hệ chính giữa các lớp bao gồm: kế thừa (inheritance), kết hợp (association), tập hợp (aggregation), và hợp thành (composition).

## Getting Involved

### 0. Mối quan hệ isA and hasA trong lập trình

Trong lập trình hướng đối tượng (OOP), mối quan hệ giữa các lớp rất quan trọng để xác định cách các đối tượng tương tác với nhau. Trong Java, có hai mối quan hệ cơ bản là "isA" và "hasA", mỗi mối quan hệ có mục đích và cách sử dụng riêng biệt.

#### Mối quan hệ "isA"

Mối quan hệ "isA" xác định một lớp con là một loại của lớp cha. Nó thể hiện mối quan hệ phân cấp giữa các lớp.

```java
class Animal {
    void eat() {
        System.out.println("Animal is eating");
    }
}
class Dog extends Animal {
    void bark() {
        System.out.println("Dog is barking");
    }
}
public class Main {
    public static void main(String[] args) {
        Animal animal = new Dog(); 
        animal.eat();
    }
}
```

#### Mối quan hệ "hasA"

Mối quan hệ "hasA" xác định một lớp có một đối tượng của một lớp khác như một phần của nó. Đây là một mối quan hệ sử dụng lại đối tượng khác trong một lớp.

```java
class Car {
    private Engine engine; 
    Car(Engine engine) {
        this.engine = engine;
    }
    void start() {
        engine.start();
    }
}
class Engine {
    void start() {
        System.out.println("Engine is starting");
    }
}
public class Main {
    public static void main(String[] args) {
        Engine engine = new Engine();
        Car car = new Car(engine); 
        car.start();
    }
}
```

Trong ví dụ này, lớp Car có một đối tượng Engine như là một phần của nó. Bằng cách này, mối quan hệ "hasA" giúp Car sử dụng lại chức năng của Engine mà không cần kế thừa từ Engine.

#### Tổng kết lý thuyết

Mối quan hệ "isA" thể hiện mối quan hệ phân cấp giữa các lớp, trong khi "hasA" thể hiện mối quan hệ sở hữu hoặc sử dụng lại một đối tượng khác trong một lớp.

- "isA" thường được sử dụng trong kế thừa

- "hasA" thường được sử dụng trong kết hợp và tập hợp.

Hiểu và áp dụng đúng mối quan hệ sẽ giúp cho việc thiết kế và triển khai các lớp trong Java trở nên hiệu quả và dễ bảo trì hơn.

### 1. Kế Thừa (Inheritance)

Kế thừa là một cơ chế trong đó một lớp mới (lớp con) kế thừa các thuộc tính và hành vi (phương thức) từ một lớp cha hiện có. Điều này cho phép tái sử dụng mã và tạo mối quan hệ phân cấp giữa các lớp.

```java
class Animal {
    void eat() {
        System.out.println("This animal eats food.");
    }
}
class Dog extends Animal {
    void bark() {
        System.out.println("The dog barks.");
    }
}
public class Main {
    public static void main(String[] args) {
        Dog dog = new Dog();
        dog.eat();  
        dog.bark(); 
    }
}
```

### 2. Kết Hợp (Association)

Đây là một mối quan hệ đơn giản giữa các đối tượng, nơi một đối tượng "biết" về đối tượng khác. Quan hệ này có thể là một chiều hoặc hai chiều.

Ví dụ: Một lớp Teacher có thể liên kết với lớp Student. Một giáo viên có thể dạy nhiều học sinh, và mỗi học sinh có thể có nhiều giáo viên.

```java
class Teacher {
    private String name;
    public String getName() {
        return name;
    }
    public void setName(String name) {
        this.name = name;
    }
    void teach(Student student) {
        System.out.println(this.name + " is teaching " + student.getName());
    }
}
class Student {
    private String name;
    public String getName() {
        return name;
    }
    public void setName(String name) {
        this.name = name;
    }
}
public class Main {
    public static void main(String[] args) {
        Teacher teacher = new Teacher();
        teacher.setName("Mr. Smith");

        Student student = new Student();
        student.setName("John Doe");

        teacher.teach(student);
    }
}
```

### 3. Tập Hợp (Aggregation)

Tập hợp là một dạng đặc biệt của `Association`, trong đó một lớp chủ (owner) chứa các đối tượng con (part). Các đối tượng con có thể tồn tại độc lập với lớp chủ.

Ví dụ: Lớp Team bao gồm nhiều lớp Player. Mỗi cầu thủ có thể tồn tại mà không cần phải thuộc về một đội cụ thể.

```java
class Player {
    String name;
    Player(String name) {
        this.name = name;
    }
}
class Team {
    String teamName;
    List<Player> players;
    Team(String teamName) {
        this.teamName = teamName;
        this.players = new ArrayList<>();
    }
    void addPlayer(Player player) {
        players.add(player);
    }
}
public class Main {
    public static void main(String[] args) {
        Team team = new Team("Football CLUB");
        Player player1 = new Player("Le Tuan Binh");
        Player player2 = new Player("Binh Le Tuan");

        team.addPlayer(player1);
        team.addPlayer(player2);

        System.out.println(team.teamName + " has players:");
        for (Player player : team.players) {
            System.out.println(player.name);
        }
    }
}
```

### 4. Hợp Thành (Composition)

Hợp thành là một loại quan hệ mạnh hơn `Aggregation`, nơi các đối tượng con không thể tồn tại độc lập với lớp chủ. Điều này có nghĩa là đối tượng chủ quản lý vòng đời của các đối tượng con.

Ví dụ: Lớp House bao gồm nhiều lớp Room. Một căn phòng không thể tồn tại nếu không có căn nhà chứa nó.

```java
class House {
    private Room kitchen;
    House() {
        this.kitchen = new Room();
    }
}
class Room {
    
}
```

### 5. Phụ thuộc (Dependency)

`Dependency` là một loại quan hệ mà một lớp cần một lớp khác để hoạt động đúng. Điều này thường xảy ra khi một lớp sử dụng một đối tượng của một lớp khác như là một tham số hoặc biến cục bộ.

```java
class Engine {
    private String type;

    public Engine(String type) {
        this.type = type;
    }

    public String getType() {
        return type;
    }
}

class Car {
    private String model;
    private Engine engine;

    public Car(String model, Engine engine) {
        this.model = model;
        this.engine = engine;
    }

    public void display() {
        System.out.println(model + " với loại động cơ " + engine.getType());
    }
}
```

### 6. Kí hiệu trong quá trình thiết kế

![alt text](/images/image_01.png)