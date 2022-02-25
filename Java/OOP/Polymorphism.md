# Đa hình (Polymorphism)

-	Tính đa hình là khả năng một đối tượng có thể thực hiện một tác vụ theo nhiều cách khác nhau

-	Đối với tính chất này, nó được thể hiện rõ nhất qua việc gọi phương thức của đối tượng. Các phương thức hoàn toàn có thể giống nhau, nhưng việc xử lý luồng có thể khác nhau. Nói cách khác: Tính đa hình cung cấp khả năng cho phép người lập trình gọi trước một phương thức của đối tượng, tuy chưa xác định đối tượng có phương thức muốn gọi hay không. Đến khi thực hiện (run-time), chương trình mới xác định được đối tượng và gọi phương thức tương ứng của đối tượng đó. Kết nối trễ giúp chương trình được uyển chuyển hơn, chỉ yêu cầu đối tượng cung cấp đúng phương thức cần thiết là đủ.
-	Trong Java, chúng ta sử dụng nạp chồng phương thức (method overloading) và ghi đè phương thức (method overriding) để có tính đa hình.
    + **Nạp chồng (Overloading)**: Đây là khả năng cho phép một lớp có nhiều thuộc tính, phương thức cùng tên nhưng với các tham số khác nhau về loại cũng như về số lượng. Khi được gọi, dựa vào tham số truyền vào, phương thức tương ứng sẽ được thực hiện.
    + **Ghi đè (Overriding)**: là hai phương thức cùng tên, cùng tham số, cùng kiểu trả về nhưng thằng con viết lại và dùng theo cách của nó, và xuất hiện ở lớp cha và tiếp tục xuất hiện ở lớp con. Khi dùng override, lúc thực thi, nếu lớp Con không có phương thức riêng, phương thức của lớp Cha sẽ được gọi, ngược lại nếu có, phương thức của lớp Con được gọi.

### 1.Đa hình trong lúc runtime trong java

-	Đa hình lúc runtime là quá trình gọi phương thức đã được ghi đè trong thời gian thực thi chương trình. Trong quá trình này, một phương thức được ghi đè được gọi thông qua biến tham chiếu của một lớp cha.
-	Trước khi tìm hiểu về đa hình tại runtime, chúng ta cùng tìm hiểu về Upcasting.

#### 1.1.Upcasting là gì

Khi biến tham chiếu của lớp cha tham chiếu tới đối tượng của lớp con, thì đó là Upcasting. Ví dụ:

```
class A {
} 
 
class B extends A {
} 
```

```
A a = new B(); // upcasting 
```

#### 1.2.Ví dụ về đa hình tại runtime trong Java

Ví dụ 1: chúng ta tạo hai lớp Bike và Splendar. Lớp Splendar kế thừa lớp Bike và ghi đè phương thức run() của nó. Chúng ta gọi phương thức run bởi biến tham chiếu của lớp cha. Khi nó tham chiếu tới đối tượng của lớp con và phương thức lớp con ghi đè phương thức của lớp cha, phương thức lớp con được triệu hồi tại runtime.

Khi việc gọi phương thức được quyết định bởi JVM chứ không phải Compiler, vì thế đó là đa hình tại runtime.

```
public class Bike {
    public void run() {
        System.out.println("running");
    }
}
 
public class Splender extends Bike {
    public void run() {
        System.out.println("running safely with 60km");
    }
 
    public static void main(String args[]) {
        Bike b = new Splender(); // upcasting 
        b.run();
    }
}
```
<p align="center">
  <span>Kết quả</span>
</p>

```
running safely with 60km
```

Ví dụ 2: Giả sử Bank là một lớp cung cấp phương thức để lấy lãi suất. Nhưng lãi suất lại khác nhau giữa từng ngân hàng. Ví dụ, các ngân hàng VCB, AGR và CTG có thể cung cấp các lãi suất lần lượt là 8%, 7% và 9%. (Ví dụ này cũng có trong chương ghi đè phương thức nhưng không có Upcasting).

```
class Bank {
    int getRateOfInterest() {
        return 0;
    }
}
 
class VCB extends Bank {
    int getRateOfInterest() {
        return 8;
    }
}
 
class AGR extends Bank {
    int getRateOfInterest() {
        return 7;
    }
}
 
class CTG extends Bank {
    int getRateOfInterest() {
        return 9;
    }
}
 
class Test3 {
    public static void main(String args[]) {
        Bank b1 = new VCB(); // upcasting 
        Bank b2 = new AGR(); // upcasting 
        Bank b3 = new CTG(); // upcasting 
        System.out.println("VCB lai suat la: " + b1.getRateOfInterest());
        System.out.println("AGR lai suat la: " + b2.getRateOfInterest());
        System.out.println("CTG lai suat la: " + b3.getRateOfInterest());
    }
}
```
<p align="center">
  <span>Kết quả</span>
