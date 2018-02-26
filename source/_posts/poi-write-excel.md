---
title: APACHE POI写入Excel-07操作
categories:
  - Java
date: 2017-02-22 14:22:26
---
<pre>
// 创建Excel工作簿
XSSFWorkbook workBook = new XSSFWorkbook();
// 创建一个工作薄对象
XSSFSheet sheet = workBook.createSheet("sheet1");
// 设置单元格宽度
sheet.setDefaultColumnWidth(20);
// 画表
XSSFRow row_1 = sheet.createRow(0);
XSSFCell cell_1_0 = row_1.createCell(0);
XSSFCell cell_1_1 = row_1.createCell(1);
cell_1_0.setCellValue("value");
cell_1_1.setCellValue("value");
// 写入文件
File file = new File("");
file.createNewFile();
FileOutputStream os = FileUtils.openOutputStream(file);
workBook.write(os);
os.close();
</pre>
