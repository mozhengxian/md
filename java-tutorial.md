<!-- TOC -->

- [基本数据类型](#基本数据类型)

<!-- /TOC -->

## 基本数据类型

1. 整型
   
类型   | 存储需求(字节)
---    | ---
`byte` | 1
`short`| 2
`int`  | 4
`long` | 8

2. 浮点类型

- `float` 4个字节
- `double` 8个字节
  
3. 字符型

- `char` 2个字节   

4. 布尔类型

- `true` 1个字节
- `false` 1个字节

> 基本数据类型是不可变的。整型默认为`int`类型，定义`long`类型需要在后面加上`L或者l`,`eg: long num = 400L`。浮点类型默认为`double`类型，定义`float`类型需要在后面加上`F或者f`, `eg: float number = 3.5F`。

定义常量：需要使用`final`关键字指示常量
`eg: final double CM_PER_INCH = 2.54`，习惯上常量名使用全大写。



<details>
<summary>CLICK ME</summary><summary>标签与正文间一定要空一行！！！
<summary>标签与正文间一定要空一行！！！</details>
----

继承：

关键字：`extends`

```java
class Animal{
    //
}

public class Mammal extends Animal{
    //
}
```

关键字：`implements`，使用在类接口的情况下，这种情况不能使用关键字`extends`。

```java
public interface Animal{
    //
}
public class Mammal implements Animal{
    //
}
public class Dog extends Mammal{
    //
}
```

多态

```java
package DemoJava;


class Employee{
    private String name;
    private String address;
    private int number;

    public Employee(String name, String address, int number)
    {
        System.out.println("Constructing an Employee.");
        this.name = name;
        this.address = address;
        this.number = number;
    }

    public void mailCheck()
    {
        System.out.println("Mailing a check to " + this.name + " " + 
        this.address);
    }

    public String toString()
    {
        return name + " " + address + " " + number;
    }

    public String getName()
    {
        return name;
    }

    public String getAddress()
    {
        return address;
    }

    public int getNumber()
    {
        return number;
    }
}

class Salary extends Employee
{
    private double salary;
    public Salary(String name, String address, int number, double salary)
    {
        super(name, address, number);
        setSalary(salary);
    }

    public void mailCheck()
    {
        System.out.println("Within mailCheck of Salary class ");
        System.out.println("Mailing check to " + getName() + 
        " with salary " + salary);
    }

    public double getSalary(){
        return salary;
    }

    public void setSalary(double newSalary)
    {
        if (newSalary >= 0.0)
        {
            salary = newSalary;
        }
    }

    public double computePay()
    {
        System.out.println("Computing salary pay for " + getName());
        return salary / 52;
    }
}

public class Demo1{
    public static void main(String[] args) {
        Salary s = new Salary("Mohd Mohtashim", "Ambehta, UP", 3, 3600.00);
        Employee e = new Salary("John Adams", "Boston, MA", 2, 2400.00);
        /**
         * 对象变量 s是Salary的引用， 对象变量 e是Employee的引用
         * 在调用s.mailCheck()时，java虚拟机调用Salary类的mailCheck方法
         * 因为e是Employee的引用，所以调用e的mailCheck方法则有所不同
         * 当编译器检查e.mailCheck()方法时，编译器检查到Employee类中的mailCheck方法，
         * 在编译的时候，编译器使用Employee类中的mailCheck方法验证该语句，但是在运行时，
         * java虚拟机调用的是Salary类的mailCheck方法。
         * 该行为成为虚拟方法的调用，该方法成为虚拟方法。
         */

        System.out.println("Call mailCheck using Salary reference --");
        s.mailCheck();
        System.out.println("\n Call mailCheck using Employee reference --");
        e.mailCheck();
    }
}
```

抽象类

使用`abstract class`定义抽象类

```java
// Employees.java
// 抽象类
public abstract class Employees
{
    private String name;
    private String address;
    private int number;
    
    public Employees(String name, String address, int number)
    {
        System.out.println("Constructing an Employee.");
        this.name = name;
        this.address = address;
        this.number = number;
    }
	
    // 抽象方法
    public abstract double computePay();

    public abstract void mialCheck();

    public abstract String toString();

    public abstract String getName();

    public abstract String getAddress();

    public abstract int getNumber();

}
```

继承抽象类后，子类必须实现所有的抽象方法。



接口(`interface`)

接口无法被实例化，但是可以被实现，一个实现接口的类，必须实现接口内所描述的所有方法，除非实现接口的类是抽象类。

接口与类的相似点：

- 一个接口可以有多个方法
- 接口文件保存在`.java`结尾文件中，文件名使用接口名
- 接口的字节码文件保存在`.class`结尾的文件中
- 接口相应的字节码文件必须在与包名称相匹配的目录结构中

接口与类的区别：

- 接口不能用于实例化对象
- 接口没有构造方法
- 接口中所有的方法必须是抽象方法
- 接口不能包含成员变量，除了`static和final`变量
- 接口不是被类继承了，而是要被类实现
- 接口支持多重继承

接口特性：

- 接口是隐式抽象的，当声明一个接口的时候，不必使用`abstract`关键字
- 接口中的每一个方法也是隐式抽象的，声明时同样不需要`abstract`关键字
- 接口中的方法都是公有的

```java
eg:
interface Animal{
    public String getName( String name);
    public void travel();
}

// 接口的实现
// ... implements 接口名称[, 其他接口， 其他接口 ..., ...] ...
public class MammalInt implements Animal{
    public String getName(String name){
        return name;
    }
    public void travel(){
        System.out.println("Mammal travels.")
    }
    // ...
}
```

