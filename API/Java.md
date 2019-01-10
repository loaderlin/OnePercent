Date JDK1.11之后 推荐使用 Calendar类

```java
long now = System.currentTimeMillis();  // 从1970.01.01 到现在
Date today = new Date(now);             // new Date(long)
Calendar c1 = Calendar.getInstance();   
System.out.println("hi" + now + today + c1.getTime().toString());
```

时间日期的应用
- 获取完整的日期
- 时间日期的格式化
- 时间日期的转换

```java
Date > String

Date today = new Date();
SimpleDateFormat sdf = new SimpleDateFormat("yyyy-MM-dd");
String dateToString = sdf.format(today);

String > Date

String today = "2019-01-01"
SimpleDateFormat sdf = new SimpleDateFormat("yyyy-MM-dd");
Date today = sdf.parse(today);
```

传入1个日期，计算出该日期的2个星期前的 周六的日期

```java
public static Date prepare2WeekDay(Date paramdate) {
    Calendar cal = new GregorianCalendar();
    cal.setTime(paramdate);
    cal.add(Calendar.WEEK_OF_MONTH, -2);
    cal.set(Calendar.DAY_OF_WEEK, Calendar.SATURDAY);
    return cal.getTime();
}
```

Date && Calendar 简单使用

```java
DateTime > Object > String > SimplateDateFormat > Date
Date InsBeginDate = new SimpleDateFormat("yyyy-MM-dd").parse(String.valueOf(insuranceModel.get("insurance_begin_date")));
```