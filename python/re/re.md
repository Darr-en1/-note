
# re(正则表达式)

## 一、基本语法

### re.match 从头匹配

**原型:** match(pattern,string,flags=0)<br>

**参数：**<br>
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

**功能：** 从头开始匹配，匹配失败返回None<br>

### re.search 匹配包含

**原型:** search(pattern,string,flags=0)<br>

**功能：** 扫描整个字符串返回第一个匹配，匹配失败返回None<br>

### re.findall 匹配包含返回列表

**原型:** findall(pattern,string,flags=0)<br>

**功能：** 扫描整个字符串返回结果列表，匹配失败返回None<br>

### re.split  以匹配到的字符当做列表分隔符

**原型:** split(pattern, string, maxsplit=0, flags=0)

**参数：** maxsplitmaxsplit为最多被分割的字符串
```python
str ="Darr_en1     is so cool"
print(re.split(r' +',str))   #['Darr_en1', 'is', 'so', 'cool']
print(str.split(' '))        #['Darr_en1', '', '', '', '', 'is', 'so', 'cool']
```
<br>

## 二、常用正则表达式符号

### 单个字符
```
'.'     　 匹配除\n之外的任意一个字符，若指定flag DOTALL,则匹配任意字符，包括换行
'[]'       匹配括号内的所有字符,第一个字符^为取反
```
### 预定义字符集
```
'\d'       匹配数字[0-9]
'\D'       匹配非数字,即[^0-9]
'\w'       匹配单词，即[A-Za-z0-9_]
'\W'       匹配非单词,即[^A-Za-z0-9_]
'\s'       匹配空格、\t、\n、\r , 即[<空格>\f\n\r\t],re.search("\s+","ab\tc1\n3").group() 结果 '\t'
'\S'       匹配非空格、\t、\n、\r , 即[^<空格>\f\n\r\t]
```
### 锚字符（边界字符）
```
'^'      　匹配字符开头，若指定flags MULTILINE,这种也可以匹配上(r"^a","\nabc\neee",flags=re.MULTILINE)
'\A'       匹配字符开头，同$区别是，只匹配整个字符串开头，在re.M下匹配第一行开头
'$'      　匹配字符结尾，或e.search("foo$","bfoo\nsdfsf",flags=re.MULTILINE).group()也可以
'\Z'       匹配字符结尾，同$区别是，只匹配整个字符串结尾，在re.M下匹配最后一行结尾
'\b'       匹配单词边界，即匹配\W和\w之间的位置
'\B'       匹配非单词边界
```
### 量数词(匹配多个字符)
```
'*'      　匹配*号前的字符0次或多次，re.findall("ab*","cabb3abcbbac")  结果为['abb', 'ab', 'a']
'+'      　匹配前一个字符1次或多次，re.findall("ab+","ab+cd+abb+bba") 结果['ab', 'abb']
'?'      　匹配前一个字符1次或0次
'{m}'    　匹配前一个字符m次
'{n,m}' 　 匹配前一个字符n到m次，re.findall("ab{1,3}","abb abc abbcbbb") 结果'abb', 'ab', 'abb']
'{m,}'     匹配前一外字符至少 m次 至多无限次；
'{,n}'     匹配前一个字符 0 到 n次
'|'        匹配|左或|右的字符，re.search("abc|ABC","ABCBabcCD").group() 结果'ABC'
'(...)' 　 分组匹配，re.search("(abc){2}a(123|456)c", "abcabca456c").group() 结果 abcabca456c
```
#### 贪婪匹配 非贪婪匹配
```
贪婪模式在整个表达式匹配成功的前提下，尽可能多的匹配。
非贪婪模式在整个表达式匹配成功的前提下，尽可能少的匹配。

属于贪婪模式的量词，也叫做匹配优先量词，包括：
“{m,n}”、“{m,}”、“?”、“*”和“+”。

属于非贪婪模式的量词，也叫做忽略优先量词，包括：
“{m,n}?”、“{m,}?”、“??”、“*?”和“+?”。

举例：
源字符串：aa<div>test1</div>bb<div>test2</div>cc
正则表达式一：<div>.*</div>
匹配结果一：<div>test1</div>bb<div>test2</div>
正则表达式二：<div>.*?</div>
匹配结果二：<div>test1</div>,<div>test2</div>
```


