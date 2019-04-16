## Date & Time 

- **instant:**  时间戳
- **LocalDate:** 日期（时区无关）
- **LocalTime:** 时间（时区无关）
- **LocalDateTime:**  日期和时间(时区无关)
- **ZonedDateTime:** 日期和时间
- **ZoneId:** 时区

------

- 时间加减

  ```java
          /*
          * 时间加减
          * */
          ztime.plus(1, ChronoUnit.DAYS);
          System.out.println(ztime.toString());
  
  ```

- **时间比较**

  ```java
          /*
          * 时间比较
          * */
          LocalDateTime localNextyear = localtime.plusYears(1);
          System.out.println("Compare this year and next year = " + localNextyear.isAfter(localtime));
  ```

- **本地时间转化为GMT时间**

  ```java
          /*
          * ZoneId 表示特定时区
          * */
          //本地时间转化为GMT时间
          ZonedDateTime gmtZonetime = ZonedDateTime.ofInstant(Instant.now(), ZoneId.of("GMT"));
          System.out.println(gmtZonetime.toLocalDateTime().toString());
  ```

- **格式化输出**

  ```java
          /*
          * 格式化输出
          * */
          DateTimeFormatter df = DateTimeFormatter.ofPattern("yyyy-MM-dd HH:mm:ss");
          System.out.println(df.format(gmtZonetime));
  ```

- **时间格式解析**

  ```java
          /*
          * 时间格式解析
          * */
          df = DateTimeFormatter.ofPattern("yyyy-MM-dd HH:mm:ss");
          localtime = LocalDateTime.parse("2018-12-11 12:11:12", df);
          System.out.println(localtime.toString());
  ```

  

