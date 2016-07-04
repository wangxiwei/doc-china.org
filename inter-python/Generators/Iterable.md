# 可迭代对象(Iterable)

Python中任意的对象，只要它定义了可以返回一个迭代器的```__iter__```方法，或者定义了可以支持下标索引的```__getitem__```方法(这些双下划线方法会在其他章节中全面解释)，那么它就是一个可迭代对象。简单说，可迭代对象就是能提供迭代器的任意对象。那迭代器又是什么呢？