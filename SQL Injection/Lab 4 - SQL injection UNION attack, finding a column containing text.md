![[Pasted image 20220303220149.png]](https://github.com/LanPhuong07/PortSwigger/blob/main/pic/Pasted%20image%2020220303220149.png)

**Mô tả:**

SQL injection trong bộ lọc danh mục sản phẩm. Kết quả từ truy vấn được trả về trong phản hồi của ứng dụng, vì vậy bạn có thể sử dụng cuộc tấn công UNION để truy xuất dữ liệu từ các bảng khác. 

**Các bước cần làm:**

- Xác định số cột (sử dụng order by hoặc union null)
- Xác định kiểu dữ liệu của từng cột

**Giải quyết**

Chọn danh mục sản phẩm, bắt request bằng BurpSuite. Thử giá trị order by: 

![[Pasted image 20220303220919.png]](https://github.com/LanPhuong07/PortSwigger/blob/main/pic/Pasted%20image%2020220303220919.png)

Thử kiểu dữ liệu text ở từng cột cho đến khi respose trả về 200:

![[Pasted image 20220303221740.png]](https://github.com/LanPhuong07/PortSwigger/blob/main/pic/Pasted%20image%2020220303221740.png)

-> Cột 2 có thể chèn string

Chèn string theo yêu cầu:

![[Pasted image 20220303222359.png]](https://github.com/LanPhuong07/PortSwigger/blob/main/pic/Pasted%20image%2020220303222359.png)

Solved!