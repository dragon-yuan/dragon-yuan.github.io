---
title: Java中处理double数据类型运算不精确的问题
categories:
  - Java
id: 177
date: 2016-07-25 07:00:48
tags:
---

1.相加 

public double sum(double d1,double d2){

        BigDecimal bd1 = new BigDecimal(Double.toString(d1));

        BigDecimal bd2 = new BigDecimal(Double.toString(d2));

        return bd1.add(bd2).doubleValue();

}

2.相减

 public double sub(double d1,double d2){

        BigDecimal bd1 = new BigDecimal(Double.toString(d1));

        BigDecimal bd2 = new BigDecimal(Double.toString(d2));

        return bd1.subtract(bd2).doubleValue();

}

3.相乘

 public double mul(double d1,double d2){

        BigDecimal bd1 = new BigDecimal(Double.toString(d1));

        BigDecimal bd2 = new BigDecimal(Double.toString(d2));

        return bd1.multiply(bd2).doubleValue();

}

4.相除

  public double div(double d1,double d2,int scale){

        //在之前需要判断分母是否为0，或者处理异常

        BigDecimal bd1 = new BigDecimal(Double.toString(d1));

        BigDecimal bd2 = new BigDecimal(Double.toString(d2));

        return bd1.divide(bd2,scale,BigDecimal.ROUND_HALF_UP).doubleValue();

}
