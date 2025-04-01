---
title: PythonNotes
tags: Python
categories: PythonNotes
date: 2024-09-29
sticky: 11
thumbnail: "/images/PythonNotes/miku_point_buckground.png"
cover: "/images/PythonNotes/miku_point_buckground.png"
excerpt: "好好看,好好学"
---
Python Notes _Base Grammars 

## 基础语法
P(屁) y(眼) t(通) hon(红)
![](/images/PythonNotes/xuehuan_cry.png)

### 标准代码架构
``` python
def find7():  #含参fuction
    num_I = 1
    while num_I<= 100:
        if num_I % 7 == 0 or '7' in str(num_I):
            num_yv = num_I
            print(f'{num_yv}')
            num_I += 1
        else:
            num_I += 1

def main():  #主函数执行fuction调用
    find7()

if __name__ == "__main__":  #启动语句
    main()
```
优秀的代码架构是后期修bug的救命稻草

### 数据转换&数据计算

``` python
bin(x) #转为2进制 
oct(x) #转为8进制
int(x) #转为10进制,整数  常用 y = int(input('啊吧啊吧'))
hex(x) #转为16进制
float(x) #转为浮点数
complex(x) #转为复数
_________________________
+,-,*,/
% #取余
// #整除
** #幂运算
__________________________
num += 2 #表示num = num + 2
-=,*=,/=,//=,%=,**=
__________________________
```

在实际应用中二,八,十六进制数的显示方式分别为 : 

```python
# 十进制转换为其他进制
num = 26

# 十进制转为二进制
binary_num = bin(num)  # 输出为 '0b11010'
print(f'{num} 的二进制表示为: {binary_num}')

# 十进制转为八进制
octal_num = oct(num)  # 输出为 '0o32'
print(f'{num} 的八进制表示为: {octal_num}')

# 十进制转为十六进制
hex_num = hex(num)  # 输出为 '0x1a'
print(f'{num} 的十六进制表示为: {hex_num}')
```

带有 `0x` 前缀的数字代表十六进制数，`0b` 前缀代表二进制数，`0o` 代表八进制数。

### 逻辑&逻辑运算符

``` python
if x < y :
	print(x)
elif x = y:
	print(x)
else :
	print(y)
_______________________
while x < y :
	print(x)
______________________
# if 和 while 的判断条件输出的是bool值,因此可用 while True : 来实现无线循环
判断条件:
==,!=,>,<,>=,<=
x and y #x和y均为true时输出y
x or y #x和y均为true时输出x
not x  #x为true时输出false
x in ['商业贷款', '公积金贷款', '组合贷款']:
x not in ['商业贷款', '公积金贷款', '组合贷款']: #用于判断多个条件中是否含有其中一个

_____________________
for i in rang(5) : #循环遍历数组里的元素
	print(i)
________________________
break #结束循环,执行下一段代码
continue #跳过本次循环,执行下一次循环

```

好啊

### 字符串
``` python
print('啊吧啊吧')
print(f"贷款年限：{years} 年") #f'{x}'用于在字符串中输出变量x
print('啊吧啊吧'\n) #\n为换行符
\b,退格  \n,换行  \v,纵向制表 \t,横向制表 \r,回车
________________________________________________
# 格式化字符串的输出方式
value = 10
string_x = '我今年%d岁' #字符串中变量用%d格式化为整数
print(string_x % value) #输出时按照 字符串%参数 的样式书写

#数据格式化符
%c #格式化为字符
%s #格式化为字符串
%d #格式化为整数
%u #格式化为无符号整型
%o #格式化为八进制数
%x #格式化为十六进制数
%f #格式化为浮点数
________________________________________________
str_x.find('a',0,5) #目标字符串.find('指定查出找的字符',起始索引,结束索引)
#输出指定字符在字符串中的索引序号
_________________________________________________
str_x.replace('a','b',3) #目标字符串.replace('指定字符','新字符',替换次数(默认全部替换)) 
#替换字符
_________________________________________________
str_x.split('/',3) #目标字符串.split('分割符号(默认为空格)',分割次数(默认全部))
#分割字符串
__________________________________________________
str_x.jion('a') #目标字符串.join('连接字符串的字符')
__________________________________________________
str_x = 'aabb'
str_y = 'bbcc'
print(str_x + str_y) #+号课实现字符串首尾拼接
__________________________________________________
.strip('a')#移除首尾指定字符
.lstrip('a')#移除右端指定字符(left strip)
.rstrip('a')#移除左端指定字符(right strip)
.upper()#字符串全转换为大写字母
.lower()#字符串全转换为小写字母
.capitalize()#字符串中第一个字母大写
.title()#字符串每个单词字母大写
.center(13,'_')#字符串居中  #目标字符串.center(字符串总长度,补齐两端的符号)
.ljust(13,'_')#字符串向左对齐 #目标字符串.ljust(字符串总长度,补齐右端的符号)
.rjust(13,'_')#字符串向左对齐 #目标字符串.rjust(字符串总长度,补齐左端的符号)
__________________________________________________
#在字符串操作中总有将指定字符进行参数化,以实现模块化修改
string_x = 'okjuhtabab'
find_y = 'o'
res_1 = string_x.find(find_y,0,5)
print(res_1)
__________________________________________________

```
好好好

