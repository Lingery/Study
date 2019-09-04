# 06-Java常用API

[TOC]

## API概述

API(Application Programming Interface) : 应用程序编程接口

Java API就是Java提供给我们使用的类，这些类将底层的实现封装了起来，我们不需要关心这些类是如何实现的，只需要学习这些类如何使用。
我们可以通过查帮助文档来了解Java提供的API如何使用

### API的使用

```
A:打开帮助文档
B:点击显示，找到索引，看到输入框
C:你要学习什么内容，你就在框框里面输入什么内容
	  举例：Random
D:看包
java.lang包下的类在使用的时候是不需要导包的
E:看类的描述
	Random类是用于生成随机数的类
F:看构造方法
	Random():无参构造方法
	Random r = new Random();
G:看成员方法
	   public int nextInt(int n):产生的是一个[0,n)范围内的随机数
		调用方法：
			看返回值类型：人家返回什么类型，你就用什么类型接收
			看方法名：名字不要写错了
			看形式参数：人家要几个参数，你就给几个，人家要什么数据类型的，你就给什么数据类型的
			int number = r.nextInt(100);
```

### Scanner类

用Scanner类的方法可以完成接收键盘录入的数据(基本数据类型，字符串数据)

1. 导包(位置放到class定义的上面)
	- A:手动导包
	
 			import java.util.Scanner;

	- B:鼠标点击红色叉叉，自动生成
	
	- C:快捷键(推荐)
	
 			ctrl+shift+o

2. 创建对象

		Scanner sc = new Scanner(System.in);

3. 接收数据

		int x = sc.nextInt();

注意：在程序的不同的地方创建多个scanner对象读取一整行信息，每次用完后调用close方法关掉，当第二个scanner对象调用nextLine时就会出现NoSuchElementException: No line found的异常。
如果第一个scanner对象不关掉，就不会报错。

public void close()关闭此扫描器，sc.close()会把System.in也关掉 
如果此扫描器尚未关闭，并且其底层 readable 也实现 Closeable 接口，则该 readable 的 close 方法将被调用。
System.in是InputStream的对象,并且关掉之后不能再打开

Java 是顺序执行的，执行到.close() 后就代表你关闭了流，再去调用已经被你关闭的流显然是不现实的

可以专门写一个类：

	class input
	{
    	final static Scanner sc=new Scanner(System.in);
	}

以后每次都调用input.sc，最后再把它关掉。

### Random类

用于产生一个随机数

-	使用步骤(和Scanner类似)
	1. 导包
	
			import java.util.Random;
	2. 创建对象
	
			Random r = new Random();

	3. 获取随机数
	
			int number = r.nextInt(10);

	- 产生的数据在0到10之间，包括0，不包括10。
	- 括号里面的10是可以变化的，如果是100，就是0-100之间的数据

### String类

在实际开发中，字符串的操作是最常见的操作，没有之一。
Java没有内置的字符串类型，所以，就在Java类库中提供了一个类String 供我们来使用。
String 类代表字符串。Java 程序中的所有字符串字面值（如 "abc" ）都作为此类的实例实现。

注意：String s = “helloworld”;s也是一个对象。

String 是 java.lang 包下的一个类，是一种引用数据类型（类，接口，数组）。字符串是常量；它们的值在创建之后不能更改。字符串缓冲区支持可变的字符串。因为 String 对象是不可变的，所以可以共享。

根据JDK的源码：
```
public final class String    
	implements java.io.Serializable, Comparable<String>, CharSequence {    
	/** The value is used for character storage. */  
	private final char value[];
```
字符串常量String就是一个char数组，内部封装了一个final修饰的char数组，并且String中所有方法的实现都是对char数组的改变。

#### String对象初始化

String类常用的构造方法有以下三种：

```
String(String original)://把字符串数据封装成字符串对象
String(char[] value)://把字符数组的数据封装成字符串对象
String(char[] value, int index, int count)://把字符数组中的一部分数据封装成字符串对象
```

还可以直接把一个字符串赋值给String类型的变量进行初始化：

	String s4 = "hello";

#### String的特别之处

字符串是一种比较特殊的引用数据类型，直接输出字符串对象输出的是该对象中的数据（其他对象直接输出的是该对象的地址值）。 
另外，为了便于字符串常量的共享和复用，在方法区中有一个字符串常量池专门用来存放字符串。

通过构造方法创建与直接赋值创建的字符串对象有什么不同呢？请看下图：

![字符串对象构造方法创建和直接赋值的区别](./images/06/01String.png)

	==:
	基本数据类型：比较的是基本数据类型的值是否相同
	引用数据类型：比较的是引用数据类型的地址值是否相同

