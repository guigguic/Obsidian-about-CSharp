#委托和事件 
# 什么是Lambad表达式
可以将`lambad表达式`理解为匿名函数的简写
它除了写法不同外 使用上和[[匿名函数]]一模一样
都是和[[delegate委托|委托]]或者事件配合使用

# Lambad表达式语法
```csharp
//————————————————————————Main
//匿名函数
delegate(参数列表)
{
	
};

//lambad表达式
(参数列表)=>{
	函数体：
};
```

# 使用
**其他传参使用等和匿名函数一样**
**缺点也是一样的**
1. 无参无返回
```csharp
//————————————————————————Main
Action a = () =>{
	Console.WriteLine("无参无返回值的lambad表达式");
};
a();
```

2. 有参无返回
```csharp
//————————————————————————Main
Action<int> a2 = ()=>{
	Console.WriteLine($"有参数的lambad表达式 {value}");
};
a2(100);
```

3. 甚至参数类型都可以省略 参数类型和委托或事件容器一致就行
```csharp
//————————————————————————Main
Action<int> a3 = (/*int*/value)=>{
	Console.WriteLine($"省略参数类型的写法 {value}");
};
a3(200);
```

4. 有返回
```csharp
//————————————————————————Main
Func<string,int> a4 = (value) =>{
	Console.WriteLine($"有参数有返回值的lambad表达式 {value}");
	return 1;
};
Console.WriteLine(a4("321321"));
```

# 闭包
闭包就是内层的函数可以应用包含在它外层的函数的表达式
即使外层函数的执行已经终止
****注意***
该变量提供的值并非创建时候的值，而是父函数范围内的最终值
```csharp
class Test
{
	public event Action action;
	public Test()
	{
		int value = 10;
		action = () =>
		{
		//这里就形成了闭包
		//因为当构造函数执行完毕时 其中声明的零食变量value的声明周期就被改变了
			Console.WriteLine(value);
		};

		//1.增加For循环
		for(int i = 0 ; i <10; i++)
		{
			//2.声明一个临时的index变量
			int index = i;
			action += () =>
			{
				Console.WriteLine(index/*i*/);
			};
		}
	}	
	
	//由于声明了一个事件 所有不能在外部调用只能封装一个方法
	public void DoSomething()  
	{
		action();
	}
}
//————————————————————————Main
Test t = new Test(); 
t.DoSomething();  //打印结果为10
/*增加for循环后*/t.DoSomething();  //打印十次10
/*增加临时变量index后*/ t.DoSomething();  //打印0~9
```

# 练习
有一个函数 返回一个委托函数 这个委托函数中只有一句打印代码
之后执行返回的委托函数时 可以打印1~10
```csharp
static Action Fun()
{
	Action action = null;
	for(int i = 1 ; i<=10 ; i++)
	{
		int index = i;
		Console.WriteLine(index);
	}
	return action;
}
//————————————————————————Main
```