## 数据类型

### 列表
``` python
list_x = [1,'p',6,'o']#手动创建
list_x =list(1,'p',6,'o',6)#list()方法创建
#同一元素可重复
_________________________________________
#以切片索引的方式访问和调用列表中的元素
print(list_x[1:4:3])#目标列表[起始索引:结束索引:步长]
_________________________________________
#添加末尾元素
list_x.append('a')#目标列表.append(元素or参数)
_________________________________________
#末尾接新列表
list_x.extend(list_y)#目标列表.append(新列表)
_________________________________________
#指定索引插入元素
list_x.insert(2,'a')#目标列表.insert(索引序号，新元素)
_________________________________________
#按特定顺序排列
list_x.sort()#目标列表.sort(key排序规则，布尔值（True为降序False为升序）)  
#在（）为空时，默认为字符串以大写字母有限的正序排列，数字升序排列
#string和数字无法进行sort排列
#常用的key：
.sort(key=len)  # 按字符串长度排序
.sort(key=str.lower)  # 忽略大小写进行排序
.sort(key=lambda x: x[1]) #自定义排序规则  #按第二个元素（字符串）排序，x:x[元素内索引号]
_________________________________________
#升序排列列表元素并赋值到新列表，原列表排序不变
list_y = sorted(list_x)#新列表 = sorted(原列表)
_________________________________________
#反转列表排序
list_x.reverse()
_________________________________________
#按索引删除元素.s
del list_x[1] #del 目标列表[索引]  
#当为 del list_x 是为删除整个列表，此时list_x的定义也会消失
_________________________________________
#按索引删除元素.f
list_x.pop(4) #目标列表.pop(索引序号) #当()为空是为删除最后一个元素
_________________________________________
#清空列表，列表定义依然存在
list_x.clear()
_________________________________________
#按值删除元素,若列表又多个同一元素仅删除匹配到的第一个元素
list_x.remove('a') #目标列表.remove(目标值）
_________________________________________



```

好得很呐

### 元组
``` python
tuple_x = (1,'a',6)
_________________________________________
#元组可称为列表中的元素
list_x = [(3,'o')(1,'a'),(8,'g'),(2,'i')]
#在使用元组式列表时元组同索引的数据类型必须相同，否则无法进行排序
_________________________________________
#按索引切片访问元组
print(tuple_x[2:5:2])#目标元组[起始索引:结束索引:步长]
_________________________________________

```

好的不得了

### 集合
``` python
set_x = {1,'a',6}
set_x = {(3,'o')(1,'a'),(8,'g')}
set_x = {[1,'p',6,'o'],[6,'i',9,8]}
#集合中的元素具有唯一性
_________________________________________
#集合可包含列表、元组  #其本身为可变类型
set_x = {1,'a',6,(3,'o'),[1,'p',(2,'i')]}
_________________________________________
#set()传入元素
set_x = set([6,(3,'o'),1,'p',range(5)])
#set仅支持单次传入一种类型的数据，当需要传入不同类型数据时可将他们放入列表中，再进行传入
_________________________________________
#添加元素
set_x.add('a')#目标集合.add(元素)
_________________________________________
#按值删除元素，当元素不存在时输出KeyError
set_x.remove('a')#目标集合.remove(元素)
_________________________________________
##按值删除元素，当元素不存在时不做操作
set_x.discard('a')#目标集合.discord(元素)
_________________________________________
#随机返回一个元素，并删除再集合中该元素
y = set_x.pop()#目标集合.pop(元素)
_________________________________________
#清空集合,定义依然存在
set_x.clear()
_________________________________________
#复制集合
set_y = set_x.copy()
_________________________________________
#判断两个集合中是否有相同的元素，有相同元素输出False,无相同元素输出True
set_x.isdisjoint(set_y)#目标集合.isdisjiont(另一集合)
_________________________________________



```

