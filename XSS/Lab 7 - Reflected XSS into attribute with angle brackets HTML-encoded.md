![[Pasted image 20220312010323.png]](https://github.com/LanPhuong07/PortSwigger/blob/main/pic/Pasted%20image%2020220312010323.png)

*Lab này xảy ra Reflected XSS ở function search.* 

Thử nhập abc vào thanh search thì thu được kết quả: 

![[Pasted image 20220312010850.png]](https://github.com/LanPhuong07/PortSwigger/blob/main/pic/Pasted%20image%2020220312010850.png)

String được hiển thị thẻ h1 và thuộc tính được trích dẫn 

⇒ Sử dụng payload đơn giản

![[Pasted image 20220312011401.png]](https://github.com/LanPhuong07/PortSwigger/blob/main/pic/Pasted%20image%2020220312011401.png)

Payload đã sử dụng:

*"onmouseover="alert(1)

" autofocus onfocus = alert (1) x = "*

