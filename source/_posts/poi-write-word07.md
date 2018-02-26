---
title: APACHE POI写入Word-07操作
categories:
  - Java
date: 2017-02-23 15:22:26
---
<pre>
// 使用POI读取模版
MSWordTool changer = new MSWordTool();
changer.setTemplate(templatePath);
// 导入书签
Map<String, String> wordContent = getContent();
// 替换文件
changer.replaceBookMark(wordContent);
changer.saveAs("path");

// 获取书签数据
private Map<String, String> getContent(){
    Map<String, String> content = new HashMap<String, String>();
  	try {
      content.put("A1", obj);
    } catch (Exception ex) {
      ex.printStackTrace();
    }
    return content;
}

/**
	 * 为文档设置模板
	 * @param templatePath  模板文件路径
   */
public void setTemplate(String templatePath) {
		try {
			this.document = new XWPFDocument(POIXMLDocument.openPackage(templatePath));
			bookMarks = new BookMarks(document);
		} catch (IOException e) {
			e.printStackTrace();
		}
}

/**
	 * 进行标签替换的例子,传入的Map中，key表示标签名称，value是替换的信息
	 * @param indicator
*/
public void  replaceBookMark(Map<String,String> indicator) {
		//循环进行替换
		Iterator<String> bookMarkIter = bookMarks.getNameIterator();
		while (bookMarkIter.hasNext()) {
			String bookMarkName = bookMarkIter.next();

			//得到标签名称
			BookMark bookMark = bookMarks.getBookmark(bookMarkName);

			//进行替换
			if (indicator.get(bookMarkName)!=null) {
				bookMark.insertTextAtBookMark(indicator.get(bookMarkName), BookMark.INSERT_BEFORE);
			}
	  }
}

public void saveAs(String path) {
	  File newFile = new File(path);
		FileOutputStream fos = null;
		try {
			fos = new FileOutputStream(newFile);
		} catch (FileNotFoundException e) {
			e.printStackTrace();
		}
		try {
			this.document.write(fos);
			fos.flush();
			fos.close();
		} catch (IOException e) {
			e.printStackTrace();
		}
}
</pre>
