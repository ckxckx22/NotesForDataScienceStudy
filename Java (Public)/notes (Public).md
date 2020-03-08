## 1. 第一个程序 与 用变量做计算
### 1.1 第一个程序
* Java传统是首字母大写.  
* 用control+/打开补全（联想）.  
* console是程序运行的地方.  
* 每句话结尾用分号结尾(insert ; to complete BlockStatement).  
* `Command` + `/` to commentize a line (or multiple line if multiple line are selected)   
* `println`: print words + /n    
* `+`: when used in `println`, will make the value into strings and then connect strings and then print  
* `nextInt()`：输入一个整数，如果没输入整数会报错exception: mismatch
* <b>`Scanner in = new Scanner(System.in)` 输入</b>  
```Java
import java.util.Scanner; // This is automatically generated when I clicked util - Scanner

public class hello2 {

	public static void main(String[] args) {
		// TODO Auto-generated method stub

		System.out.println("Hello"); 
		Scanner in = new Scanner(System.in); //read input of user as "in"
		System.out.println("echo:" + in.nextLine()); // `+` to connect words; next Line `in` 
		
		System.out.println("2+3=" + (2+3)); //(2+3) must be within parenthis
		
		Scanner in = new Scanner(System.in); //read input of user as "in". We will enter 23 here. 
		System.out.println("100-23=" + (100-in.nextInt())); // next "in" as Integer. 
		System.out.println("100-"+ in.nextInt() + "=" + (100-in.nextInt())); //Not work as we want. This requires us to enter a number twice. 
	}

}
```

### 1.2 用变量做计算
* 变量的名字是一种标识符：字母、数字、下划线  
* `int price=0`。 <u>Java是强类型的语言，必须定义变量，必须定义类型，类型不可改变</u>  
* 若变量没有被赋值，不可应用它。 每一个变量都必须有单独都赋值。推荐用一行赋值一个变量 eg `int price = 0, amount = 0;`  
* 常量 `final int amount2 = 100` 之后就不能再改动amount2的值  
例子： 输入两个数，做减法  
```java
import java.util.Scanner; // This is automatically generated when I clicked util - Scanner

public class hello2 {

	public static void main(String[] args) {
		//instead, use a variable to refer to the input 
        Scanner in = new Scanner(System.in); //read input of user as "in"
		//赋值
		int price = 0;
		int amount = 100;
		System.out.print("Please enter amount: ");
		amount = in.nextInt();
		System.out.print("Please enter price: ");
		price = in.nextInt();
		System.out.println(amount+"-"+price+"="+(amount-price));
		
	}

}
```

## 2. 比较 与 判断 
### 2.1 浮点数double 和整数  
* <u>10和10.0在Java中是完全不同的数，后者是浮点。</u>  
* <u>两个integer做除法只能得到integer</u>, eg 10/3 = 3 (instead of 3.33333)，只要其中一个不是int得出的结果就是float, eg 10/3.0 = 3.3333  
* 整数可以做精确的运算，而且运算比较快、占地方小。浮点是有误差的，比如`0.1+0.1+0.1+0.1+0.1+0.1+0.1+0.1+0.1+0.1` != 1    
例子：将英制长度转换为国际通用长度  
```java
import java.util.Scanner; 

public class hello2 {

	public static void main(String[] args) {
		// TODO Auto-generated method stub
		int foot;
		double inch;
		Scanner in = new Scanner(System.in);
		foot = in.nextInt();
		inch = in.nextInt(); //可以读取整数，交给double. 这里也可以用in.nextDouble()
		System.out.println("foot="+foot+", inch="+inch);
		System.out.println((foot+inch/12)*0.3048);
	}

}
```
#### 强制类型转换
* double to int: `int ...` eg:`double b = 10.3; int a = (int)b`  
* int to dbl can be done automatically  


### 2.2 优先级  
* 运算符: `%`取余数  
* 单目的运算符优先级最高,比如取相反数`3*-2`  
* 结合关系： 赋值是从右到左 eg`result = a = b = 3+c`  
* 关系运算符比算术运算符低，但是比赋值高。  
* 判断是否相等的`==`和`!=`比其他的低；连续的关系运算是从左到右进行的. `a==b==true`,(wrong!)`a==b==6`,`true==a>b`  


### 2.3 判断 if语句
```java
if (x > y)
    max = x;
else 
    max = y;
```
* debug: 用step over 一行一行的运行

#### 嵌套和级联的判断
* 嵌套：有多个if...else...; 级连：if... else if ...
* 在没有`{}`的情况下，else总是和最近的if匹配（与缩进无关）。建议总是加上`{}`.  
* 建议单一出口（即在语句的最后统一print，而非在每一个嵌套中都有一个print）  

#### 常见错误的解决方案
* 永远在if和else后面加上大括号。括号后面最好锁进一个tab  
* if那一行，括号后面不加分号  
* 比较相等，用“==“（两个等号）

### 2.4 多路分支switch-case  
```java
switch( 控制表达式 ){
    case 常量：
        语句
        ...
    case 常量：
        语句
        ...
    default：
        语句
        ....
}
```
* 控制表达式只能是整数型的结果  
* 常量可以是常数，也可以是常数计算的表达式  
* 根据表达式的结果，寻找匹配的case，并执行case后面的语句，一直到break为止 
* 如果所有的case都不匹配，那么就执行default后面的语句；如果没有default，就什么都不做   
```java
import java.util.Scanner; 

public class hello2 {

	public static void main(String[] args) {
		Scanner in = new Scanner(System.in);
		int type = in.nextInt();
		switch (type) {
		case 1: //if 1, will do nothing and then perform 2 until break
		case 2:
			System.out.println("Hello"); // if 2, will print "Hello" and then break
			break;
		case 3:
			System.out.println("Good evening"); // if 3, will print "Good evening" and then perform 4, i.e. print Good by, and then break 
		case 4:
			System.out.println("Good bye");
			break;
		default:
			System.out.println("Parden me?");
			break;
		}		
	}
}

```

## 3. 循环  
### 3.1 while循环
```java
while (<循环条件>){
    <循环体语句>
}
```  
* 当条件满足时，不断地重复循环语句  
* 循环执行之前判断满不满足条件，所以有可能一次循环都没有过就跳过了  
* 条件成立是循环继续的条件  
* 循环内要有改变条件的机会
例子：【数数字】读入整数，输出这个整数的位数。比如：输入352，输出3
思路：从右往左数有多少位。即，整数除法，可以除多少次10
```java
import java.util.Scanner; 

public class hello2 {
	public static void main(String[] args) {
		Scanner in = new Scanner(System.in);
		int number = in.nextInt();
		int count = 0;
		while (number>0)
		{
			number = number/10;
			count = count +1;
		}
		System.out.println(count);
	}
}
```  

### 3.2 do-while循环
```java
do
{
    <循环体语句>
} while (<循环条件>)
```
* 在进入循环是不做检查，而是在执行完一轮循环体的代码之后，再来验证循环的条件是否满足，如果满足则继续下一轮循环，不满足则结束循环
```java
import java.util.Scanner; 

public class hello2 {
	public static void main(String[] args) {
		Scanner in = new Scanner(System.in);
		int number = in.nextInt();
		int count = 0;
		do // use `do` before the while loop
		{
			number = number/10;
			count = count +1;
		}
		while (number>0); // put `while` at the end of the while loop 
		System.out.println(count);
	}
}
```

### 6.3 验证
* 测试程序常使用边界数据，如有效范围两端的数据、特殊的倍数等
    * 个位数；
    * 10；
    * 负数。