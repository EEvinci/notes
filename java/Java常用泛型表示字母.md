# Java泛型中的字母表示

## 常用的泛型表示字母

常用的泛型字母表示有`?`, `T`，`K`, `V`, 	`E`

`?`表示不确定的Java类型
`T`取词为	`type`, 表示一种具体的Java类型
`K`取词为`key`, 表示Java键值对中的键
`V`取词为`value`, 表示Java键值对中的值
`E`取词为`element`, 表示元素

## `?`和T在类型表示上的区别
###  `?`表示的泛型参数不一定, 即表示的类型不一定是相同的
例如:
```java
public int MyList(List <? extends Number> dest, List<? extends Number> src)
```
在上面的函数中, 就不能保证两个List具有相同类型的参数
#### 无界通配符
```java
<?>
```
对于不关心实际操作的或者不确定的类型, 可以直接使用一个`<?>`, 表示其可以持有任何类型
#### 上界通配符
```java
<? extends E>
```
extends表示?的类型只能是E或者E的子类, 如果不是会报错 

#### 下届通配符
```java
<? super E>
```
super表示?的类型可以是E或者E的父类, 最高到`Object`
### `T`确保泛型参数是一定的, 即表示的类型是相同的
例如
```java
public <T extends Number> MyList(List <T> dest, List <T> src)
```



## demo
下面是例子 
~~~java
public class FanXing {
 
    TestA a = new TestA("13");
    TestA b = new TestA(123);
 
    public void getClass1(TestA<?> test) {
 
    }
    //报错
    public void getClass2(TestA<T> test) {
 
    }
}
 
class TestA<T> {
    private T t;
 
    public TestA(T key) {
        this.t = key;
    }
}
~~~

在使用泛型作为方法的参数时 就需要使用泛型通配符来解除传入参数的类型，类型参数就做不到

<?>与<字母>的还有一个区别就在于   字母形参可以在之后的函数调用  T  t= it.next();
~~~java
public static void printColl(ArrayList<T> al){
        Iterator<T> it = al.iterator();
        while(it.hasNext())
        {
            T t = it.next();
            System.out.println(t.toString());
        }
}
~~~