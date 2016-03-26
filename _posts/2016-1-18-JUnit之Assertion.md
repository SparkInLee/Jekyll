---
layout: post
title: "JUnit之Assertion"
comments: true
---

**摘要**：本文总结了单元测试框架JUnit的断言函数。
<!-- excerpt split -->

### 1、True断言

```java
assertTrue(boolean)
assertTrue(String, boolean)
```
注：相对应的有`assertFalse`进行False断言

### 2、非等断言

```java
assertNotEquals(Object, Object)
assertNotEquals(String, Object, Object)
assertNotEquals(long, long)
assertNotEquals(String, long, long)

// 参数分别指：unexpected, actual,delta，其中delta用于非精准断言
assertNotEquals(float, float, float)

assertNotEquals(double, double, double)
assertNotEquals(String, double, double, double)
```
注：相对应的有`assertEquals`进行相等断言

## 3、 数组断言

```java
// [Object | boolean | byte | char | short | int | long | double | float]
assertArrayEquals(Object[], Object[]) 

assertArrayEquals(String, Object[], Object[])
```
注：对于`double`及`float`需要传入`delta`进行非精准断言

## 4、非空断言

```java
assertNotNull(Object)
assertNotNull(String, Object)
```
注：相对应的有`assertNull`进行空断言

## 5、相同断言

```java
assertSame(Object)
assertSame(String, Object)
```
注：相对应的有`assertNotSame`进行非同断言

## 6、匹配断言

```java
assertThat(T, Matcher<? super T>)
assertThat(String, T, Matcher<? super T>)
```
注：具体见[JUnit之Matcher]({{ site.baseurl }}/2016/01/JUnit之Matcher)