这也太好了吧

### 字典
``` python
dictionary_x = {'a':1,'b':2,'k':'p',2:'o'，'l':1}# {key:value}
#字典元素无序，key 唯一 ,value 可有多个重复
_________________________________________
#按key值访问字典元素
print(dictionary_x.get('a'))#目标字典.get(key值)
_________________________________________
#仅访问所有key值
print(dictionary_x.key())#目标字典.key()
_________________________________________
#仅访问所有values值
print(dictionary_x.values())#目标字典.values()
_________________________________________
#仅访问所有items值
print(dictionary_x.items())#目标字典.items()
_________________________________________
#根据key值修改value，当key值不在字典中，则视为添加新key
dictionary_x['a'] = 8 #目标字典[key值] = value
_________________________________________
#使用update修改value
dictionary_x.update('a'=8)#目标字典.update(key值 = value)
_________________________________________
#按key值删除元素
dictionary_x.pop('a')#目标字典.pop(key值)
_________________________________________
#随机删除元素
dictionary_x.popitem()#目标字典.popitem()
_________________________________________
#清空z字典,定义依然存在
dictionary_x.clear()


```
好好好

### 组合数据类型应用运算符
``` python
#字符串，列表，元组，字典均可使用 + 来进行同类型元素合并
dictionary_z = dictionary_x + dictionary_y
list_z = list_x + list_y
_________________________________________
# * 实现表内元素自行复制
list_z = list_x * 3
#判断元素是否在表内,返回值为bool
print('a' in list_x)
print('a' not in list_x)
```

没见过这么好的


## 函数

### 函数参数
``` python
def fuction_x(a,b): 
	result = a + b 
    def fuction_y(a,b,/,c):
    	y = c + d

```

简直令人惊叹不已

### 参数传递
``` python
def fuction_x(a,b): #a和b称为形参,在调用函数时可通过对应位置进行传参
	result = a + b
_____________________________________________________    
#位置参数传递
fuction_x(2,3) #2和3称为实参,实际传入fuction_x中的参数
_____________________________________________________
#关键字参数传递
fuction_x(a=2,b=3) #在参数数量过多时,关键字参数传递更为优秀
_____________________________________________________
#传递限制
def fuction_x(a,b,/,c,d): # /前的参数仅能接受位置传递,/后的参数二者均可
_____________________________________________________
#参数混合传递
def fuction_x(a,b,*c,**d):
	print(a,b,*c,d) #print不接受字典形式的参数,因此应写为d而不是**d
fuction_x(1,'o',(4,5,9),p=2)

```

让人心潮澎湃的好啊

### 参数打包/解包
``` python
#参数打包
def fuction_x(*a): # *a为以元组形式接受参数
fuction_x(11,23,56,80)

def fuction_x(**b): #**b为以字典形式接受参数
fuction_x(a=11,b=22,c=90) #在字典传递参数时应遵循 key=value 的形式,字符串不用引号
_____________________________________________________
#参数解包,用于组合数据向多个单数据接口传输
def fuction_x(a,b,c,d,e):
parameter_x = (1,2,3,4,'p')
fuction_x(*parameter_x) #parameter_x被解包成多个单数据,并按照索引传fuction_x
#当组合数据与单数据接口数不对应时会报错

def fuction_x(a,b,c,d,e):
parameter_x = {'a':1,'b':2,'k':'p',2:'o',5:'n'}
fuction_x(**parameter_x) #解包字典后传入的是value值

```

实在是太令人满意了呀

### 参数返回值
``` python
def fuction_x(a,b):
    c = a + b
    return c #return将值返回到主程序中,同时程序回到函数被调用的时候继续执行
print(fuction_x(1,2)) #此时fuction_x(1,2)实际被替换成了c的值
#当return多个值的时候将返回元组

```

真是无可挑剔的完美体验

