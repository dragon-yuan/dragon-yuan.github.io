---
title: List对于remove操作抛出ConcurrentModificationException
categories:
  - Java
---
<pre>
for(int i=0;i<list.size();i++){
    if(list.get(i).equals("del"))
        list.remove(i);
}
这种方式的问题在于，删除某个元素后，list的大小发生了变化，而你的索引也在变化，
所以会导致你在遍历的时候漏掉某些元素。比如当你删除第1个元素后，
继续根据索引访问第2个元素时，因为删除的关系后面的元素都往前移动了一位，
所以实际访问的是第3个元素。因此，这种方式可以用在删除特定的一个元素时使用，
但不适合循环删除多个元素时使用。
for(String x:list){
    if(x.equals("del"))
        list.remove(x);
}
这种方式的问题在于，删除元素后继续循环会报错误信息ConcurrentModificationException，
因为元素在使用的时候发生了并发的修改，导致异常抛出。
但是删除完毕马上使用break跳出，则不会触发报错。
Iterator<String> it = list.iterator();
while(it.hasNext()){
    String x = it.next();
    if(x.equals("del")){
        it.remove();
    }
}
这种方式可以正常的循环及删除。
</pre>
