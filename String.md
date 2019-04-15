#### String

- **两种新建方法，存储位置**
  
	- 通过new新建的存储在堆上
   
		String heap1 = new String("heap");

	- 不通过new新建的存在常量池

		String constantArea1 = "constantArea";

	- 编码验证
	```
	private static void testStorLocation(){

		//在堆上声明
		String heap1 = new String("heap");
		String heap2 = new String("heap");

		//在常量池声明
		String constantArea1 = "constantArea";
		String constantArea2 = "constantArea";

		//String重写过hashCode，String的值一样则hashCode一样
		System.out.println(System.identityHashCode(heap1));
		System.out.println(System.identityHashCode(heap2));
		System.out.println(System.identityHashCode(constantArea1));
		System.out.println(System.identityHashCode(constantArea2));
	}
	```
	```
	Begin test [testStorLocation]
	10568834  //new申请地址不同
	21029277
	24324022  //非new申请地址相同
	24324022
	```

- **长度 Length()**
  - length 等于Unicode字符的数量
  - String实际存储为final char[]类型，char类型为Unicode,长度为2个Byte.
关于Unicode：Unicode 只是一个符号集，**它只规定了符号的二进制代码(它就是个取值，其他类似UTF-8是编码格式)**，却没有规定这个二进制代码应该如何存储。
[更多相关Unicode请参考](https://blog.csdn.net/Deft_MKJing/article/details/79460485)


	```
		private static void length(){
			String test = "test1";

			System.out.println("Ori is " + test);
			System.out.println("Length  = " + test.length());


			String testChinese = "中文";
			System.out.println("Ori is " + testChinese);
			System.out.println("Length Chinese = " + testChinese.length());
		}
	```
	```
			Ori is test1
			Length  = 5
			Ori is 中文
			Length Chinese = 2
	```
- 比较 equals() compareTo()
	- equals判断是否相等，compareTo还能判断大小。
	```
	private static void equalsAndCompareTo() {
		String test1 = "test1";
		String test2 = "test2";
		System.out.println("Ori test1 is " + test1);
		System.out.println("Ori test2 is " + test2);

		// equals 只判断是否相等， compareTo能判断大小，返回INT型
		System.out.println("equls = " + test1.equals(test2));
		System.out.println("compareTo = " + test1.compareTo(test2));
	}
	```
	```
	Ori test1 is test1
	Ori test2 is test2
	equls = false
	compareTo = -1
	```
- 取字符 charAt()
- 大小写转换 toUpperCase() toLowerCase
- 连接 concat()
- 判断开头 startWith()  endWith()
- 模式匹配(获取某个字符或字符串首次出现的位置) indexOf()  lastIndexOf()
- 子串 substring()
- 修建左右空白 trim()
- 替换 replace() replaceAll()
- 拆分 split()


