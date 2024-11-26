#常用泛型数据结构类 #链表

# LinkedList是什么
`LinkedList`是c#为我们封装好的一个类
它的本质是一个可变类型的泛型双向[[Csharp知识点/顺序存储和链式存储|链表]]

# LinkedList的声明
需要引用命名空间 `System.Collections.Generic`
```csharp

//————————————————————————Main
LinkedList<int> linkedLast = new LinkedList<int>();
LinkedList<string> linkStr = new LinkedList<string>();
```
链表对象 需要掌握两个类
一个是链表本身`LinkedList` 一个是链表节点类`LinkedListNode`

# LinkedList的增删查改
## 增
```csharp
//————————————————————————Main 声明
LinkedList<int> linkedLast = new LinkedList<int>();
LinkedList<string> linkStr = new LinkedList<string>();

//1.从链表尾部添加元素
linkedLast.AddLast(10);

//2.在链表头部添加元素
linkedLast.AddFirst(20);

//3.在某一个节点之后添加一个节点
//  需要指定节点 先得得到一个节点(查)
LinkedListNode<int> n = linkedLast.Find(20);
linkedLast.AddAfter(n,15);  //在找到的节点后面添加一个15的节点

//4.在某一个节点之前添加一个节点
//  要指定节点 先得得到一个节点（查）
linkedLast.AddBefore(n, 12);
```

## 删
```csharp

//————————————————————————Main

//1.移除头部节点
LinkedLast.RemoveFrist();

//2.移除尾部节点
LinkedLast.Rmovelast();

//3.移除指定节点
//  无法通过位置直接删除
LinkedLast.Remove(20);

//4.清空
LinkedLast.Clear();
```

重新赋值
```csharp
linkedLast.AddLast(1);
linkedLast.AddLast(2);
linkedLast.AddLast(3);
linkedLast.AddLast(4);
```
## 查
删的部分重新赋值了
```csharp

//————————————————————————Main

//1.查询头节点
LindeListNode<int> first = LinkedLast.Frist;

//2.查询尾节点
LinedListNode<int> last = LinkedLast.Last;

//3.找到指定值的节点
//  无法直接通过下标获取中间值
//  只能通过遍历查找元素位置
LinkedListNode<int> node = LinkedLast.Find(/*Find寻找，填入值*/3);
Console.Writeline(node.value);  //显示3
node = linkedLast.Find(5);  //显示空

//4.判断是否存在
if(LinkedLast.Contains(1))
{
	console.writeline("存在1节点");
}
```

## 改
```csharp

//————————————————————————Main

//要先得再改 得到节点 再改变其中的指
Console.WriteLine(LinkedLast.Frist.Value);  //1
linkedLast.First.Value = 10;
Console.WriteLine(LinkedLast.Frist.Value);  //10
```

# 遍历
1.foreach遍历
```csharp

//————————————————————————Main
foreach(int item in linkedLast){
	console.writeline(item)
}
```
2.通过节点遍历
  从头到尾
```csharp

//————————————————————————Main
LinkedListNode<int> nowNode = linkedLast.first;
while(nowNode != null){
	console.writeline(nowNode.value);
	nowNode = nowNdoe.Next;
}
```
从尾到头
```csharp

//————————————————————————Main
nowNode = linkedLast.last;
while(nowNOde != null)
{
	console.writeline(nowNode.Value);
	nowNode = nowNode.Previous;
}
```