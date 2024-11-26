
# 回顾
在c#核心中 [[封装#索引器#索引器的增删查改|索引器]]的练习题
自定义一个整形数组类 该类专用有一个整形数组变量
为它封装增删查改的方法

# Arraylist的本质
1. ArrayList本质是C#为我们封装好的类
2. 他的本质是一个[[继承#万物之父&装箱拆箱#基本概念|object]]的数组
3. ArrayList类帮助我们实现了很多方法
4. 比如[[数组]]的增删查改

# ArrayList的声明
需要引用命名空间`System.Collections`
```csharp
Arraylist array = new ArrayList();
```

# ArrayLIst的增删查改遍历
## 增
可以存储任意类型在其中（单个）
```csharp
array.Add(1);
array.Add("123");
array.Add(true);
array.Add(new object());
array.Add(new Test());
array.Add(1);
array.Add(true);
```
批量（范围）
```csharp
ArrayList array2 = new ArrayList();
array2.add(123);
```
把另一个ArrayList容器里面的内容加到后面
```csharp
array.AddRange(array2);
```
插入
```csharp
//左边是插入到哪个位置，右边是插入什么内容
array.Insert(1,"1234567");
console.Writeline(array[1]);//显示结果为1234567
```

## 删
移除指定元素 从头找 找到删(找到1就删)
```csharp
array.Remove(1);
```
移除指定位置的元素（删掉索引号为2的内容）
```csharp
array.RemoveAt(2)
```
清空
```csharp
array.clear();
```

## 查
得到指定位置的元素
`console.writeline(array[0]);`

查看元素是否存在
```csharp
if ( array.Contains("123") ){
	//Contains是bool类型的
	Console.WirteLine("存在123");
}
```

正向查找
找到的返回值 是==位置== 找不到 返回值就是-1
```csharp
int index = array.IndexOf(true);
Console.WriteLine(index); //重头开始找 找到就停止
```

反向查找
反向查找元素位置，返回的是从头开始的索引数
```csharp
index = array.LastIndexOf(true);
Console.WriteLine(index);
```

## 改
与数组相同
```csharp
 Console.WriteLine(array[0]);
 array[0] = "999";
 Console.WriteLine(array[0]);
```

## 遍历
得到长度的关键字：Count
`Console.WriteLine(array.Count);` 元素到底存了多少个
容量[[string的常用方法#StringBuilder|StringBuilder]]避免产生过多的垃圾
`Console.WriteLine(array.Capacity);`
方法1for循环
```csharp
for( int i = 0; i <array.Count;i++ ){
	Console.WirteLine(array[i]);
}
```
方法2 [[循环#foreach|foreach]]
```csharp
foreach (object item in array){
	Console.WriteLine(item);
}
```

# 装箱
1. ArrayList本质上是一个可以自动扩容的object数组
2. 由于用万物之父来存储，自然存在装箱拆箱
3. 当往其中进行值类型存储时就是在装箱，当将值类型对象取出来,，转换使用时，就存在装箱拆箱
4. 所有ArrayList尽量少用
```csharp
int i = 1;  //栈
array[0] = i;//装箱 栈=>堆

i = (int)array[0];  //拆箱 堆=>栈
```

# ArrayLIst和数组的区别
ArrayList本质上是一个object数组的封装

1. ArrayList可以不用一开始就定长（定义长度），单独使用数组是定长
2. 数组可以指定存储类型，ArrayList默认为object类型
3. 数组的增删需要我们自己去实现，ArrayList帮我们封装了方便的API来使用
4. ArrayList使用时可能存在装箱拆箱，数组使用时只要不是object数组那就不存在这个问题
5. 数组长度为length，ArrayList长度为Count
