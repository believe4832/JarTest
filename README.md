> mpi包在打包时会把jar打进去，于是产生了一个疑问：比如有一个commons-lang-2.2.jar被打进了jar中，项目也引用了“commons-lang-2.2.jar”。那么在运行时到底调用mpi包中的“commons-lang-2.2.jar”还是调用项目中引用的“commons-lang-2.2.jar”？

# 测试过程

## 准备common-test-in.jar
### 新建CommonTestIn工程

Common.java的代码如下：
```java
package common;

public class Common {

	public static String common_test() {
		return "I am common in";
	}
}
```

### 打common-test-in.jar

## 准备common-test-out.jar
### 新建CommonTestOut工程
- Common.java类的包路径跟common-test-in.jar中的是一样的

- Common.java的代码如下：
```java
package common;

public class Common {

	public static String common_test() {
		return "I am common out";
	}
}
```

### 打common-test-out.jar
步骤跟“打common-test-in.jar”一样。

## 准备mpi.jar
### 新建Mpi工程
- 将上面打的common-test-in.jar放进去


- MpiTest.java的代码如下：
```java
package mpi;

import common.Common;

public class MpiTest {

	public String getCommonMsg() {
		return Common.common_test();
	}
}
```

### 打mpi.jar

## 准备测试工程JarTest
- 将mpi.jar放进工程里

- JarTest.java的代码如下：
```java
package jartest;

import common.Common;

public class JarTest {

	public static void main(String[] args) {
		// TODO Auto-generated method stub
		System.out.println("Who are you?");
		System.out.println("Mpi调用common");
		System.out.println(Common.common_test());
		System.out.println("main调用common");
		System.out.println(Common.common_test());
	}
}
```

- 在只引用mpi.jar的情况下，提示类缺失：

- 导入common-test-out.jar后，编译正常：

- 接下来我们看下执行结果：

## 总结
jar里面的jar是无法被外部调用的，也无法被jar中的方法调用。也就是说，打进jar中的jar是没有用的。当我们需要提供jar给外部系统使用的时候，应该告知对方，我们的jar使用了哪些依赖包。