### 变量作用域
``` python
#局部变量
def fuction_x():
    a = 5 #对于变量a,只能在函数内调用,函数外无a的定义
_____________________________________________________
#全局变量 #global 变量
a = 1 
b = 3 #在函数外定义变量之后可被全局调用
def fuction_x():
    global a #声明a为全局变量,实现函数内外a值互通
    b += 1 #在b进行迭代时,外部定义将被覆盖,此时a又变成了局部变量,此步会报错,需像a一样声明全局变量
	a += 2
    c = a + b 
_____________________________________________________
#嵌套函数变量 #nonlocal 变量        
def fuction_x():
    def fuction_y():
        nonlocal a #声明局部作用变量a,使得fuction_x可以调用a,同时不溢出整个函数
        a = 2
    fuction_y()
    b = a + 1
    print(b)

fuction_x()
```



### 递归/匿名函数

这个学起来有点费劲,回头再补

``` python
啊吧 啊吧 啊吧
```





## 文件/数据 操作



### 标准文件访问方法
``` python
# 打开文本文件
file_path = 'F:\\mulyilytest\\pytest.txt' #文件地址参数化 #地址区分符号用\\

with open(file_path, 'r', encoding='utf-8') as file_01: #as后命名文件在代码中的参数名
    content = file.read()  #读取文件内容并参数化
```

### 文本文件操作

``` python
#打开文件
flie_01 = open('F:\\genshinUsercount.txt','r',encoding='utf-8')#open('路径','打开模式','编码格式')#常用的编码格式 : ascii , utf-8 , Unicode , gbk

r/rb #以只读方式打开
w/wb #以只写方式打开,若文件不存在则创建新文件,此模式下执行写入会覆盖原来数据
a/ab #以追加方式打开,若文件不存在则创建新文件

_____________________________________________________
#关闭文件
file_01.close()
_____________________________________________________
#文件操作前置语句
with open(file_path, 'r', encoding='utf-8') as file_01:  
#with open() as filename : #as后命名文件在代码中的参数名
_____________________________________________________
#读取文件内容
print(file_01.read(2)) #file_01.read(字节索引) #当索引为空或-1是为全读
content = file_01.read()

file_01.readline() #读取指定文件的一行数据,当二次调用.readline()时会读取下一行数据

file_01.readlines(5) #读取指定文件的多行数据,当索引为空或-1是为全读

_____________________________________________________
#文件写入
file_01.write('abcd114514') #在文件末尾写入数据,无法换行

file_01.writelines('abcd114514 \n 啊实打实打算') #可用\n进行换行
_____________________________________________________
#获取当前读写索引
file_01.tell() #文件每次被读写一个位置之后会接着上一个位置往下进行读写,此方法可产看当前读写位置索引
_____________________________________________________
#读写索引控制
file_01.seek(5,0) #.seek(位置索引偏移量,指定位置索引) 
#指定位置索引值为 0时为文章开头 1时为当前位置 2时为文章结尾
_____________________________________________________


```


### 文件与目录(文件夹)管理
``` python
#文件管理需调用os模块
import os
_____________________________________________________
#删除文件
os.remove('F:\\mulyilytest\\python_test.txt')
_____________________________________________________
#文件重命名
os.rename('F:\\mulyilytest\\pytest.txt','F:\\mulyilytest\\python_test.txt') #os.rename(旧地址和名字,新) #通常将地址和名字参数化
_____________________________________________________
#创建/删除目录(文件夹)
os.mkdir('F:\\mulyilytest\\pytteesstt') #创建目录makedirectory
os.rmdir('F:\\mulyilytest\\pytteesstt') #删除目录removedirectory
_____________________________________________________
#获取当前目录
os.getcwd()
_____________________________________________________
#更改默认目录
os.chdir('F:\\mulyilytest')
#os在没有指定路径时会自动在默认中寻找文件,修改默认目录后可不在重复书写路经

_____________________________________________________
#获取文件名列表
os.listdir('./') #输出的是列表类型数据 # ./ 表示当前工作目录
 
```

### 数据维度与数据格式化

在代码输出栏里绘表???神金

## 面向对象		


