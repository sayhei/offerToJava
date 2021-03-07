## 1. JDK 和 JRE 有什么区别？ 
- JDK：Java Development Kit 的简称，Java 开发工具包，提供了 Java 的开发环境和运行环境。 
- JRE：Java Runtime Environment 的简称，Java 运行环境，为 Java 的运行提供了所需环境。 具体来说 JDK 其实包含了 JRE，同时还包含了编译 Java 源码的编译器 Javac，还包含了很多 Java 程序调试和分析的工具。简单来说：如果你需要运行 Java 程序，只需安装 JRE 就可以了，如果你需要编写 Java 程序，需要安装 JDK。 

2. == 和 equals 的区别是什么？ 
对于基本类型和引用类型 == 的作用效果是不同的，
如下所示： 
	基本类型：比较的是值是否相同； 
	引用类型：比较的是引用是否相同；
代码示例：
	String x =“string”;
	String y =“string”;
	String z = new String(“string”);
	System.out.println(x==y); // true
	System.out.println(x==z); // false
	System.out.println(x.equals(y)); // true
	System.out.println(x.equals(z)); // true
	代码解读：因为 x和  y指向的是同一个引用，所以  ==也是  true，而 new String()方法则重写开辟了
	内存空间，所以 ==结果为  false，而 equals比较的一直是值，所以结果都为  true。
	equals解读
	equals本质上就是  ==，只不过 String和  Integer等重写了  equals方法，把它变成了值比较。看下面的代码就明白了。
	首先来看默认情况下 equals比较一个有相同值的对象，代码如下：
	class Cat {
		public Cat(String name){
			this.name=name;
		}
		private String name;
		public String getName(){
			return name;
		}
		public void setName(String name){
			this.name=name;
		}
	}
	Cat c1=new Cat("王磊");
	Cat c2=new Cat("王磊");
	System.out.println(s1.equales(s2));
	同样的，当我们进入String的equals方法，找到了答案，代码如下：
	public boolean equals(Object anObject){
		if(this == anObject){
			return true;
		}
		if(anObject instanceof String){
			String anotherString = (String)anObject;
			int n=value.length;
			if (n == anotherString.value.length){
				char v1[] = value;
				char v2[] = anotherString.value;
				int i =0;
				while (n-- != ){
					if (v1[i] != 0){
						return false;
						i++;
					}
					return true;
				}
			}
		return false;
	}
	原来是String重写了Object 的equals方法，把引用比较改成了值比较。
	总结：==对于基本类型来说是值比较，对于引用类型来说是比较的是引用：而equals默认情况下是引用比较，只是很多类重写了equals方法，比如String,Integer等把它变成了值比较，所以一般情况下equals比较的是值是否相等.

3.两个对象的hashCode()相同,则equals() 也不一定为true，对吗？
	不对，来干嘛个对象的hashCode()相同，equals()不一定为true;
	代码示例：
	String str1="通话";
	String str2="重地";
	System.out.println(String.format("str1: %d | str2: %d",str1.hashCode(),str2.hashCode()));
	System.out.println(str1.equals());
	执行的结果：
	str1:1179395 |str2:1179395
	false
	代码解读：很显然“通话”和“重地”的hashCode()相同，然而equals()则为false,因为在散列表中,hashCode()相等即两个键值对的哈希值相等，然而哈希值相等，不一定得出键值对相等。

	4.final在java中有什么作用？
	final 修饰的类叫最终类，该类不能被继承。
	final 修饰的方法不能被重写。
	final 修饰的变量叫常量，常量必须初始化，初始化值得的值就不能被修改
	
	5.jAVA 中的Math.round(-1,5)等于多少？
	等于 -1,Math.round四舍五入大于0.5向上取整的.

	6.String属于基础数据类型吗？
	String不属于基础类型，基础类型有8种：byte,short,int,long,float,double,char,boolean.而String属于对象.

	7.Java种操作字符串都有哪些类？它们之间有什么区别？
	操作字符串的类有：String、StringBuffer、StringBuilder.

	String和StringBuffer、StringBuilder的区别在于String声明的是不可变的对象，每次操作都会生成新的String对象，然后将指针指向新的String对象，而StringBuffer,StringBuilder可以在远对象的基础上进行操作,所以在经常改变字符串内容的情况下最好不要使用String.

	StringBuffer与StringBuilder的最大区别在于，StringBuffer是线程安全的，而StringBuilder是非线程安全的,但StringBuilder的性能却高于StringBuilder，所以在但线程环境下推荐使用StringBuilder，多线程环境下使用StringBuffer.

	8. String str="i"与String str = new String("i)一样嘛;
	不一样，因为内存分配的方式不一样，String str="i"的方式，Java虚拟机会将其分配到常量池中；而String str=new String("i")则会被分配到堆内存中。

	9. 如何将字符串反转？
	使用StringBuilder或者StringBuffer的reverse()方法。

	10. String类的常用方法有哪些？
	indexOf():返回指定字符的索引.
	charAt():返回指定索引的字符。
	replace():字符串替换。
	trim():去掉字符串两端空白。
	split():分割字符串，返回一个分割后的字符串数组。
	getBytes():返回字符串的byte类型数组。
	length():返回字符串长度。
	toLowerCase():将字符串转成小写字母。
	toUpperCase():将字符串转成大写字母。
	substring():截取字符串。
	equals():字符串比较。

	11.抽象类必须要有抽象方法吗？
	不需要，抽象类不一定非要抽象方法。

	12.普通类和抽象类有哪些区别？
	普通类不能包含抽象方法，抽象类可以包含抽象方法。
	抽象类不能直接实例化，普通类可以直接实例化。

	13.抽象类能使用final修饰吗？
	不能，定义抽象类就是让其他类继承的，如果定义为final该类就不能被继承，这样彼此就会产生矛盾，所以final不能修饰抽象类。

	14.接口和抽象类有什么区别？
	默认方法实现：抽象类可以有默认的方法实现，接口不能有默认的方法实现。
	实现：抽象类的子类使用extends来继承，接口必须使用implements来实现接口。
	构造函数：抽象类可以有构造函数，接口不能有。
	main方法：抽象类可以有main方法，并且我们能够运行它，接口不能有main方法。

	15.java中io流分为几种？
	按功能分：输入流、输出流
	按类型来分：字节流、字符流
	字节流和字符流的区别是：字节流按8位传输以字节为单位输入输出数据，字符流按16位传输以字符为单位的输入输出数据。

	16.BIO、NIO、AIO有什么区别
	BIO：Block IO同步阻塞式IO，就是我们平常使用的传统IO，它的特点就是模式简单使用方便，并发能力低。
	NIO：New IO同步非阻塞IO，是传统IO的升级，客户端和服务器端通过Channel（通道）通讯，实现多路复用。
	AIO：Asynchronous IO是NIO的升级，也叫NIO2，实现了异步非阻塞IO，异步IO的操作基于事件和回调机制。

	17.Files的常用方法都有哪些？
	Files.exist(): 检测文件路径是否存在。
	Files.createFile():创建文件。
	Files.createDirectory():创建文件夹。
	Files.delete():删除一个文件或目录。
	Files.copy():复制文件。
	Files.move():移动文件。
	Files.size():查看文件个数。
	Files.read():读取文件。
	Files.write():写入文件。

	
