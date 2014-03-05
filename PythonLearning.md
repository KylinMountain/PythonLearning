
##for 循环
素数求解，素数就是除了自身和1能整除外的数，不包括0和1
```Python
>>> for n in range(2, 10):
...     for x in range(2, n):
...         if n % x == 0:
...             print(n, 'equals', x, '*', n//x)
...             break
...     else:
...         # loop fell through without finding a factor
...         print(n, 'is a prime number')
...
```

奇偶数求解，
```Python
>>> for num in range(2, 10):
...     if num % 2 == 0:
...         print("Found an even number", num)
...         continue
...     print("Found a number", num)
```
##pass 语句
pass 语句什么也不做。它用于那些语法上必须要有什么语句，但程序什么也不做的场合
这通常用于创建最小结构的类:
```Python
>>> class MyEmptyClass:
...     pass
...
```
pass 可以在创建新代码时用来做函数或控制体的占位符。可以让你在更抽象的级别上思考。
```Python
>>> def initlog(*args):
...     pass   # Remember to implement this!
...
```
##定义函数
定义一个具有边界的斐波那契数列，这个a, b = b ,a+b的语法真是令人惊叹
```
>>> def fib(n):    # write Fibonacci series up to n
...     """Print a Fibonacci series up to n."""
...     a, b = 0, 1
...     while a < n:
...         print(a, end=' ')
...         a, b = b, a+b
...     print()
...
```
>>> # Now call the function we just defined:
... fib(2000)
0 1 1 2 3 5 8 13 21 34 55 89 144 233 377 610 987 1597

def 定义一个函数，其后跟随函数的函数名括号和参数，一般函数体第一行写Doc String(生成项目文档)
函数调用生成一个局部变量表，变量引用首先在局部符号表中查找，然后是包含函数的局部符号表，然后是全局符号表，最后是内置名字表。函数内部一般无法对全局变量赋值。

