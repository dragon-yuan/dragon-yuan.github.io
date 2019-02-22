---
title: 线程池中Feture使用
categories:
  - Java
date: 2019-02-20 22:00:26
---
最近遇到一个业务场景：
在导出Excel的时候、Service查询数据库数据返回List集合，数据量很大，在请求完数据以后还需要遍历调用其他中心RPC服务，这种业务场景下无法完成，超时等在所难免。
考虑到多线程处理业务。
顺便提一下……真的很难受，大数据量分片查询ES本来就很慢，真心很无奈。

Futrue：对于多线程来说，可以先拿到一个未来的Future，等所有分支取到结果后在组合数据。阻塞线程。

```java
Vector<Map<String,Object>> dataList = new Vector<>();
// 按照业务场景自定义分页大小
int pageSize = 1000;
// 按照CPU核心数自定义线程大小
int processor = 1 << 3;
ExecutorService executorService = new ThreadPoolExecutor(processor, processor, 1000, TimeUnit.MILLISECONDS, new LinkedBlockingDeque(),
new ThreadFactoryBuilder().setNameFormat("package-task-%d").build());
try {
	// 选择分页方式查询
	int totalPage = (total % pageSize == 0) ? (total / pageSize) : (total / pageSize) + 1;
    List<Future<List<Map<String, Object>>>> futures = new ArrayList<>();
    for (int i = 1; i <= totalPage; i++) {
        final int page = i;
        Future<List<Map<String, Object>>> task = executorService.submit(() -> {
        	PageResult<Map<String, Object>> result = XXX;
            List<Map<String, Object>> listData = result.getListData();
            return listData;
        });
        futures.add(task);
    }
    for (Future<List<Map<String, Object>>> future : futures) {
        dataList.addAll(future.get());
    }
    executorService.shutdown();
} catch (Exception e) {
	executorService.shutdown();
	return Collections.emptyList();
}
```
future.get方法：获取计算结果（如果还没计算完，也是必须等待的）

future.cancel方法：还没计算完，可以取消计算过程

future.isDone方法：判断是否计算完

future.isCancelled方法：判断计算是否被取消