#委托和事件
# 什么是事件
事件是基于委托的存在
事件是委托的安全包裹
让委托的使用更具有安全感
事件 是一种特殊的==变量类型==

# 事件的使用
声明语法
`访问修饰符 event 委托类型 事件名;`
事件的使用
1. 事件是作为 成员变量存在于类中的
2. 委托于事件的 ***使用方法*** 几乎一致

事件相对于委托的区别
1. 不能在类外部 赋值
2. 不能再类外部 调用

注意
	它只能作为成员存在于类和接口以及结构体中
```csharp
class Test{
	//委托成员变量 用来存储 函数的
	public Action myFun;
	//事件成员变量 用来存储 函数的
	public event Action myEvent;
	
	public Test(){
		//事件的使用和委托一模一样 只是有些细微的区别
		myFun = TestFun;
		myFun += TestFun;
		myFun -= TestFun;
		myFun.Invoke();
		myFun();
		myFun = null;
		
		myEvent = TestFun;
		myEvent += TestFun;
		myEvent -= TestFun;
		myEvent.Invoke();
		myEvent();
		myEvent = null;
	}
	public void TestFun(){
		Console.WriteLine("123");
	}
	
	//想要在外部使用事件只能封装一个方法
}
//————————————————————————Main
Test t = new Test();
//委托是可以在外部赋值的
t.myFun = null;
t.myEvent = TestFun;

//委托可以在外部调用的
t.myFun();  
t.myFun.Invoke();
```
==事件无法在外部赋值==
```csharp

//————————————————————————Main
~~t.myEvent = null;~~  //不允许赋值 这里报错
//只能+=或者-=
t.myEvent += null;
t.myEvent -= null;
//并且只能是+=/-=必须是符合运算符不能
t.myEvent = t.myEvent + null;
```
==事件无法在外部调用==
```csharp

//————————————————————————Main
~~t.myEvent.Invoke()~~;  //不允许在外部调用 这里报错
~~t.myEvent();~~
```

# 如果想要在外部调用事件只能封装一个方法
```csharp
class Test{
	public event Action myEvent;
	public void DoEvent(){
		if(myEvent != null){
			myEvent();
		}
	}
}
//————————————————————————Main

```

# 为什么有事件
1. 防止外部随意指控委托
2. 防止外部随意调用委托
3. 事件相当于对委托进行了一次封装，让其更安全