##定义一个返回列表的斐波那契函数
```Python
def fib2(n):
	result = []
	a, b = 0, 1
	while a < n:
		result.append(a)
		a, b = b, a+b
	return result

```
## 函数默认参数值
```Python

def ask_ok(prompt, retries=4, complaint='Yes or no, please!'):
	while True:
		ok = input(prompt)
		if ok in ('y', 'ye', 'yes'):
			return True
		if ok in ('n', 'no', 'nop', 'nope'):
			return False
		retries = retries - 1
		if retries < 0:
			raise IOError('refusenik user')
		print(complaint)

```
调用时，可以ask_ok('Do you ') 或者ask_ok('Do you ', 2)或者ask_ok('Do you ',2 , 'Hurry Up’)

默认值只被赋值一次。这使得当默认值是可变对象时会有所不同，比如列表、字典或者大多数类的实例。例如，下面的函数在后续调用过程中会累积（前面）传给它的参数:
```
def f(a, L=[]):
	L.append(a)
	return L

print(f(1))
print(f(2))
print(f(3))
```
输出:
```
[1]
[1, 2]
[1, 2, 3]
```
解释：因为默认值只被赋值一次，意思是L对象是不可变的。所以每次append都会将元素添加到最初的L上，所以元素会增加

如果不想让默认值在后续调用中累计，可以将L的默认值设为None，接着在来一条语句判断是否为None，是就将L置[],比如：
```Python
def f(a, L = None):
	if L is None:
		L = []
	L.append(a)
	return L

```

##关键字参数
函数可以通过 关键字参数 的形式来调用，形如 keyword = value 
```Python
def parrot(voltage, state='a stiff', action='voom', type='Norwegian Blue'):
	print("-- This parrot wouldn't", action, end=' ')
	print("if you put", voltage, "volts through it.")
	print("-- Lovely plumage, the", type)
	print("-- It's", state, "!")
	
	#可以使用以下方式调用：
	parrot(voltage=1000000, action='VOOOOOM') 
	key = value方式，若使用关键字，就都得使用
```
引入一个形如 **name 的参数时，它接收一个字典（参见 typesmapping ） ，该字典包含了所有未出现在形式参数列表中的关键字参数。这里可能还会组合使用一个形如 *name （下一小节詳細介绍） 的形式参数，它接收一个元组（下一节中会详细介绍），包含了所有没有出现在形式参数列表中的参数值。（ *name 必须在 **name 之前出现）
示例：
```Python
def cheeseshop(kind, *arguments, **keywords):
    print("-- Do you have any", kind, "?")
    print("-- I'm sorry, we're all out of", kind)
    for arg in arguments:
        print(arg)
    print("-" * 40)
    keys = sorted(keywords.keys())
    for kw in keys:
        print(kw, ":", keywords[kw])

# 调用
cheeseshop("Limburger", "It's very runny, sir.",
           "It's really very, VERY runny, sir.",
           shopkeeper="Michael Palin",
           client="John Cleese",
           sketch="Cheese Shop Sketch")        
````

可以看出*arguments是除了第一个参数之后的非字典参数，字典参数使用关键字参数。
在打印关键字参数时，一定要**sort**，否则无序

## 变参数列表
就是上一节的一个* 的参数，该参数可以接任意个任意类型的参数，示例：
```Python
def write_multiple_items(file, separator, *args):
    file.write(separator.join(args))
```

##参数列表的拆分
加入 '*' 操作符来自动把参数列表拆开，比如：
```Python
>>> list(range(3, 6))            # normal call with separate arguments
[3, 4, 5]
>>> args = [3, 6]
>>> list(range(*args))            # call with arguments unpacked from a list
[3, 4, 5]
```

同样可以使用** 操作符将关键字参数分拆为字典，比如将顶一个字典变量，然后传入函数的，并加**

## lambda形式
用于定义匿名函数，例如：
```
lambda x: n+x
```
就会返回x与n的和

比如：
```
def make_increment(n):
	return lambda x: x+n
```
##文档字符串
```Python
>>> def my_function():
...     """Do nothing, but document it.
...
...     No, really, it doesn't do anything.
...     """
...     pass
...
>>> print(my_function.__doc__)
Do nothing, but document it.

    No, really, it doesn't do anything.
```

##编码风格

- 使用 4 空格缩进，而非 TAB。
- 在小缩进（可以嵌套更深）和大缩进（更易读）之间，4空格是一个很好的折中。TAB 引发了一些混乱，最好弃用。

- 折行以确保其不会超过 79 个字符。

- 这有助于小显示器用户阅读，也可以让大显示器能并排显示几个代码文件。

- 使用空行分隔函数和类，以及函数中的大块代码。

- 可能的话，注释独占一行

- 使用文档字符串

- 把空格放到操作符两边，以及逗号后面，但是括号里侧不加空格： a = f(1, 2) + g(3, 4) 。

- 统一函数和类命名。

- 推荐类名用 驼峰命名， 函数和方法名用 小写_和_下划线。总是用 self 作为方法的第一个参数（关于类和方法的知识详见 初识类 ）。

- 不要使用花哨的编码，如果你的代码的目的是要在国际化 环境。 Python的默认情况下，UTF-8，甚至普通的ASCII总是工作的最好。

- 同样，也不要使用非ASCII字符的标识符，除非是不同语种的会阅读或者维护代码。


##list 和 tuple

- list的元素以"[]"包围，元素长度可变，元素可赋值。

classmates = ['jack', 'Mike', 'Tom', 'Helen', 'Alice', 'Sarah']
classmates.append('Kylin')，插入到classmates末尾
classmates.insert(元素)，插入到末尾
classmates.insert(index, 元素)，插入到index位置的元素
classmate.pop()，默认弹出最后最后一个元素
classmates.pop(index)，弹出索引为index的元素
list中元素类型不固定

- tuple元组，用"()"包围，元素不可变，只可访问不可更改。

如果可能，能用tuple代替list就尽量用tuple。

Tips
> t = (1)

定义的不是tuple，是1这个数！这是因为括号()既可以表示tuple，又可以表示数学公式中的小括号，这就产生了歧义，因此，Python规定，这种情况下，按小括号进行计算，计算结果自然是1
所以，只有1个元素的tuple定义时必须加一个逗号,，来消除歧义
> t = (1,)

tuple的元素不可变指的是tuple的每个元素，指向永远不变。所以tuple中包含list元素时，list是可变的，但是tuple指向还是那个list，还是那个指针。

##心得
变量本身类型不固定的语言称之为动态语言，与之对应的就是Java或C这类的静态语言。
在Python中同一个变量指向的对象类型可以变化，从整型，字符串到列表等都可以使用同一个变量。
变量中存储的只是指向该对象的指针，所以变量可以赋值任意类型的变量，因为变量只是重新指向另外一个指针。
所以当tuple的元素固定之后，tuple指向每个元素的指针是不会变的，当时有些元素本身是可变的，比如list
所以在tuple中存在可变元素后，这个tuple就不再不可变了，也不再安全了。
最终就是所谓的“指向不变”

##问题
我在Python3.3中运行
```Python
sum = 0

for x in range(101):

	sum = sum + x

print(sum)
```
提示无效的语法, for语句后面的print(sum)，只要与for的缩进一样，就会出错，提示invalid syntax。去掉print，直接运行，然后打印，就没问题。

另外，我又测试打印任意的字符串都报错。

## Dict
Python内置字典，简单说就是键值对，在Java就是Map集合
```
d = {'Michael': 95, 'Bob': 75, 'Tracy': 85}

#赋值
d['Adam'] = 99
#取值
d['Adam']
#判断有无该键值，返回True or False
'Adam' in d
# get值
d.get('Adam')	# 没有该键对应的值，返回None
d.get('Adam', -1)	#没有该键值对应的值，返回默认值-1，该值可自定义
#删除一个key
d.pop(key)

```
通过对**d['Adam']**和**d.pop(key)**可以发现，Dict内部对于键值对是没有按照添加顺序或者其他的条件进行排序的

Tips
> 和list比较，dict有以下几个特点：
查找和插入的速度极快，不会随着key的增加而增加；
需要占用大量的内存，内存浪费多。
而list相反：
查找和插入的时间随着元素的增加而增加；
占用空间小，浪费内存很少。
所以，dict是用空间来换取时间的一种方法。

dict根据key计算value的存储位置，通过key计算位置的算法就是哈希算法（hash）
key是不可变元素，比如整型和字符串。

set是一个key的集合，不能重复。要新建一个set，那么需要一个list作为输入。
```
#传入一个list作为set的集合
s = set([1, 2, 3])
#set会自动过滤掉集合中重复的key
s = set([1,2,3,5,5,5,5])
#只会返回{1，2，3，5}
#添加元素
s.add(key)
# 删除元素
s.remove(key)
````
set可以看成数学意义上的无序和无重复元素的集合，因此，两个set可以做数学意义上的交集、并集等操作.








