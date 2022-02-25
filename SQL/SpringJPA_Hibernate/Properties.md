# Config application.properties

## Hibernate config
``` 
spring.jpa.show-sql=true 
dùng để hiển thị các câu lệnh sql trong terminal hay không
```


```
spring.jpa.hibernate.ddl-auto=create-drop

- Kiểm soát việc tạo cơ sở dữ liệu với Hibernate
 Spring cung cấp một thuộc tính JPA cụ thể mà Hibernate có thể sử dụng nó để tạo ra DDL: spring.jpa.hibernate.ddl-auto

- Các giá trị 

 * create: trước tiên hibernate sẽ drop các bảng đang có và sau đó tạo ra các bảng mới 
 
 * update: Mô hình đối tượng được tạo dựa trên việc ánh xạ (thông qua các annotation hoặc 
 XML) được so sánh với dữ liệu hiện có trong schema và sau đó Hibernate sẽ cập nhật lại
schema với những thông tin mới. Nó sẽ không bao giờ xóa đi các bảng hay các cột đang có ngay cả khi chúng không còn được ứng dụng của ta yêu cầu nữa.

* create-drop: Tương tự như create nhưng sau khi tất cả các hoạt động đã được hoàn thành, Hibernate sẽ thực hiện việc drop database. Thường được sử dụng cho UNIT TEST

* validate: Hibernate chỉ xác thực xem các bảng và các cột có tồn tại hay không, nếu không nó sẽ ném ra một ngoại lệ (exception).

* none: Giá trị này được dùng để tắt việc tạo DDL.

```

```
spring.jpa.properties.hibernate.format_sql=true

-Dùng để format sql đẹp hơn
-Mặc dù cách này cực kỳ đơn giản, nhưng nó không được khuyến khích vì nó xuất trực tiếp các câu truy vấn ra các thiết bị output mà không có bất kỳ một sự tối ưu nào từ các logging framework.  
-Ngoài ra, đối với cách này thì các tham số đầu vào cho các câu truy vấn cũng không được xuất ra.
```

```
spring.jpa.properties.hibernate.dialect

- Chọn csdl dùng 
```

```
logging.level.org.hibernate.SQL=debug
```

