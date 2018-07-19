
# re(正则表达式)

## 基本语法

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

