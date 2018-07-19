
# re(正则表达式)
## 基本语法
### re.match
**原型：**match(pattern,string,flags=0)<br>
<br>
**参数：**
patter:匹配的正则表达式<br>
string:要匹配的字符串<br>
flags:标志位，控制正则表达式匹配方式有如下：<br>
```
re.I	使匹配对大小写不敏感
re.L	做本地化识别（locale-aware）匹配
re.M	多行匹配，影响 ^ 和 $
re.S	使 . 匹配包括换行在内的所有字符
re.U	根据Unicode字符集解析字符。这个标志影响 \w, \W, \b, \B.
re.X	该标志通过给予你更灵活的格式以便你将正则表达式写得更易于理解。
```
**功能：** 从头开始匹配，匹配失败返回None
### re.search 匹配包含
### re.findall 把所有匹配到的字符放到以列表中的元素返回
### re.split  以匹配到的字符当做列表分隔符
