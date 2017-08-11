---
title: 高德地图工具类（原创）
categories:
  - Java
date: 2017-08-11 21:41:47
---
```java
import com.alibaba.fastjson.JSON;
import com.alibaba.fastjson.JSONArray;
import com.alibaba.fastjson.JSONObject;
import org.apache.http.HttpEntity;
import org.apache.http.client.config.RequestConfig;
import org.apache.http.client.methods.CloseableHttpResponse;
import org.apache.http.client.methods.HttpGet;
import org.apache.http.impl.client.CloseableHttpClient;
import org.apache.http.impl.client.HttpClients;
import org.apache.http.util.EntityUtils;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

import java.io.IOException;

/**
 * 获取高德地图坐标数据
 * Created by dragon on 2017/8/10.
 */
public class GaodeMapGeographyUtil {

    private Logger logger = LoggerFactory.getLogger(this.getClass());
    private final String KEY = "3c831a5f6d3fbf3820e067f7f00fb242";
    private RequestConfig requestConfig = RequestConfig.custom()
            .setSocketTimeout(15000)
            .setConnectTimeout(15000)
            .setConnectionRequestTimeout(15000)
            .build();

    /**
     * 方法入口1 : 通过城市名称，详细地址；获取高德地图经纬度
     * @param city
     * @param address
     * @return 地理坐标
     */
    public String getContantGeographical(String city,String address) {
        String getUrl = "http://restapi.amap.com/v3/geocode/geo?batch=true&address=" + address + "&city=" + city + "&output=JSON&key=" + KEY;
        String location = "";
        try {
            HttpGet httpGet = new HttpGet(getUrl);
            String resultStr = sendHttpGet(httpGet);
            JSONObject resultObj = JSON.parseObject(resultStr);
            JSONArray geocodesArray = resultObj.getJSONArray("geocodes");
            if (null != geocodesArray && geocodesArray.size() > 0){
                JSONObject geocodesObj = JSON.parseObject(geocodesArray.get(0).toString());
                location = geocodesObj.get("location").toString();
            }
        } catch (Exception e) {
            e.printStackTrace();
        }
        return location;
    }

    /**
     * 方法入口2 : 通过高德地图经纬度，逆向获取地址
     * @param geographical
     * @return 地址
     */
    public String getContantAddressByGeographical(String geographical){
        String getUrl = "http://restapi.amap.com/v3/geocode/regeo?key=" + KEY + "&location=" + geographical + "&poitype=&radius=1000&extensions=all&batch=false&roadlevel=0";
        String address = "";
        try {
            HttpGet httpGet = new HttpGet(getUrl);
            String resultStr = sendHttpGet(httpGet);
            JSONObject resultObj = JSON.parseObject(resultStr);
            Object regeocodeObj = resultObj.get("regeocode");
            String jsonString = JSON.toJSONString(regeocodeObj);
            JSONObject jsonObj = JSON.parseObject(jsonString);
            address = jsonObj.get("formatted_address").toString();
        } catch (Exception e) {
            e.printStackTrace();
        }
        return address;
    }

    /**
     * 方法入口3 : 测试方法，通过高德地图经纬度，逆向获取地址，POIS
     * @param geographical
     * @return 地址
     */
    public String getContantAddressByGeographicalPois(String geographical){
        String getUrl = "http://restapi.amap.com/v3/geocode/regeo?key=" + KEY + "&location=" + geographical + "&poitype=&radius=1000&extensions=all&batch=false&roadlevel=0";
        String address = "";
        double distance = 500;
        try {
            HttpGet httpGet = new HttpGet(getUrl);
            String resultStr = sendHttpGet(httpGet);
            JSONObject resultObj = JSON.parseObject(resultStr);
            // 获取 [regeocode]
            Object regeocodeObj = resultObj.get("regeocode");
            String regeocodeObjToStr = JSON.toJSONString(regeocodeObj);
            JSONObject jsonObj = JSON.parseObject(regeocodeObjToStr);
            // 获取 [pois]
            Object poisObj = jsonObj.get("pois");
            String poisObjToStr = JSON.toJSONString(poisObj);
            JSONArray poisArray = JSON.parseArray(poisObjToStr);
            // 获取最近 [poi]
            for (int i = 0; i < poisArray.size(); i++){
                Object poiObj = poisArray.get(i);
                String poiStr = JSON.toJSONString(poiObj);
                JSONObject poi = JSON.parseObject(poiStr);
                double poiDistance = Double.parseDouble(poi.get("distance").toString());
                if (poiDistance < distance){
                    // 返回地址数据
                    distance = poiDistance;
                    address = poi.get("address").toString() + poi.get("name").toString();
                }
            }
            logger.info("address = " + address + " , " +"pois.distance = " + distance);
        } catch (Exception e) {
            e.printStackTrace();
        }
        return address;
    }

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
}

```