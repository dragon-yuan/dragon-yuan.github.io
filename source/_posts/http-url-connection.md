---
title: HttpURLConnection中GET请求
categories:
  - Java
date: 2017-08-09 21:11:21
---
```java
public static void httpURLConectionGET() {
    try {
        URL url = new URL("");
        HttpURLConnection connection = (HttpURLConnection) url.openConnection();
        connection.connect();
        BufferedReader br = new BufferedReader(new InputStreamReader(connection.getInputStream(), "UTF-8"));
        String line;
        StringBuilder sb = new StringBuilder();
        while ((line = br.readLine()) != null) {
            sb.append(line);
        }
        br.close();
        connection.disconnect();
        System.out.println(sb.toString());
    } catch (Exception e) {
        e.printStackTrace();
    }
}
```