三个字符串存储的都是同一个字符串"hello"，但是s1和s2、s3所指向的地址是不同的。String s2 = "hello"; 和 String s3 = "hello"; 都在编译期间生成了字面常量和符号引用，运行期间字面常量 "hello" 被存储在运行时常量池（当然只保存了一份）。通过这种方式来将 String 对象跟引用绑定的话，JVM 执行引擎会先在运行时常量池查找是否存在相同的字面常量，如果存在，则直接将引用指向已经存在的字面常量；否则在运行时常量池开辟一个空间来存储该字面常量，并将引用指向该字面常量。　
　
而通过 new 关键字来生成对象是在堆区进行的，而在堆区进行对象生成的过程是不会去检测该对象是否已经存在的。因此通过 new 来创建对象，创建出的一定是不同的对象，即使字符串的内容是相同的。但是对于相同的字符串常量，它们最终所指向的都是常量池中的同一个字符串。

#### String类的判断功能

	boolean equals(Object obj):比较字符串的内容是否相同
		Object:是类层次结构中的根类，所有的类都直接或者间接的继承自该类。
		如果一个方法的形式参数是Object，那么这里我们就可以传递它的任意的子类对象。
	boolean equalsIgnoreCase(String str):比较字符串的内容是否相同,忽略大小写
	boolean startsWith(String str):判断字符串对象是否以指定的str开头
	boolean endsWith(String str):判断字符串对象是否以指定的str结尾

#### String类的获取功能：

	int length():获取字符串的长度，其实也就是字符个数
	char charAt(int index):获取指定索引处的字符
	int indexOf(String str):获取str在字符串对象中第一次出现的索引
	String substring(int start):从start开始截取字符串
	String substring(int start,int end):从start开始，到end结束截取字符串。包括start，不包括end
	
#### String类的转换功能

	char[] toCharArray():把字符串转换为字符数组
	String toLowerCase():把字符串转换为小写字符串
	String toUpperCase():把字符串转换为大写字符串

字符串的遍历：
 * length()加上charAt()
 * 把字符串转换为字符数组，然后遍历数组

#### 字符串分割

String[] split(String regex)根据给定正则表达式的匹配拆分此字符串
String[] split(String regex, int limit)根据匹配给定的正则表达式来拆分此字符串


#### String类的其他常用功能

- 去除字符串两端空格	

		String trim()

- 按照指定符号分割字符串	

		String[] split(String str)

### StringBuilder类

StringBuilder:是一个可变的字符串，是字符串缓冲区类。  

#### String和StringBuilder的区别

- String的内容是固定的
- StringBuilder的内容是可变的

+=拼接字符串每次拼接都会产生新的字符串对象,而利用StringBuilder来拼接字符串自始至终用的都是同一个StringBuilder容器

![](./images/06/02StringBuilder.png)

#### StringBuilder类的常用方法

```
 A:构造方法:
    StringBuilder()
  B:成员方法:
    public int capacity():返回当前容量 (理论值)
    public int length():返回长度(已经存储的字符个数)
	public StringBuilder append(任意类型):添加数据，并返回自身对象
	public StringBuilder reverse():反转功能
```

#### StringBuilder和String的相互转换

StringBuilder -- String
public String toString():通过toString()就可以实现把StringBuilder转成String

String -- StringBuilder
StringBuilder(String str):通过构造方法就可以实现把String转成StringBuilder

## Java集合

### 对象数组

A:基本类型的数组:存储的元素为基本类型

	int[] arr={1,2,3,4}

B:对象数组:存储的元素为引用类型

	Student[] stus=new Student[3];
	Student代表一个自定义类
	stus数组中stus[0],stus[1],stus[2]的元素数据类型为Student,都可以指向一个Student对象

![对象数组的内存图](./images/06/03ObjectArray.png)

### ArrayList类

A:我们学习的是面向对象编程语言，而面向对象编程语言对事物的描述都是通过对象来体现的。
为了方便对多个对象进行操作，我们就必须对这多个对象进行存储，而要想对多个对象进行存储，	就不能是一个基本的变量，而应该是一个容器类型的变量。
 	  
B:到目前为止，我们学习过了哪些容器类型的数据呢？
StringBuilder,数组。
StringBuilder的结果只能是一个字符串类型，不一定满足我们的需求。
所以，我们目前只能选择数组了，也就是我们前面学习过的对象数组。
但是，数组的长度是固定的， 如果有时候元素的个数不确定的,我们无法定义出数组的长度,这个时候，java就提供了集合类供我们使用。

集合类的特点：长度可变。

ArrayList&lt;E&gt;:大小可变数组的实现，&lt;E&gt;是一种特殊的数据类型，泛型,在出现E的地方我们使用引用数据类型替换即可

	举例：ArrayList<String>,ArrayList<Student>

构造方法

	ArrayList()

成员方法

```
添加元素
	public boolean add(E e):添加元素
	public void add(int index,E element):在指定的索引处添加一个元素
获取元素
    public E get(int index):返回指定索引处的元素
集合长度
	 public int size():返回集合中的元素的个数
删除元素
	 public boolean remove(Object o):删除指定的元素，返回删除是否成功
    public E remove(int index):删除指定索引处的元素，返回被删除的元素
修改元素
	public E set(int index,E element):修改指定索引处的元素，返回被修改的元素
```