### 概述
``` python
class cls_x:  # 创建类; class 类名称
    name_a = 66  # 类属性; 属性名 = 属性值

    def fuc_x(self,value):  # 实例方法; def 方法名(self);
        # 实例方法的第一个参数总是 self，它指向调用这个方法的具体实例对象
        self.value = value  #实例属性value,可接受外部传参
        print(self.value)
        instan_x = cls_x()  # 创建类的实例
        print(instan_x.name_a)  # 实例访问类属性；输出类属性

        instan_x.name_a = 1 #通过实例访问类属性并修改
        print(instan_x.name_a) #通过实例修改类属性后实例会在内存中创建一个专属于instan_x的name_a参数,不会对clas_x的name_a产生影响
        print(cls_x.name_a) #通过类访问属性发现值并未改变

        instan_x.str_new = '好i好i好i'
        print(instan_x.str_new)
        #print(cls_x.str_new) #类无法调用通过实例创建的新属性

        cls_x.str_new01 = 'n牛牛牛'
        print(instan_x.str_new01)
        print(cls_x.str_new01) #通过类创建的新属性,类和实例均可调用

        print('-----------------------------------------')

        cls_x.name_a = 9 #通过类访问类属性并修改
        print(instan_x.name_a) #通过类修改类属性后不影响实例属性
        print(cls_x.name_a)
        #类和实例的属性关系课理解为UE中母材质和材质实例的关系



    @classmethod # 类方法修饰符
    def fuc_y(cls): #类方法;; def 方法名(cls);
        # 类方法的第一个参数是 cls，它指向类本身，而不是具体的实例
        print('bbbb')
        instan_y = cls_x()
        print(instan_y.name_a)

        instan_y.str_new = '好i好i好i'
        print(instan_y.str_new)
        #print(cls_x.str_new) #类无法调用通过实例创建的新属性

    @staticmethod  # 类方法修饰符
    def fuc_z():
        print(111)

# 创建类的实例
instance = cls_x()

# 调用实例方法并向其传参;
instance.fuc_x(233) #调用实例方法必须先将类实例化,然后才能调用,该参数传给value而非self


cls_x.fuc_y() #调用类方法,类方法可直接通过类调用

cls_x.fuc_z() #调用静态方法,类方法可直接通过类调用

```


### 类创建
``` python
class cls_x:  # 创建类; class 类名称
    name_a = 66  # 类属性; 属性名 = 属性值
    
    def fuc_x(self,value):  # 实例方法; def 方法名(self);
        self.value = value  #实例属性value,可接受外部传参
        print(self.value)
```

### 类成员

类和实例的属性关系课理解为UE中母材质和材质实例的关系

``` python
#类/实例属性
class cls_x:  # 创建类; class 类名称
    name_a = 66  # 类属性; 属性名 = 属性值

    def fuc_x(self,value):  # 实例方法; def 方法名(self);
        # 实例方法的第一个参数总是 self，它指向调用这个方法的具体实例对象
        self.value = value  #实例属性value,可接受外部传参
        print(self.value)
        instan_x = cls_x()  # 创建类的实例
        print(instan_x.name_a)  # 实例访问类属性；输出类属性

        instan_x.name_a = 1 #通过实例访问类属性并修改
        print(instan_x.name_a) #通过实例修改类属性后实例会在内存中创建一个专属于instan_x的name_a参数,不会对clas_x的name_a产生影响
        print(cls_x.name_a) #通过类访问属性发现值并未改变

        instan_x.str_new = '好i好i好i'
        print(instan_x.str_new)
        #print(cls_x.str_new) #类无法调用通过实例创建的新属性

        cls_x.str_new01 = 'n牛牛牛'
        print(instan_x.str_new01)
        print(cls_x.str_new01) #通过类创建的新属性,类和实例均可调用

        print('-----------------------------------------')

        cls_x.name_a = 9 #通过类访问类属性并修改
        print(instan_x.name_a) #通过类修改类属性后不影响实例属性
        print(cls_x.name_a)
```

关于对象:实例和对象本质是一个东西,均为类的继承体

### 实例方法

``` python
class cls_x:  # 创建类; class 类名称
    name_a = 66
# 实例方法
    def fuc_x(self):  # 实例方法; def 方法名(self);slef代表函数本身
        print('aaaa')
#调用:
# 创建类的实例
instance = cls_x()
# 调用实例方法并向其传参;
instance.fuc_x(233) #调用实例方法必须先将类实例化,然后才能调用,该参数传给value而非self       
```

两种方法中属性修改和继承关系是相同的

