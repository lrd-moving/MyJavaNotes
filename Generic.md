## 泛型（Generic）



### 泛型类

```java
class 类名称 <泛型标识：可以随便写任意标识号，标识指定的泛型的类型>{
  private 泛型标识 成员变量类型 var; 
  .....

  }
}
```

一个栗子：

```Java
class Mystack<T>{
    private T[] elements;

    public T top(){
    }
}
```

- **注意：** 泛型的类型参数不能为简单类型（int，char...）

### 泛型接口

- 直接参考 Collections

### 泛型方法

```Java
public static <E extends Number> void printArray(E[] array) {
    for (E element : array){
        System.out.printf("%d \n", element);
    }

    System.out.println();
}
```

- 泛型声明在 static 和 void 间，**"E"** 类型声明，即可用
- **extends** 限定E为 **Number** 的子类