</p>

```
VCB lai suat la: 8
VCB lai suat la: 7
VCB lai suat la: 9
```

Ví dụ 3: Shape

```
class Shape {
    void draw() {
        System.out.println("drawing...");
    }
}
 
class Rectangle extends Shape {
    void draw() {
        System.out.println("drawing rectangle...");
    }
}
 
class Circle extends Shape {
    void draw() {
        System.out.println("drawing circle...");
    }
}
 
class Triangle extends Shape {
    void draw() {
        System.out.println("drawing triangle...");
    }
}
 
class TestPolymorphism2 {
    public static void main(String args[]) {
        Shape s;
        s = new Rectangle();
        s.draw();
        s = new Circle();
        s.draw();
        s = new Triangle();
        s.draw();
    }
}
```

<p align="center">
  <span>Kết quả</span>
</p>

```
drawing rectangle...
drawing circle...
drawing triangle...
```

#### 1.3.	Đa hình tại runtime trong Java với thành viên dữ liệu

Phương thức bị ghi đè không là thành viên dữ liệu, vì thế đa hình tại runtime không thể có được bởi thành viên dữ liệu. Trong ví dụ sau đây, cả hai lớp có một thành viên dữ liệu là speedlimit, chúng ta truy cập thành viên dữ liệu bởi biến tham chiếu của lớp cha mà tham chiếu tới đối tượng lớp con. Khi chúng ta truy cập thành viên dữ liệu mà không bị ghi đè, thì nó sẽ luôn luôn truy cập thành viên dữ liệu của lớp cha.

`Qui tắc: Đa hình tại runtime không thể có được bởi thành viên dữ liệu`

```
class Bike {
    int speedlimit = 90;
}
 
class Honda3 extends Bike {
    int speedlimit = 150;
 
    public static void main(String args[]){  
      Bike obj=new Honda3();  
      System.out.println(obj.speedlimit); // 90  
    }
}
```

<p align="center">
  <span>Kết quả</span>
</p>

```
```

#### 1.4. Đa hình lúc runtime trong Java với kế thừa nhiều tầng

Ví dụ 1:

```
class Animal {
    void eat() {
        System.out.println("eating");
    }
}
 
class Dog extends Animal {
    void eat() {
        System.out.println("eating fruits");
    }
}
 
class BabyDog extends Dog {
    void eat() {
        System.out.println("drinking milk");
    }
 
    public static void main(String args[]) {
        Animal a1, a2, a3;
        a1 = new Animal();
        a2 = new Dog();
        a3 = new BabyDog();
        a1.eat();
        a2.eat();
        a3.eat();
    }
}
```
<p align="center">
  <span>Kết quả</span>
</p>

```
eating
eating fruits
drinking Milk
```


Ví dụ 2:

```
class Animal {
    void eat() {
        System.out.println("animal is eating...");
    }
}
 
class Dog extends Animal {
    void eat() {
        System.out.println("dog is eating...");
    }
}
 
class BabyDog1 extends Dog {
    public static void main(String args[]) {
        Animal a = new BabyDog1();
        a.eat();
    }
}
```

<p align="center">
  <span>Kết quả</span>
</p>

```
Dog is eating
```

Vì **BabyDog1** không ghi đè phương thức eat(), nên phương thức eat() của lớp Dog được gọi.

## 2.Nạp chồng phương thức (method overloading)

Nếu một lớp có nhiều phương thức cùng tên nhưng khác nhau về kiểu dữ liệu hoặc số lượng các tham số, thì đó là nạp chồng phương thức (Method Overloading).

Sử dụng nạp chồng phương thức giúp tăng khả năng đọc hiểu chương trình.

Nạp chồng phương thức được sử dụng để thu được tính đa hình lúc biên dịch (compile).

- Có 2 cách nạp chồng phương thức trong java

    + Thay đổi số lượng các tham số
    + Thay đổi kiểu dữ liệu của các tham số

#### 2.1.Nạp chồng phương thức: thay đổi số lượng các tham số

Ví dụ: tạo 2 phương thức có cùng kiểu dữ liệu: phương thức add() đầu tiên thực hiện việc tính tổng của 2 số, phương thức thứ hai thực hiện việc tính tổng của 3 số.

```
class Adder {
    static int add(int a, int b) {
        return a + b;
    }
 
    static int add(int a, int b, int c) {
        return a + b + c;
    }
}
 
class TestOverloading1 {
    public static void main(String[] args) {
        System.out.println(Adder.add(5, 5));
        System.out.println(Adder.add(5, 5, 5));
    }
}
```

```
10
15
```

#### 2.2.Nạp chồng phương thức: thay đổi kiểu dữ liệu của các tham số

Ví dụ: tạo 2 phương thức có kiểu dữ liệu khác nhau: phương thức add() đầu tiên nhận 2 đối số có kiểu giá trị là integer, phương thức thứ hai nhận 2 đối số có kiểu giá trị là double.