### 类方法

``` python
class cls_x:  
    name_a = 6
#类方法       
    @classmethod # 类方法修饰符
    def fuc_y(cls): #类方法;; def 方法名(cls);cls代表类本身
        print('bbbb')    
 #调用:       
 cls_x.fuc_y() #调用类方法,类方法可直接通过类调用 
```

#### 类方法 vs 实例方法的区别

| 特性     | 实例方法                     | 类方法                           |
| -------- | ---------------------------- | -------------------------------- |
| 绑定对象 | 实例（`self` 指向实例对象）  | 类（`cls` 指向类本身）           |
| 装饰器   | 无特殊装饰器                 | `@classmethod`                   |
| 调用方式 | 通过实例调用                 | 通过类或实例调用                 |
| 访问权限 | 可以访问和修改实例属性和方法 | 不能访问实例属性，但可访问类属性 |
| 常见用途 | 操作对象实例，修改实例状态   | 操作类的状态，通常用于工厂方法   |


### 静态方法

``` python
class cls_x:  
    name_a = 6
#静态法
    @staticmethod  # 类方法修饰符
    def fuc_z():
        print(111)
#调用:
cls_x.fuc_z() #调用静态方法,类方法可直接通过类调用
        
```



#### 类方法 vs 静态方法的区别

| 特性     | 类方法                           | 静态方法                     |
| -------- | -------------------------------- | ---------------------------- |
| 绑定对象 | 类（`cls` 指向类本身）           | 无绑定对象                   |
| 装饰器   | `@classmethod`                   | `@staticmethod`              |
| 调用方式 | 通过类或实例调用                 | 通过类或实例调用             |
| 访问权限 | 可以访问类属性，不能访问实例属性 | 不能访问实例或类的任何属性   |
| 常见用途 | 操作类的状态，创建类方法         | 定义功能函数，逻辑上和类有关 |




### 私有成员

``` python
class cls_x :
    __attribute = 8  #__参数名 = 值
    def __fuction_1(self): #__方法名()
        print('aaa')

instanse_x = cls_x()
# instanse_x.__fuction_1() #无法从外部访问私有方法
# print(instanse_x.__attribute) #无法从外部访问私有参数

# 虽然私有成员不能直接访问，但可以通过名称改编来访问
print(instanse_x._cls_x__attribute) #实例名._类名__属性名
```

关于私有成员调用,看封装模块的代码

### 受保护成员

除了公有和私有成员，还有一种称为**受保护成员（Protected Members）**的概念，尽管 Python 本身没有严格的受保护机制,用处不大

``` python
class cls_x :
    _attribute = 8  #受保护参数 #_参数名 = 值
    def __fuction_1(self): #__方法名(self):
        print('aaa')

instanse_x = cls_x()
# instanse_x.__fuction_1() #无法从外部访问私有方法
# print(instanse_x.__attribute) #无法从外部访问私有参数

# 虽然私有成员不能直接访问，但可以通过名称改编来访问
print(instanse_x._cls_x__attribute) #实例名._类名__属性名
```

#### 共有成员 vs 私有成员 vs 受保护成员

| 特性     | 共有成员（Public Members） | 受保护成员（Protected Members） | 私有成员（Private Members）  |
| -------- | -------------------------- | ------------------------------- | ---------------------------- |
| 前缀     | 无前缀                     | `_` 开头                        | `__` 开头                    |
| 访问权限 | 类内外都可访问             | 子类可访问，外部不推荐访问      | 只能在类内部访问（但有例外） |
| 子类访问 | 可以访问                   | 可以访问                        | 无法直接访问                 |
| 外部访问 | 可以访问                   | 按照惯例不建议访问              | 不能直接访问                 |
| 使用场景 | 对外公开的成员             | 半封装，允许子类继承使用        | 完全封装，隐藏类的实现细节   |

### 构造方法

构造方法在创建类的对象时自动调用，用来初始化对象的属性。它是类的实例化过程中执行的第一个方法，常用于设置实例的初始状态。

相当于在类本身上附加一系列属性

``` python
class Person:
    def __init__(self, name, age): #构造方法 #__int__(self,属性名):
        self.name = name  # 初始化属性 name
        self.age = age  # 初始化属性 age

    def introduce(self):
        print(f"My name is {self.name}, and I am {self.age} years old.")


# 创建类的实例
person1 = Person("Alice", 30) #当 Person 类被实例化时，__init__ 方法被自动调用，设置了 name 和 age 属性

# 调用实例方法
person1.introduce()  # 输出: My name is Alice, and I am 30 years old.

```

