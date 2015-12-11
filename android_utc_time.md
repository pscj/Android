# Java UTC时间戳的坑

项目中有个地方需要取到UTC的时间戳传给Server,找到网络上大部分的代码如下转换：
```Java
//1、取得本地时间：
java.util.Calendar cal = java.util.Calendar.getInstance();
//2、取得时间偏移量：
int zoneOffset = cal.get(java.util.Calendar.ZONE_OFFSET);
//3、取得夏令时差：
int dstOffset = cal.get(java.util.Calendar.DST_OFFSET);
//4、从本地时间里扣除这些差量，即可以取得UTC时间：
cal.add(java.util.Calendar.MILLISECOND, -(zoneOffset + dstOffset));
//之后，您再通过调用cal.get(int x)或cal.getTimeInMillis()方法所取得的时间即是UTC标准时间。
```
实际上从cal.getTimeInMillis()取出来的毫秒数是不对的，当设置不同时间时，用这个方法取到的值是不同的。正确的方法应该是
```
java.util.Calendar cal = java.util.Calendar.getInstance();
cal.getTimeInMillis();
```
getTimeInMillis实际上已经是取utc毫秒数了，和时区没关系 
***
参考资料：[Java Timezone why different timezone give same value in millisec](http://stackoverflow.com/questions/9867254/java-timezone-why-different-timezone-give-same-value-in-millisec)
