# Queue的本质
是c#为我们封装好的类
它的本质是Object数组，只是封装好了特殊的规则

Queue是队列存储容器
队列是一种==先进先出==得数据结构
先存入的数据先获取，后存入的数据后获取

# 声明
引用命名空间 System.Collections
`Queue queue = new Queue();`

# 增取查改遍历

## 增
关键字:`queue.Enqueue();`
只能一个一个加

## 取
关键字`queue.Dequeue();`

## 查
`objcet v;`
关键字`v = queue.Peek();`

查看元素是否在队列中
```csharp
if(queue.Contains("123")){
	console.writeline("存在123");
}
```
## 改
无法改变其中的元素 只能进出队列
`queue.Clear();`
## 遍历
`console.writeline(queue.count)`

[[循环#foreach|foreach]]遍历
```csharp
foreach (object item in queue){
	console.writeline(item);
}
```

将队列转换为object数组
```csharp
objcet[] ob = queue.ToArray();
for(int i = 0;i < ob.length;i++){
	console.writeline(ob[i])
}
```

循环出列
```csharp
while(queue.count > 0){
	console.writeline(queue.Dequeue());
}
```

# 装箱拆箱
[[ArrayList#装箱|同ArrayList stack 万物之父]]