```
class Adder {
    static int add(int a, int b) {
        return a + b;
    }

    static double add(double a, double b) {
        return a + b;
    }
}

class TestOverloading2 {
public static void main(String[] args) {
    System.out.println(Adder.add(5, 5));
    System.out.println(Adder.add(4.3, 5.6));
    }
}
```

```
10
9.9
```

#### 2.3.	Một số câu hỏi về nạp chồng phương thức trong Java

`Câu 1: Tại sao không thể nạp chồng phương thức bằng cách chỉ thay đổi kiểu trả về của phương thức?`

* Trong java, không thể nạp chồng phương thức bằng cách chỉ thay đổi kiểu trả về của phương thức bởi vì không biết phương thức nào sẽ được gọi.

```
class Adder {
    static int add(int a, int b) {
        return a + b;
    }
 
    static double add(int a, int b) {
        return a + b;
    }
}
 
class TestOverloading3 {
    public static void main(String[] args) {
        System.out.println(Adder.add(11, 11)); // Không biết gọi phương thức nào
    }
}
```

`Câu 2: Có thể nạp chồng phương thức main() không?`

- Có, bạn có thể nạp chồng n phương thức main. Nhưng JVM chỉ gọi phương thức main() có tham số truyền vào là một mảng String.

```
public class TestOverloading4 {
    public static void main(String[] args) {
        System.out.println("main with String[]");
    }
 
    public static void main(String args) {
        System.out.println("main with String");
    }
 
    public static void main() {
        System.out.println("main without args");
    }
}
```

```
main with String[]
```

## 3. Ghi đè phương thức (method overriding)

**Ghi đè phương thức** trong java xảy ra nếu lớp con có phương thức giống lớp cha.

Nói cách khác, nếu lớp con cung cấp sự cài đặt cụ thể cho phương thức đã được cung cấp bởi một lớp cha của nó được gọi là ghi đè phương thức (method overriding) trong java.

Ghi đè phương thức được sử dụng để thu được tính đa hình tại runtime.

- Nguyên tắc ghi đè phương thức:
    + Phương thức phải có tên giống với lớp cha.
    + Phương thức phải có tham số giống với lớp cha.
    + Lớp con và lớp cha có mối quan hệ kế thừa.

#### 4.1.Ví dụ về ghi đè phương thức (method overriding)

`Ví dụ 1`: chúng ta định nghĩa phương thức run() trong lớp con giống như đã được định nghĩa trong lớp cha, nhưng được cài đặt rõ ràng trong lớp con. Tên và tham số của phương thức là giống nhau, 2 lớp cha và con có quan hệ kế thừa.

```
class Vehicle {
    void run() {
        System.out.println("Vehicle is running");
    }
}
 
class Bike extends Vehicle {
    void run() {
        System.out.println("Bike is running safely");
    }
 
    public static void main(String args[]) {
        Bike obj = new Bike();
        obj.run();
    }
 
}
```

```
Bike is running safely
```

`Ví dụ 2`: Giả sử Bank là một đối tượng cung cấp lãi suất. Nhưng lãi suất lại khác nhau giữa từng ngân hàng. Ví dụ, các ngân hàng VCB, AGR và CTG có thể cung cấp các lãi suất lần lượt là 8%, 7% và 9%.

```
class Bank {
    int getRateOfInterest() {
        return 0;
    }
}
 
class VCB extends Bank {
    int getRateOfInterest() {
        return 8;
    }
}
 
class AGR extends Bank {
    int getRateOfInterest() {
        return 7;
    }
}
 
class CTG extends Bank {
    int getRateOfInterest() {
        return 9;
    }
}
 
class BankApp {
    public static void main(String args[]) {
        VCB s = new VCB();
        AGR i = new AGR();
        CTG a = new CTG();
        System.out.println("VCB Rate of Interest: " + s.getRateOfInterest());
        System.out.println("AGR Rate of Interest: " + i.getRateOfInterest());
        System.out.println("CTG Rate of Interest: " + a.getRateOfInterest());
    }
}
```

```
VCB Rate of Interest: 8
AGR Rate of Interest: 7
CTG Rate of Interest: 9
```

#### 3.1.Một số câu hỏi về ghi đè phương thức (method overriding) trong java

`Có ghi đè được phương thức static không?`

* Không, phương thức static không thể ghi đè được, bởi vì ghi đè phương thức được thực thi lúc runtime (tính đa hình).

`Tại sao không ghi đè được phương thức static?`
* Vì phương thức static được ràng buộc với class, còn phương thức instance được ràng buộc với đối tượng. Static thuộc về vùng nhớ class còn instance thuộc về vùng nhớ heap.

`Có ghi đè phương thức main được không?`
* Không, vì main là phương thức static.






