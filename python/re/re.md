
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

**功能：** 从头开始匹配返回第一个匹配对象，匹配失败返回None<br>

**Demo**:
```python
print(re.match('www', 'www.Darr_en1.com').group())   #www
print(re.match('arr', 'www.Darr_en1.com').group())   #AttributeError: 'NoneType' object has no attribute 'group'
```

### re.search 匹配包含

**原型:** search(pattern,string,flags=0)<br>

**功能：** 扫描整个字符串返回第一个匹配对象，匹配失败返回None<br>

**Demo**:
```python
print(re.search('www', 'www.Darr_en1.com').group())  #www
print(re.search('arr', 'www.Darr_en1.com').group())  #arr
```

### re.compile 预编译

**原型:** compile(pattern,flags=0)<br>

**功能：**  把正则表达式编译成一个正则对象

#### 在看《python核心编程》（第3版）对于编译的说法，深有体会，以下摘录：<br>
> 编译正则表达式（编译还是不编译？）<br>
&emsp;&emsp;在 Core Python Programming 或者即将出版的 Core Python Language Fundamentals 的执行环境章节中，介绍了 Python 代码最终如何被编译成字节码，然后在解释器上执行。特别是，我们指定 eval()或者 exec（在 2.x 版本中或者在 3.x 版本的 exec()中）调用一个代码对象而不是一个字符串，性能上会有明显提升。这是由于对于前者而言，编译过程不会重复执行。换句话说，使用预编译的代码对象比直接使用字符串要快，因为解释器在执行字符串形式的代码前都必须把字符串编译成代码对象。<br>
&emsp;&emsp;同样的概念也适用于正则表达式—在模式匹配发生之前，正则表达式模式必须编译成正则表达式对象。由于正则表达式在执行过程中将进行多次比较操作，因此强烈建议使用预编译。而且，既然正则表达式的编译是必需的，那么使用预编译来提升执行性能无疑是明智之举。re.compile()能够提供此功能。<br>
&emsp;&emsp;其实模块函数会对已编译的对象进行缓存，所以不是所有使用相同正则表达式模式的 search()和 match()都需要编译。即使这样，你也节省了缓存查询时间，并且不必对于相同的字符串反复进行函数调用。在不同的 Python 版本中，缓存中已编译过的正则表达式对象的数目可能不同，而且没有文档记录。purge()函数能够用于清除这些缓存。<br>

**Demo**:
```python
re_obj = re.compile("www")
print(re_obj.match('www.Darr_en1.com').group())   #www
```

### re.findall 匹配包含返回列表

**原型:** findall(pattern,string,flags=0)<br>

**功能：** 扫描整个字符串返回结果列表，匹配失败返回None<br>

**Demo**:
```python
mail='<Darr_en101@mail.com> <Darr_en102@mail.com> Darr_en103@mail.com'
print(re.findall(r'(\w+@m....[a-z]{3})',mail))    #['Darr_en101@mail.com', 'Darr_en102@mail.com', 'Darr_en103@mail.com']
```

### re.finditer 匹配包含返回迭代器

**原型:** findall(pattern,string,flags=0)<br>

**功能：** 扫描整个字符串返回迭代器，可防止内存过大现象<br>

**Demo**:
```python
mail='<Darr_en101@mail.com> <Darr_en102@mail.com> Darr_en103@mail.com'
print(next(re.finditer(r'(\w+@m....[a-z]{3})',mail)).group())    #Darr_en101@mail.com
```

### re.split  以匹配到的字符当做列表分隔符

**原型:** split(pattern, string, maxsplit=0, flags=0)

**参数：** maxsplit：最大分割字符串，默认为0，表示每个匹配项都分割

**Demo**:
```python
str ="Darr_en1     is so cool"
print(re.split(r' +',str))   #['Darr_en1', 'is', 'so', 'cool']
print(str.split(' '))        #['Darr_en1', '', '', '', '', 'is', 'so', 'cool']
```
### re.sub 替换字符串的匹配项

**原型**： sub(pattern, repl, string, count=0)

**参数：** <br>
rep1:替换后的字符串<br>
count：替换个数,默认为0，表示每个匹配项都替换<br>

**功能：** 替换字符串的匹配项，返回str<br>

**Demo**:
```python
str="Darr_en1 is so cool"
print(re.sub(r'\s','-',str))    #Darr_en1-is-so-cool
print(re.sub(r'\s','-',str,2))  #Darr_en1-is-so cool
```

### re.subn 替换字符串的匹配项

**原型**： subn(pattern, repl, string, count=0)

**参数：** <br>
rep1:替换后的字符串<br>
count：替换个数,默认为0，表示每个匹配项都替换<br>

**功能：** 替换字符串的匹配项，返回tuple,第一个值为被替换的str，第二个值为被替换次数<br>

**Demo**:
```python
str="Darr_en1 is so cool"
print(re.subn(r'\s','-',str))    #('Darr_en1-is-so-cool', 3)
print(re.subn(r'\s','-',str,2))  #('Darr_en1-is-so cool', 2)
```

### group() groups()       分组

**功能：** 通过()来进行分组，group(n)返回第n个值,groups()返回tuple<br>

**Demo**:
```python
str="Darr_en1-is-so-cool"
print(re.findall(r'(\w+)(-)',str))           #[('Darr_en1', '-'), ('is', '-'), ('so', '-')]
print(re.findall(r'\w+-',str))               #['Darr_en1-', 'is-', 'so-']
print(re.match(r'(\w+)(-)',str).group())     # Darr_en1-
print(re.match(r'(\w+)(-)',str).group(0))    # Darr_en1-
print(re.match(r'(\w+)(-)',str).group(1))    # Darr_en1
print(re.match(r'(\w+)(-)',str).group(2))    # -
print(re.match(r'(\w+)(-)',str).groups())    # ('Darr_en1', '-')
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


