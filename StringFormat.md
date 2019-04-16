## String.format

`%[argument_index$][flags][width][.precision]conversion`

### argument_index

- 指定第n个变量进行格式化

- 依次支持一个变量、多个格式的格式化操作

  ```Java
  Calendar c = new GregorianCalendar(1995, MAY, 23);
  String s = String.format("Duke's Birthday: %1$tb %1$te, %1$tY", c);
  // -> s == "Duke's Birthday: May 23, 1995"
  ```

### flags

**flags是可选参数，用于控制输出的格式，比如左对齐、金额用逗号隔开。**

- '-' 在最小宽度内左对齐，不可以与“用0填充”同时使用

- '+' 结果包含正负号

- ' ' 正值前加空格，负值前加负号

- '0' 结果用0填充

- ',' 每3位用逗号分隔

- '(' 若参数是负数，用括号把数字括起来。

  ```java
          System.out.println(String.format("%-5d", 2));
          System.out.println(String.format("%+5d", -2));
          System.out.println(String.format("% 5d", -2));
          System.out.println(String.format("%05d", -2));
          System.out.println(String.format("%,5d", -2000));
          System.out.println(String.format("%,(5d", -2000));
  
  ```

  

   **结果：**

  ```java
  2    
     -2
     -2
  -0002
  -2,000
  (2,000)
  
  ```

### width

- width是可选参数，用于控制输出的宽度

  ```java
  System.out.println(String.format("%5d", 2));     
  //    2
  ```

### precision

- precision是可选参数，用来限定输出的精度，用于浮点数

- 不可用于整数，会抛异常 *IllegalFormatPrecisionException*

  ```Java
  System.out.println(String.format("%.2f", 1.2));
  //1.20
  ```

  

### conversion

代表转换规格，可分为几类：

1. 通用

2. char类型转换

3. 整数、浮点数的转换

4. Date/Time

5. %%转义

6. 分行负号 %n 等同于 \n

   这里转几个常用的，[详情可查看](https://www.cnblogs.com/travellife/p/Java-zi-fu-chuan-ge-shi-hua-xiang-jie.html)和JavaDoc

```
'b':将参数格式化为boolean类型输出，'B'的效果相同,但结果中字母为大写。false
'h':将参数格式化为散列输出，原理：Integer.toHexString(arg.hashCode())，'H'的效果相同,但结果中字母为大写。fc42
's':将参数格式化为字符串输出，如果参数实现了 Formattable接口，则调用 formatTo方法。'S'的效果相同。16
FormatImpl类实现了Formattable接口：我是Formattable接口的实现类
'c':将参数格式化为Unicode字符，'C'的效果相同。A
'd':将参数格式化为十进制整数。11
'o':将参数格式化为八进制整数。11
'x':将参数格式化为十六进制整数。11
'e':将参数格式化为科学计数法的浮点数，'E'的效果相同。1.000000E+01
'f':将参数格式化为十进制浮点数。10.000001
'g':根据具体情况，自动选择用普通表示方式还是科学计数法方式，'G'效果相同。10.01=10.0100
'g':根据具体情况，自动选择用普通表示方式还是科学计数法方式，'G'效果相同。10.00000000005=10.0000
'a':结果被格式化为带有效位数和指数的十六进制浮点数，'A'效果相同,但结果中字母为大写。0x1.4333333333333p3
't':时间日期格式化前缀，会在后面讲述
'%':输出%。%
'n':平台独立的行分隔符。System.getProperty("line.separator")可以取得平台独立的行分隔符，但是用在format中间未免显得过于烦琐了
已经换行
```









