#### Object

#### 字符串相关

- `String`
  与C++STL的std::string不同，Java的字符串是完全内置且被编译器特殊处理的。但其原理类似，都是由字符串长度和`char`数组组成的
  String的不可变性是由其内部的`private final char[]`保证的。
  C++可以通过运算符重载实现字符串的比较，但Java在进行字符串内容的比较时应当使用`equals()`方法，而不是`==`，后者只能判定二者是否是**同一个对象*。
  具体的各种方法见[文档 | String](https://www.runoob.com/manual/jdk11api/java.base/java/lang/String.html)。

- `StringBuilder`
  由于Java `String`的不可变性（类似于`const char *`），我们显然需要可变的字符串管理。
  StringBuilder支持链式调用，这是通过对方法返回`this`实现的（类似于`std::stringstream`的`operator <<`）：
  ```java
    var sb = new StringBuilder(1024);
    sb.append("Mr ")
      .append("Bob")
      .append("!")
      .insert(0, "Hello, ");
    sb.toString(); // Hello, Mr Bob!
  ```
  此外还有`StringBuffer`，这是`StringBuilder`的线程安全版本，一般不需要使用。
- `StringJoiner`，简陋的cxx `std::string`似乎没有对应物（`std::stringstream`也过于简陋了）
  ```java
    String[] names = {"Bob", "Alice", "Grace"};
    var sj = new StringJoiner(", ", "[ ", " ]");
    for (String name : names) {
        sj.add(name);
    }
    sj.toString(); // [ Bob, Alice, Grace ]
  ```
#### 包装类
包装类为基本类型的各种操作提供了便利，与fp中的单子（`monad`）的概念类似。
```java
Integer.parseInt("100") // 100
Integer.toString(100); // "100"
Integer.toHexString(255); // "ff"
Integer.MAX_VALUE; // 2147483647

// 由于Java没有运算符重载，应当使用equals进行比较

Integer m = 99999;
Integer n = 99999;
m == n; // false
m.equals(n); // true
```
#### Java Bean
如果一个Java类正确地实现了`getter`和`setter`，比如：
```java
class Clazz {
    Type var;
    Type readOnlyVar;
    int age
    ...
    
    public Type getVar(){...}
    public void setVar(Type value){...}

    public Type getReadOnlyVar(){...} // 只有getter则为只读属性
    
    public boolean isAdult(){ return age > 18;} // 不一定要有对应的成员变量
    ...
}
```
那么称该类为一个`Java Bean`，通过使用`java.beans.*`可以操作`Bean`：
```java
BeanInfo info = Introspector.getBeanInfo(Clazz.class);
for (PropertyDescriptor pd : info.getPropertyDescriptors()) {
    System.out.println(pd.getName());
    System.out.println("  " + pd.getReadMethod());
    System.out.println("  " + pd.getWriteMethod()); // 如果为只读属性则返回null
}
```
#### BigInteger和BigDecimal
```java
BigInteger i1 = new BigInteger("1234567890");
i1.pow(5); // 2867971860299718107233761438093672048294900000
// 显然不能使用运算符
BigInteger i2 = i1.add(new BigIngeter("1")); // "1234567891" 
long l1 = i1.longValueExact(); // 相比于longValue能保证结果准确（否则抛异常）
float f2 = i2.floatValue(); // Infinity
```
### 枚举和记录
