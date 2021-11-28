代码实例
```angular2html
public class Hello {
    public static void main(String[] args) {
        System.out.println("Hello World!");
    }
}
```

```angular2html
javap packagePath.className
javap -c packagePath.className
eg:
javap HelloWorld
javap -c HelloWorld
javap -c com.test.HelloWorld

```
![](../img/2021-11-28-jvm-bytecode/javap.png)

如果想打印常量池，应当加上-verbose
```angular2html
eg: 
javap -c -verbose HelloWorld
```
![](../img/2021-11-28-jvm-bytecode/javap-verbose.png)

如果想要看到本地变量，需要编译时添加参数,这样就会生成一些额外的debug信息
```angular2html
javac -g HelloWorld
javap -c -verbose HelloWorld
```
![](../img/2021-11-28-jvm-bytecode/javap-localvariable.png)

