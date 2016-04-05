title: "JODA-TIME 文档"
date: 2016-04-04 20:29:26
tags: joda-time
---

为什么选择joda-time？因为jdk的时间类比较简陋，先看几个joda-time官网的示例代码：

```java
public boolean isAfterPayDay(DateTime datetime) {
  if (datetime.getMonthOfYear() == 2) {   // February is month 2!!
    return datetime.getDayOfMonth() > 26;
  }
  return datetime.getDayOfMonth() > 28;
}

public Days daysToNewYear(LocalDate fromDate) {
  LocalDate newYear = fromDate.plusYears(1).withDayOfYear(1);
  return Days.daysBetween(fromDate, newYear);
}

public boolean isRentalOverdue(DateTime datetimeRented) {
  Period rentalPeriod = new Period().withDays(2).withHours(12);
  return datetimeRented.plus(rentalPeriod).isBeforeNow();
}

public String getBirthMonthText(LocalDate dateOfBirth) {
  return dateOfBirth.monthOfYear().getAsText(Locale.ENGLISH);
}
```

接下来看一下joda-time的主要功能:
* LocalDate - date without time（没有时间的日期）
* LocalTime - time without date （没有日期的时间）
* Instant - an instantaneous point on the time-line （时间轴上的时间点）
* DateTime - full date and time with time-zone （没有时区的日期时间）
* DateTimeZone - a better time-zone （好用的时区）
* Duration and Period - amounts of time （时间段）
* Interval - the time between two instants （两个时间点之间的时间）
* A comprehensive and flexible formatter-parser （灵活全面的时间格式化工具）

如何构建？
Each date-time class provides a variety of constructors. These include the Object constructor. This allows you to construct an instance from a variety of different objects: For example, a DateTime can be constructed from the following objects:
每个date-time类都提供多个构造方法。这些包含类构造方法。用这些方法能够从不同的类构造date-time类，例如：
* Date - a JDK instant
* Calendar - a JDK calendar
* String - in [ISO8601](http://baike.baidu.com/link?url=gnzdJcOeandNP8OXZUSh2U4z9EEPLQLyoBD6JjzfQEohi8-R8joiuQOBuO5J7DqE9AHak-fCXYTGsyvXusZXK_#4) format 
* Long - in milliseconds
* any Joda-Time date-time class


(ISO8601 格式：合并表示时，要在时间前面加一大写字母T，如要表示北京时间2004年5月3日下午5点30分8秒，可以写成2004-05-03T17:30:08+08:00或20040503T173008+08。)

# 日期和时间（Date and Time）

The use of an Object constructor is a little unusual, but it is used because the list of types that can be converted is extensible. The main advantage is that converting from a JDK Date or Calendar to a Joda-Time class is easy - simply pass the JDK class into the constructor. For example, this code converts a java.util.Date to a DateTime:
例如，将Date转化为DateTime
```java
java.util.Date juDate = new Date();
DateTime dt = new DateTime(juDate);
```
Each date-time class provides simple easy methods to access the date-time fields. For example, to access the month and year you can use:
每个类都提供了简单易用的方法获取时间字段。例如，可以用如下方法获取年和月：
```java
  DateTime dt = new DateTime();
  int month = dt.getMonthOfYear();  // where January is 1 and December is 12
  int year = dt.getYear();
```
All the main date-time classes are immutable, like String, and cannot be changed after creation.
However, simple methods have been provided to alter field values in a newly created object. For example, to set the year, or add 2 hours you can use:
所有主要的时间类都是不可变的，类似于String类，一旦创建就不能改变。但是可以通过类提供的简单方法修改字段值。
例如，可以设置年份或者加2个月：
```java
  DateTime dt = new DateTime();
  DateTime year2000 = dt.withYear(2000);
  DateTime twoHoursLater = dt.plusHours(2);
```
In addition to the basic get methods, each date-time class provides property methods for each field. 
These provide access to the full wealth of Joda-Time functionality. For example, to access details about a month or year:
获取年和月的的详情：
```java
  DateTime dt = new DateTime();
  String monthName = dt.monthOfYear().getAsText();
  String frenchShortName = dt.monthOfYear().getAsShortText(Locale.FRENCH);
  boolean isLeapYear = dt.year().isLeap();
  DateTime rounded = dt.dayOfMonth().roundFloorCopy();

```







