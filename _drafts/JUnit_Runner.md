# JUnit之Runner原理

### 1. 看一段运行测试的代码
运行测试会调用`JUnitCore#runClasses(Class<?>...)`：
```
	Result result = JUnitCore.runClasses(CustomTest.class);
```
然后从Result中以下接口获取测试的结果：
```
	public int getRunCount() {
        return count.get();
    }

    public int getFailureCount() {
        return failures.size();
    }

    public long getRunTime() {
        return runTime.get();
    }

    public List<Failure> getFailures() {
        return failures;
    }

    public int getIgnoreCount() {
        return ignoreCount.get();
    }
```
接下来对JUnit框架测试运行原理的分析就跟踪`JUnitCore#runClasses(Class<?>[])`这个调用入口，逐步抽丝剥茧。

### 2. 运行原理分析
#### 2.1 JUnitCore#runClasses(Class<?>...)
```
	public static Result runClasses(Class<?>... classes) {
        return runClasses(defaultComputer(), classes);
    }
```
 其中`defaultComputer`方法调用`Computer`的默认构造函数创建一个对象实例，用途后续说明。

 #### 2.2 JUnitCore#runClasses(Computer, Class<?>...)
 ```
 	public static Result runClasses(Computer computer, Class<?>... classes) {
        return new JUnitCore().run(computer, classes);
    }
 ```
 创建一个`JUnitCore`实例并调用`run(Computer, Class<?>...)`：
 ```
 	public Result run(Computer computer, Class<?>... classes) {
        return run(Request.classes(computer, classes));
    }
 ```
 调用`JUnitCore#run(Request)`方法，而Request的创建是由`Request.classes(computer, classes)`创建的：
 ```
 	public static Request classes(Computer computer, Class<?>... classes) {
        try {
            AllDefaultPossibilitiesBuilder builder = new AllDefaultPossibilitiesBuilder(true);
            Runner suite = computer.getSuite(builder, classes);
            return runner(suite);
        } catch (InitializationError e) {
            return runner(new ErrorReportingRunner(e, classes));
        }
    }
 ```

