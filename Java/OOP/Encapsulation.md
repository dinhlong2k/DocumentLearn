# Tính đóng gói (Encapsulation)

- Tính đóng gói là kỹ thuật ẩn giấu thông tin không liên quan và hiện thị ra thông liên quan. Mục đích chính của đóng gói trong java là giảm thiểu mức độ phức tạp phát triển phần mềm.

<p align="center">
  <img src="./assets/Encapsulation.png" />
</p>

- Tính bao đóng trong Java là một tiến trình đóng gói code và dữ liệu lại với nhau vào trong một đơn vị unit đơn. Chúng ta có thể tạo một lớp được bao đóng hoàn toàn trong Java bằng việc tạo tất cả thành viên dữ liệu của lớp là private. Bây giờ, chúng ta sử dụng phương thức setter và getter để thiết lập và lấy dữ liệu trong nó.

- Tính bao đóng là kỹ thuật tạo một trường của lớp private và cung cấp khả năng truy cập trường này qua các phương thức pullic. Nếu một trường được khai báo là private, nó không thể được truy cập bởi bên ngoài lớp, do đó có thể che dấu các trường có lớp này. Vì lý do này, tính bao đóng được ám chỉ như việc dấu dữ liệu (data hiding).

-	Để đạt được đóng gói trong Java chúng ta cần:
    +  Khai báo các biến của một lớp là private.
    +   Cung cấp phương thức setter và getter là public để có thể sửa đổi và xem các giá trị biến.

``` 
package com.gpcoder.encapsulation;
 
public class Student {
    private String name;
 
    public String getName() {
        return name;
    }
 
    public void setName(String name) {
        this.name = name;
    }
}
```

<p align="center">
  <span>Student.java</span>
</p>


Các phương thức public setXXX() và getXXX() là các điểm truy cập đến các biến của lớp Student. Thông thường, các phương thức này được gọi là getters và setters. Vì vậy, bất kỳ đối tượng nào nào muốn truy cập vào các biến private sẽ truy cập chúng thông qua các trình getters và setters này.

Các biến của lớp Student có thể được truy cập như chương trình dưới đây:

```
package com.gpcoder.encapsulation;
 
public class EncapsulationExample {
 
    public static void main(String[] args) {
        Student s = new Student();
        s.setName("gpcode.com");
        System.out.println(s.getName());
    }
}

```

-	Lợi ích của đóng gói trong java
    + Tất cả các trường (field) của lớp có có chế độ chỉ đọc (read-only) hoặc chỉ ghi (write-only), tức là chỉ có hàm getter hoặc setter.
    + Một lớp có thể có toàn bộ điều khiển thông qua những gì được lưu giữ trong các trường (field) của nó.
    + Người sử dụng của class không biết cách các class lưu trữ dữ liệu. Một class có thể thay đổi kiểu dữ liệu của một trường và người dùng class không cần sự thay đổi trong code.

