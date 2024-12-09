```java
class Person {
    // 每个成员变量/方法（包括构造方法）都需要指明控制访问权限
    private String name = "Unamed"; // 和C++一样，
                                    // 可以在定义时对成员变量规定初始化
                                    // 同样也会被构造方法覆盖掉
    // final 变量不可更改，类似于const
    // static表示该字段/方法是静态的（属于类而不是对象），与C++类似
    public static final String SPECIES = "Homo sapien"; 
    private static int POPULATION = 0;

    private int age = 18; 

    protected String[] nicknames;// 如果没有在构造方法中初始化字段，
                               // 引用类型默认是null，基本类型用默认值

    public Person() {
        this("Whoever", 18); // 可以使用类似C++委托构造的语法
    }

    public Person(String name, int age) {
        // 和C++一样，如果我们定义了构造方法
        // 那么编译器就不会再生成默认构造方法
        POPULATION++;
        this.name = name;
        this.age = age;
        this.nicknames = new String[];
    }

    public String getName() {
        return this.name;
    }

    // 对于引用参数，传参是引用的
    public void setName(String name) { 
        this.name = name; // this是“引用”，而不是指针，不需要"->"语法 
                          // 赋值却是拷贝的，对于String,默认就是深拷贝        
    }

    public int getAge() {
        return this.age;
    }

    // 对于基本类型（如int），传参是拷贝
    public void setAge(int age) { // 没有“默认参数”的语法
        if (age < 0 || age > 100) {
            throw new IllegalArgumentException("invalid age value");
        }
        this.age = age;
    }

    public void setNicknames(String... nicknames) { 
        // 可变参数的声明和使用比C++简单得多
        // 实际上几乎就是一个数组，只不过能够接受null值
        // 且不需要手动来(new T[])构造参数，直接(T t1, T t2, ...)就好
        this.nicknames = nicknames;
    }

    public static class PopulationManagement{ // Java支持嵌套类
        public static void addPopulation(int n){
            Person.POPULATION += n; // 嵌套类拥有访问private的权限
        }
    }


    public void say(){
        System.out.println("Hi!\n");
    }

    public void say(String sth){ // 支持重载
        System.out.println(sth);
    }

    public final void sayAge(){ // final 方法不能覆写
        System.out.println(age);
    }

    @Override
    public String toString(){ // 覆写Object的方法
                              // 还可以覆写equals、hashCode等方法
        String res = "name: " + name + ", age: " + age; // 局部变量
        return res;
    }
}
```

```java
class Student extends Person { // 继承用extends关键字，Java只支持单继承
                               // 所有的class最终都继承自Object
    // 子类无法访问父类的private字段/方法
    // 但可以访问父类（以及祖先类）protected字段/方法
    private int score;

    public Student(String name, int age, int score){
        super(name, age); // 不同于C++，Java子类的构造方法必须手动被调用
                          // 子类不会继承任何父类的构造方法
        this.score = score;    
    }

    @Override // 不是必需的，但可以帮助编译器检查
    public say(){
        System.out.println(getName()); // 基类private变量不可访问
        for(String nickname : super.nicknames){ // 基类protected变量可访问
            System.out.println(nickname);
        }
    }
    public int getScore(){...}
    public void setScore(int score){...}
}                             
```

```java
Person.SPECIES == "Homo sapien"
Person.PopulationManageerson.PopulationManage
P
Person p1 = new Person(); 
Person p2 = new Student(); // 基类引用可以指向派生类，称为向下转型
Student s1 = (Student) p1; // runtime error! ClassCastException!
Student s2 = (Student) p2; // ok
p2.say(); // 基于运行时多态，会调用Student的say方法 
// instanceof 操作符
p1 instance of Person == true
p1 instance of Student == false
p2 instance of Person == true
p2 instance of Student == true
// Java 14 以后
        Object obj = "hello";
    f (obj instanceof String s) {
    // 可以直接使用变量s:
    System.out.println(s.toUpperCase());
}
```

```java
public sealed class Shape permits Rect, Circle, Triangle {
    // 用sealed关键字修饰后，该类只允许permits后面Rect, Circle, Triangle三个类继承
    // Java17后支持，C++似乎没有类似的语法？
    public abstract double area(); // 类似于 C++ virtual f()  = 0;
                                   // 同样，含有抽象方法的类是抽象类，不能实例化
}

public final class Rect extends Shape {...} // final修饰的类不允许再被继承
```

```java
package world.of.transformers // 包类似于namespace，但和Python的包概念更像
                      // 包之间没有父子关系，包要和项目中的目录结构对应
                      // 比如，这个包可以访问所有包名为world.of.transformers的文件的内容
                      // 推荐的做法是使用倒置的域名来确保唯一性，eg. org.apache

/*
package_sample
└─ src
   └─ world
      └─ of
         └─transformers
            └─Verhicle.java
*/

interface Verhicle { // 接口相当于没有非静态字段的抽象类
    void run();
}

interface Car extends Verhicle{ // 接口也可以继承
    default void getFueled(){ // 实现类如果不覆写default方法则使用默认的
        System.out.println("fueling\n");
    }
    void startEngine(){
        Runnable r = new Runnable() { // 匿名类，实现Runnable接口
            @Override
            public void run(){
                while(true){
                    Thread.sleep(10000);
                    System.out.println("Engine running\n");
                }
            }
        }
    }
}

interface Bicycle extends Verhicle{
    public static wheelNum = 2; // 接口只可以有静态字段
}

public /*这个public表示其他包可以访问他*/ class Transformer implements Verhicle { 
                                                    // 类要实现接口，
                                                    // 不是用extends，而是用implements
    void run() {
        System.out.println("Transformer running\n");
    }
}
```