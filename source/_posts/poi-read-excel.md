---
title: APACHE POI读取Excel-07操作
categories:
  - Java
date: 2017-02-22 14:14:26
---
<pre>
// 得到Excel工作簿对象
XSSFWorkbook workbook = new XSSFWorkbook(new FileInputStream(file));
// 得到Excel工作表对象
XSSFSheet sheet = workbook.getSheetAt(0);
// 遍历工作表中行
for (Row row : sheet) {
    // 获取当行数
    int rowNum = row.getRowNum();
    // 跳过第一行，如导入Excel模版
    if (rowNum != 0) {
    // 获取此行上的单元格
		  Cell cell = row.getCell(0);
      // 得到Excel工作表指定行的单元格，并设置读取编码方式
			cell.setCellType(HSSFCell.CELL_TYPE_STRING);
			row.getCell(1).setCellType(HSSFCell.CELL_TYPE_STRING);
		  row.getCell(2).setCellType(HSSFCell.CELL_TYPE_STRING);
			row.getCell(3).setCellType(HSSFCell.CELL_TYPE_STRING);
      // 获取内容
      String str1 = cell.getStringCellValue();
			String str2 = row.getCell(1).getStringCellValue();
			String str3 = row.getCell(2).getStringCellValue();
    }
}

此方法没有处理异常，请自行添加
</pre>