ArrayList集合的遍历:集合的遍历思想和数组的遍历思想相同,循环遍历容器,依次取出里面的元素即可,通过size()和get()配合实现

## I/O流

IO流用来处理设备之间的数据传输
Java对数据的操作是通过流的方式
Java用于操作流的类都在IO包中
流按流向分为两种：输入流，输出流

![流](./images/06/04Stream.png)

### FileWriter类

#### FileWriter向文件中写数据

```
A:FileWriter向文件中写数据操作步骤:
      a:使用FileWriter流关联文件
      b:利用FileWriter的写方法写数据
      c:利用FileWriter的刷新方法将数据从内存刷到硬盘上
      d:利用FileWriter的关流方法将释放占用的系统底层资源
   B:FileWriter方法:
构造方法
FileWriter(String fileName) 传入一个文件的路径（包括名称）
成员方法
void write(String str) 向文件中写str
void flush()  将内存中的数据刷新到文件中
void close()  关流释放系统底层资源
```

```
//创建输出流对象
		FileWriter fw = new FileWriter("d:\\a.txt");
/*
		 * 创建输出流对象做了哪些事情:
		 * 		A:调用系统资源创建了一个文件
		 * 		B:创建输出流对象
		 * 		C:把输出流对象指向文件
		 */
		
		//调用输出流对象的写数据的方法
		//写一个字符串数据
		fw.write("IO流你好");
		//数据没有直接写到文件，其实是写到了内存缓冲区
		fw.flush();
		
		//释放资源
		//通知系统释放和该文件相关的资源
		fw.close();
```

输出流写数据的步骤：
* A:创建输出流对象
* B:调用输出流对象的写数据方法，并刷新缓冲区
* C:释放资源
 		
相对路径：相对当前项目而言的，在项目的根目录下(a.txt)
绝对路径：以盘符开始的路径(d:\\a.txt)

close()和flush()方法的区别：
 * 	flush():刷新缓冲区。流对象还可以继续使用。
 * 	close():先刷新缓冲区，然后通知系统释放资源。流对象不可以再被使用了。

#### FileWriter其它写方法

void write(String str):写一个字符串数据
void write(String str,int index,int len):写一个字符串中的一部分数据
void write(int ch):写一个字符数据,这里写int类型的好处是既可以写char类型的数据，也可以写char对应的int类型的值。'a',97
void write(char[] chs):写一个字符数组数据
void write(char[] chs,int index,int len):写一个字符数组的一部分数据

#### FileWriter写入换行以及向文本末尾追加

\n可以实现换行，但是windows系统自带的记事本打开并没有换行，这是为什么呢?因为windows识别的换行不是\n，而是\r\n
* 	windows:\r\n
* 	linux:\n
* 	mac:\r
 	
如何实现数据的追加写入?

	FileWriter(String fileName, boolean append)

### FileReader类

FileReader(String fileName):传递文件名称

输入流读文件的步骤：
A:创建输入流对象

	FileReader fr = new FileReader("fr.txt");

B:调用输入流对象的读数据方法

	int read():一次读取一个字符

如果读取数据的返回值是-1的时候，就说明没有数据了，可以作为循环的结束条件

```
int ch;
		1:fr.read()
		2:ch=fr.read()
		3:ch != -1
		while((ch=fr.read())!=-1) {
			System.out.println(ch);
			System.out.println((char)ch);
			System.out.print((char)ch);
		}
```
	
C:释放资源

	fr.close();

java.io.FileNotFoundException: fr.txt (系统找不到指定的文件。)

#### FileReader其他读方法

read(char[] cbuf) 将字符读入数组
read(char[] cbuf, int off, int len)将字符读入数组的某一部分
read(CharBuffer target) 试图将字符读入指定的字符缓冲区

#### 复制文件

	int ch;
	while((ch=fr.read())!=-1) {
		fw.write(ch);
	}//一次读写一个字符

	//用字符数组拷贝文件
	char[] chs = new char[1024];
	int len;
	while((len=fr.read(chs))!=-1) {
		fw.write(chs, 0, len);
	}

![复制文件图解](./images/06/05CopyFile.png)

### 字符缓冲流

BufferedWriter:将文本写入字符输出流，缓冲各个字符，从而提供单个字符、数组和字符串的高效写入

	BufferedWriter bw = new BufferedWriter(new FileWriter("bw.txt"));

BufferedReader:从字符输入流中读取文本，缓冲各个字符，从而实现字符、数组和行的高效读取

	BufferedReader br = new BufferedReader(new FileReader("FileWriterDemo.java"));

#### 缓冲流的特有方法

```
BufferedWriter
 	void newLine():写一个换行符，这个换行符由系统决定,不同的操作系统newLine()方法使用的换行符不同
windows:\r\n 
linux:\n 
mac:\r
BufferedReader
 	String readLine():一次读取一行数据，但是不读取换行符

	String line;
	while((line=br.readLine())!=null) {
		array.add(line);
	}

```


