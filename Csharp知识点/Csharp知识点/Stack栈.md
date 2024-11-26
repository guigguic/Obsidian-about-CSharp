# Stack的本质
1. stack（栈）是一个c#为我们封装好的类
2. 它的本质是一个[[继承#万物之父&装箱拆箱#|object]][ ]数组，只是封装了特殊的存储规则

3. stack是栈存储容器，栈是一种先进后出的数据结构
4. 先存入的数据后获取，后存入的数据先获取
5. 栈是==先进后出==的

# Stack的声明
引用命名空间  System.Collections
`Stack stack = new Stack();`

# Stack的增删查改遍历
## 增
 又叫*压栈*
 ```csharp
关键字：Push
stack.Push(1);
stack.Push("123");
stack.Push(true);
stack.Push(1.2f);
stack.Push(new Test());
//放和取只能一个一个来
//最先声明的在栈的最底下最上面的一个是new Test()
```

## 取
栈中不能删减元素 只把元素取出来
又叫*弹栈*
```csharp
关键字：Pop
object v = stack.Pop();
Console.WriteLine(v);

v = stack.Pop();
Console.WriteLine(v);
```

## 查
1. 栈无法查改指定内容的 **元素**
2. 只能查看栈顶的内容
```csharp
关键字：peek
v = stack.Peek();
Console.WriteLine(v);
v = stack.Peek();
Console.WriteLine(v);
```

## 改
栈无法改变其中的元素 只能压（存）和弹（取）
实在要改 只有清空
```csharp
stack.Clear();

Console.WriteLine(stack.Count);
stack.Push("1");
stack.Push(2);
stack.Push("哈哈哈");
```

## 遍历
获得长度，同[[ArrayList]]的关键字`Count`
```csharp
Console.WriteLine(stack.Count);
```

1.用[[循环#foreach|foreach]]获得遍历
```csharp
for(Object ob in stack){
	console.Writeline(ob);
}
```

2.将栈转换为object数组
遍历出来的顺序 也是从栈顶到栈底的
```csharp
object[] array = stack.ToArray();
for (int i = 0; i < array.Length; i++)
{
    Console.WriteLine(array[i]);
}
```

3.循环弹栈
```csharp
while(stack.count > 0 ){
	object o stack.Pop();
	console.Writeline(o);
}
```