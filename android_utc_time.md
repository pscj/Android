# UTC时间戳的坑

'
//1、取得本地时间：
java.util.Calendar cal = java.util.Calendar.getInstance();
//2、取得时间偏移量：
int zoneOffset = cal.get(java.util.Calendar.ZONE_OFFSET);
//3、取得夏令时差：
int dstOffset = cal.get(java.util.Calendar.DST_OFFSET);
//4、从本地时间里扣除这些差量，即可以取得UTC时间：
cal.add(java.util.Calendar.MILLISECOND, -(zoneOffset + dstOffset));
//之后，您再通过调用cal.get(int x)或cal.getTimeInMillis()方法所取得的时间即是UTC标准时间。
'
