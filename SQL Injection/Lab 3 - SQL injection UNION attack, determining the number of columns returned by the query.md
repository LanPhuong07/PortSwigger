![[Pasted image 20220302194844.png]](https://github.com/LanPhuong07/PortSwigger/blob/main/pic/Pasted%20image%2020220302194844.png)

**Mô tả:**

Lab này chứa lỗ hổng SQL injection trong bộ lọc danh mục sản phẩm. Kết quả từ truy vấn được trả về trong phản hồi của ứng dụng, vì vậy bạn có thể sử dụng một cuộc tấn công UNION để truy xuất dữ liệu từ các bảng khác. Bước đầu tiên của một cuộc tấn công như vậy là xác định số lượng cột đang được trả về bởi truy vấn. Sau đó, bạn sẽ sử dụng kỹ thuật này trong các phòng thí nghiệm tiếp theo để xây dựng cuộc tấn công đầy đủ.

Để giải quyết lab này, cần xác định số cột được trả về bởi truy vấn bằng cách thực hiện một cuộc tấn công SQL injection UNION trả về một hàng bổ sung chứa giá trị null.

**Giải quyết:**

Chọn một category bất kỳ và bắt request bằng Burpsuite. Thêm payload *order by* để xác định số cột: 

![[Pasted image 20220302195718.png]](https://github.com/LanPhuong07/PortSwigger/blob/main/pic/Pasted%20image%2020220302195718.png)

Với số cột là 3, response trả về 200 -> số cột đúng.

Thực hiện tấn công SQLi UNION: 

![[Pasted image 20220302200211.png]](https://github.com/LanPhuong07/PortSwigger/blob/main/pic/Pasted%20image%2020220302200211.png)

