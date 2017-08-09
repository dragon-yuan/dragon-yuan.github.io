---
title: HttpClient中GET请求
categories:
  - Java
date: 2017-08-09 21:11:21
---
推荐使用HttpClient版本4.5
```java
private RequestConfig requestConfig = RequestConfig.custom()  
        .setSocketTimeout(15000)  
        .setConnectTimeout(15000)  
        .setConnectionRequestTimeout(15000)  
        .build();
```
```java
private String sendHttpGet(HttpGet httpGet) {
    CloseableHttpClient httpClient = null;
    CloseableHttpResponse response = null;
    HttpEntity entity = null;
    String responseContent = null;
    try {
        httpClient = HttpClients.createDefault();
        httpGet.setConfig(requestConfig);
        response = httpClient.execute(httpGet);
        entity = response.getEntity();
        responseContent = EntityUtils.toString(entity, "UTF-8");
    } catch (Exception e) {
        e.printStackTrace();
    } finally {
        try {
            if (response != null) {
                response.close();    
            }    
            if (httpClient != null) {
                httpClient.close();
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
    return responseContent;
}
```