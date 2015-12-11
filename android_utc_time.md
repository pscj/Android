# Java UTC时间戳的坑

项目中有个地方需要取到UTC的时间戳传给Server,找到网络上大部分的代码如下转换：
`
//1、取得本地时间：
java.util.Calendar cal = java.util.Calendar.getInstance();
//2、取得时间偏移量：
int zoneOffset = cal.get(java.util.Calendar.ZONE_OFFSET);
//3、取得夏令时差：
int dstOffset = cal.get(java.util.Calendar.DST_OFFSET);
//4、从本地时间里扣除这些差量，即可以取得UTC时间：
cal.add(java.util.Calendar.MILLISECOND, -(zoneOffset + dstOffset));
//之后，您再通过调用cal.get(int x)或cal.getTimeInMillis()方法所取得的时间即是UTC标准时间。`