### 析构方法

Python使用垃圾回收机制（Garbage Collection）来处理内存管理，当对象不再被引用时，它会自动调用 `__del__` 来进行清理。

值得注意的是，Python 的垃圾回收机制是基于引用计数的。当对象不再有任何引用时，Python 会自动回收内存并调用 `__del__` 方法。但在实际开发中，除非有明确的资源管理需求，通常不需要定义 `__del__`。

``` python
class FileManager:
    def __init__(self, filename):
        self.file = open(filename, 'w')
        print(f"{filename} 文件已打开")

    def __del__(self): #析构方法 #__del__(self):
        # 在对象被销毁时关闭文件
        self.file.close()
        print("文件已关闭")
```

#### 构造方法和析构方法的区别：

| 特性     | 构造方法 (`__init__()`)                            | 析构方法 (`__del__()`)                 |
| -------- | -------------------------------------------------- | -------------------------------------- |
| 作用     | 在对象创建时初始化属性                             | 在对象销毁时清理资源                   |
| 调用时机 | 对象实例化时自动调用                               | 对象销毁时自动调用                     |
| 使用场景 | 设置初始状态、传递参数                             | 释放资源（如文件关闭、网络连接关闭等） |
| 手动调用 | 通常不需要手动调用，但可以通过类名直接调用构造方法 | 不需要手动调用，由 Python 自动管理     |

### 封装

在 Python 中，封装通常结合**访问器方法**（getter 和 setter）来管理属性的访问与修改。访问器方法用于控制对私有或受保护属性的读取和写入

优秀的封装能大大降低维护难度

``` python
#标准封装
class Car:
    def __init__(self, brand, price,num):
        self.__brand = brand  #私有属性
        self.__price = price
        self.num = num  #共有属性
        
	# 标准私有值调用方法
    # getter 方法，用于获取私有属性的值
    def get_price(self):
        return self.__price  
    
	#标准属性修改方法
    # setter 方法，用于修改私有属性的值
    def set_price(self, new_price):
        if new_price > 0:
            self.__price = new_price * self.num
        else:
            print("Price cannot be negative!")

car = Car("Audi", 40000,2)
print(car.get_price())  

# 修改私有属性的值
car.set_price(45000)
print(car.get_price()) 
```

### 继承

定义一个子类，使它获得代码中已有类的属性和方法

``` python
#单继承（Single Inheritance）

# 定义一个父类
class Animal:
    def __init__(self, name):
        self.name = name

    def speak(self):
        print(f"{self.name} makes a sound.")

# 定义一个子类，继承自 Animal
class Dog(Animal):  #此时Dog类获得了Animal类的所有属性和方法
    def speak(self):
        print(f"{self.name} barks.")

# 创建 Dog 类的实例
dog = Dog("Buddy")
dog.speak()  # 输出: Buddy barks.
_____________________________________________________
#多继承（Multiple Inheritance）

# 定义两个父类
class Animal:
    def __init__(self, name):
        self.name = name

    def speak(self):
        print(f"{self.name} makes a sound.")

class Runner:
    def run(self):
        print(f"{self.name} runs fast.")

# 定义一个子类，同时继承 Animal 和 Runner
class Dog(Animal, Runner):
    def speak(self):
        print(f"{self.name} barks.")

# 创建 Dog 类的实例
dog = Dog("Buddy")
dog.speak()  # 输出: Buddy barks.
dog.run()    # 输出: Buddy runs fast.
```

**单继承**适用于简单的类层次结构，继承关系明确，易于管理。

**多继承**可以带来更强的灵活性和功能组合，但要小心类之间的复杂关系以及可能产生的命名冲突

### 重写

子类和父类具有同名的方法，子类方法会覆盖父类的实现。

子类可以通过 `super()` 调用被重写的父类方法。

重写的过程中，子类通常会保留父类的功能并增加新的行为，但也可以完全改变父类的方法逻辑

