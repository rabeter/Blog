

# Junit
## Junit简介
JUnit是运用于Java的单元测试框架。JUnit在开发测试驱动开发中一直很重要。

## 测试简介

测试是检查应用程序的功能以确保其按照要求运行的过程。单位测试在开发商层面展现; 它是单个实体（类或方法）的测试。单位测试在帮助软件公司向客户提供优质产品方面发挥关键作用。

## JUnit的特性


- 提供注释来识别测试方法。

- 提供用于测试预期结果的断言。

- JUnit测试允许您更快地编写代码，从而提高质量。

- JUnit优雅简单。它不那么复杂，花费更少的时间。

- JUnit测试可以自动运行，并检查自己的结果并提供即时反馈。没有必要手动梳理测试结果的报告。

- JUnit测试可以组织成包含测试用例的测试套件，甚至其他测试套件。

- 如果测试运行平稳，JUnit会显示一个绿色的测试进度，当测试失败时，它会变为红色。

## 赛程

- setUp（）方法，它在每次测试调用之前运行。
- tearDown（）方法，每个测试方法后运行

## 注解

注解 | 描述
--- | --
@Test | 测试注释指示该公共无效方法它所附着可以作为一个测试用例。
@Before | 该方法必须在类中的每个测试之前执行，以便执行测试某些必要的先决条件。
@BeforeClass | 这是附着在静态方法必须执行一次并在类的所有测试之前。发生这种情况时一般是测试计算共享配置方法(如连接到数据库)。
@After | 该方法在执行每项测试后执行(如执行每一个测试后重置某些变量，删除临时变量等)
@AfterClass | 当需要执行所有的测试在JUnit测试用例类后执行，AfterClass注解可以使用以清理建立方法，(从数据库如断开连接)。注意：附有此批注(类似于BeforeClass)的方法必须定义为静态。
@Ignore | 当想暂时禁用特定的测试执行可以使用忽略注释。每个被注解为@Ignore的方法将不被执行。


``` java
// 执行顺序
@BeforeClass: onceExecutedBeforeAll

@Before: executedBeforeEach
@Test: EmptyArrayList
@After: executedAfterEach
//两个test样例
@Before: executedBeforeEach
@Test: OneItemArrayList
@After: executedAfterEach

@AfterClass: onceExecutedAfterAll
```

## 断言Assert 

断言 | 描述
--- | --
assertEquals | 断言两个值相等。值可能是类型有 int, short, long, byte, char or java.lang.Object. 
assertArrayEquals | 断言预期数组和结果数组相等。数组的类型可能是 int, long, short, char, byte or java.lang.Object.
assertTrue/assertFalse | 断言条件为真或假
assertNotNull/assertNull | 断言条件为空
assertSame/assertNotSame | 断言两个对象引用相同/不同的对象

