### 因为先接触java的缘故，因此对于python中，java不存在或者与java不同的或者比较有趣的知识点进行整理

1.Python中，（*）会把接收到的参数形成一个元组，而（**）则会把接收到的参数存入一个字典<br><br>

2.对于  if __name__ == '__main__': <br>
①.当此文件当做模块被调用时，不会从这里执行，因为此时name属性就成了模块的名字，而不是main。<br>
②.当此文件当做单独执行的程序运行时，就会从main开始执行。<br>
③.对于没有缩进的程序段，按照顺序执行。然后，才到main函数。然后才按照main内函数的执行顺序执行。
如果main内对类进行了实例化，那么执行到此处时，只会对类内成员进行初始化，然后再返回到main 函数中。 
执行其他实例化之后对象的成员函数调用。<br><br>

3.setattr(user, k, v)    给user对象的K属性赋v值<br><br>

4.python是弱类型的语言，定义一个变量，在函数中进行赋值，局部变量不能在赋值前被引用。global在函数中将其声明为全局变量即可。但声明时不可赋值。<br><br>

5.通过list,tuple 创建dict      
dict([["name","zs"],["age",18]]) ====>{'name': 'zs', 'age': 18}<br>
dict([("name","zs"),("age",18)]) ====>{'name': 'zs', 'age': 18}<br>
<br>