``` python
# 父类
class Animal:
    def __init__(self, name):
        self.name = name

    def speak(self):
        print(f"{self.name} makes a sound")

# 子类
class Dog(Animal):
    def __init__(self, name, breed): #重写构造方法,在重写后原父类的属性会被覆盖,需要重新调父类构造方法来初始化属性
        # 调用父类的构造方法，初始化 name 属性
        super().__init__(name) 
        # 初始化子类的属性
        self.breed = breed

    def speak(self): #重写父类方法
        super().speak()  # 调用父类的 speak 方法  #super().父类方法
        print(f"{self.name} is a {self.breed} and barks")

# 创建实例
dog = Dog("Buddy", "Golden Retriever")
dog.speak()

# 输出:
# Buddy makes a sound
# Buddy is a Golden Retriever and barks
```

### 多态

多态是面向对象编程中的一个重要概念，指的是不同的对象可以对同一个方法或操作作出不同的响应。换句话说，在多态中，**同样的接口，可以根据对象的类型，执行不同的行为**。

``` python
class Animal:
    def speak(self):
        return "Animal makes a sound"

class Dog(Animal):  #子类01
    def speak(self):
        return "Bark"

class Cat(Animal):  #子类02
    def speak(self):
        return "Meow"
    
#创建多态函数
#animal_sound() 函数接受 Animal 类的对象，并调用 speak() 方法
def animal_sound(animal):
    print(animal.speak())

# 创建对象
dog = Dog()  #实例化后即作为识别参数进入animal_sound() 函数中来决定执行哪个子类方法
cat = Cat()

# 调用相同的函数，传入不同的对象
animal_sound(dog)  # 输出: Bark
animal_sound(cat)  # 输出: Meow
```

### 运算符重载

在 Python 中，运算符本质上是特殊方法的另一种表示方式。例如，`+` 运算符对应的特殊方法是 `__add__()`，`-` 运算符对应的是 `__sub__()`，等等。通过重载这些特殊方法，我们可以自定义运算符在自定义对象中的行为。

~~(这B玩意改底层算法逻辑,看着都费劲,还容易和别的底层代码出现奇怪的耦合bug,我的评价是,不学!)~~

想要啥新算法自己写方法或者导库,别整这玩意

``` python
class Vector:
    def __init__(self, x, y):
        self.x = x
        self.y = y

    def __add__(self, other):
        # 重载 + 运算符，定义向量相加
        return Vector(self.x + other.x, self.y + other.y)

    def __sub__(self, other):
        # 重载 - 运算符，定义向量相减
        return Vector(self.x - other.x, self.y - other.y)

    def __eq__(self, other):
        # 重载 == 运算符，定义向量相等比较
        return self.x == other.x and self.y == other.y

    def __str__(self):
        # 重载 str() 函数，使对象可读性更强
        return f"Vector({self.x}, {self.y})"

# 创建向量对象
v1 = Vector(2, 3)
v2 = Vector(5, 7)

# 使用 + 和 - 运算符进行向量运算
v3 = v1 + v2
v4 = v1 - v2

# 输出结果
print(v3)  # Vector(7, 10)
print(v4)  # Vector(-3, -4)

# 比较两个向量是否相等
print(v1 == v2)  # False
```

下面是 Python 中一些常见的运算符及其对应的特殊方法：

| 运算符 | 特殊方法       |
| ------ | -------------- |
| `+`    | `__add__`      |
| `-`    | `__sub__`      |
| `*`    | `__mul__`      |
| `/`    | `__truediv__`  |
| `//`   | `__floordiv__` |
| `%`    | `__mod__`      |
| `**`   | `__pow__`      |
| `==`   | `__eq__`       |
| `!=`   | `__ne__`       |
| `>`    | `__gt__`       |
| `<`    | `__lt__`       |
| `>=`   | `__ge__`       |
| `<=`   | `__le__`       |

## 异常

出异常问GPT,这玩意总结了也没屌用

这里有个好东西[ChatGPT桌面版](https://github.com/lencx/chatgpt)


## Python常用库


{% btn regular::常用库速查::https://www.pythoncheatsheet.org/cheatsheet/basics::fa-solid fa-play-circle %}

{% btn regular::官方的包管理库::https://pypi.org/::fa-solid fa-play-circle %}

{% btn regular::官方提供的标准库文档::https://docs.python.org/3/library/::fa-solid fa-play-circle %}

{% btn regular::按用途类型筛选库::https://awesome-python.com/::fa-solid fa-play-circle %}