#委托和事件 #delegate
# 什么是委托
委托是一个装载==函数==的容器 可以理解为是个表示函数（方法）的变量类型
可以用来***存储，传递***函数（方法）
委托的本质是一个类，用来定义函数的类型（返回值和参数的类型）
不同的是 函数（委托）必须对应各自的 ”格式“ 一致的委托

关键字`delegate` 
写在`namespace`与`class`中 更多写在namespace中 写在class中需要点出来使用

# 基本语法
访问修饰符 delegate 返回值 委托名 （参数列表）
`public delegate void Fun();`
访问修饰符不写默认为`public`可不写

# 自定义委托
```csharp
namespace
{
	delegate void Myfun();  //将无参无无返回值的装进来
	delegate int Myfun2(int a);  //将有参有返回值的函数的装进来
	
    internal class Program
    {
        static void Main(string[] args)
        {
	        //委托类名 委托名 = new 委托类名（函数名）；
	        //必须是一个无参无返回值的函数
            Myfun f = new Myfun(Fun);
            f.Invoke()  //直接调用.Ivoke();

			Myfun f2 = Fun;  //第二种声明方法
			f2();  //直接调用 委托名（）；
			//——————————————————————————————————————————
			Myfun2 f3 = Fun2();  //装载有一个参数和有返回值的函数
			console.writeline(f3(3));  //打印结果3

			MyFun2 f4 = Fun2;
			Console.WriteLine(f4.Invoke(2));  //同上一种方法
        }

		static void Fun(){
			console.writeline("张三做了什么");
		}
		static int Fun2(int value){
			return value
		}
    }
}
```

## 使用定义好的委托
委托变量是函数的容器

委托常用在
1.作为类的成员
2.作为函数的参数
```csharp
namespace
{
	delegate void Myfun();  //将无参无无返回值的装进来
	delegate int Myfun2(int a);  //将有参有返回值的函数的装进来
	
    internal class program
    {
		class Test{
			public MyFun fun;
			public MyFun2 fun2;

			public void TestFun(MyFun fun,MyFun2 fun2){
				//先处理一些别的逻辑 当这些逻辑处理完了 在执行传入的函数
				int i = 1;
				fun();  //直接调用
				fun2(i);
				this.fun = fun;  //存储起来之后再调用
				this.fun2 = fun2;
			}
		}
		
        static void Main(string[] args)
        {
            Test t = new Test();
            t.TestFun(Fun,Fun2);  //打印张三做了声明   4
	        
        }

		static void Fun(){
			console.writeline("张三做了什么");
		}
		static int Fun2(int value){
			return value
		}
    }
}
```

## 使用委托存储多个函数（执行多次）
加什么执行什么 加一次执行一次 加两次执行两次 按顺序执行
==加==
```csharp
namespace
{
	delegate void Myfun();  //将无参无无返回值的装进来
	delegate int Myfun2(int a);  //将有参有返回值的函数的装进来
    
    internal class program
    {
        static void Main(string[] args)
        {
            MyFun ff = null;  //MyFun ff = Fun;
            // ff = ff + Fun;
            ff += Fun;
            ff += Fun3;
            ff();  //打印”张三做什么“ ”小曾做什么“
            
            ff += Fun;
            ff();  //打印”张三做什么“ ”小曾做什么“ ”张三做什么“
        }

		static void Fun()
		{
		    Console.WriteLine("张三做什么");
		}

		static void Fun3()
		{
		    Console.WriteLine("小曾做什么");
		}
    }
}
```
==减==
```csharp
namespace
{
	delegate void Myfun();  //将无参无无返回值的装进来
	delegate int Myfun2(int a);  //将有参有返回值的函数的装进来
    
    internal class program
    {
        static void Main(string[] args)
        {
            MyFun ff = null;  //MyFun ff = Fun;
            ff();  //打印”张三做什么“ ”小曾做什么“ ”张三做什么“
            
            //——————————————————- 上方是加声明过的 下方才是减
			
            ff -= Fun  //从容器中移除指定函数
			ff -= Fun;//多减不会报错 无非就是不处理而已
			ff();  //打印”打印小曾在做什么“
			//清空容器
			ff = null;
			if(ff != null){  //如果ff为空执行时会报错
				ff();
			}
        }

		static void Fun()
		{
		    Console.WriteLine("张三做什么");
		}

		static void Fun3()
		{
		    Console.WriteLine("小曾做什么");
		}
    }
}
```

## 委托变量可以存储多个函数
```csharp
class Test
{
    public MyFun fun;
    public MyFun2 fun2;
    public Action action;
    //增
    public void AddFun(MyFun fun, MyFun2 fun2)
    {
        this.fun += fun;
        this.fun2 += fun2;
    }
    //删
    public void Remove(MyFun fun,MyFun2 fun2)
    {
        this.fun -= fun;
        this.fun2 -= fun2;
    }
}
//————————————————————————Main
```

# 系统定义好的委托
引用命名空间`using System`
```csharp

//————————————————————————Main
Action action = Fun;  //Action存储无参无返回值的函数
action += Fun3;
action();  //返回”小曾做什么“

//**********************************
Func<string> funStrng = Fun4;  //自定义返回类型无参（泛型委托）
Func<int> funInt = Fun5;
static int Fun5(){
	return 1;
}

//**********************************
Action<int,string> action2 = Fun6;  //可以传n个参数的无返回函数 系统提供的1~16个参数的委托 直接用就行
static void Fun6(int a ,string s){
	
}

//**********************************
Func<int,int> func2 = Fun2;//可以传n个参数的 并且有返回值的 系统也准备好了
//也可以传1~16个参数 第17个参数就是返回值(最后一个变量类型是返回类型)
static int Fun2(int value)
{
    return value;
}
```

# 当用有返回值的委托容器存储多个函数
解决问题：
如果想要获取到每一个函数执行后的返回值
委托容器中存在方法GetInvocationList()可以返回一个委托数组
*无返回值*
```csharp
static void Method1{
	console.writeline("Method1");
}
static void Method1{
	console.writeline("Method1");
}
static void Method1{
	console.writeline("Method1");
}
//————————————————————————Main
Action myDelegate = null;
//绑定多个方法到委托中
myDelegate += Method1;
myDelegate += Method2;
myDelegate += Method3;

Delegate[] invocationList = myDelegate.GetInvocationList();  //绑定方法的列表
//遍历并逐一调用
foreach(Action del in invocationList)
{
	del();   //输出
}
//输出 Method1
	 //Method2
	 //Method3


//也可以直接调用
del();
//输出 Method1
	 //Method2
	 //Method3
```
但是无返回值的委托就可以直接省略绑定方法列表之后的流程 可以直接`myDelegate();`

但是如果是有返回值的话就只能使用`GetInvocationList();`
```csharp
static int Method5()
{
    return 10;
}
static int Method4()
{
    return 20;
}
//————————————————————————Main
Func<int> myDelegate2 =null;
myDelegate2 += Method4;
myDelegate2 += Method5;
Delegate[] invocationList2 = myDelegate2.GetInvocationList();
foreach (Func<int> item in invocationList2)
{
	//int index = (del as Func<int>)();  也可以这样
	int index = item();
	Console.WriteLine($"方法返回的结果{index}");
}
	//打印的结果为
	//方法打印的结果10
	//方法打印的结果20

/*是不能*/Console.WriteLine(myDelegate2());/*的否则*/
//打印的结果为 方法打印的结果10
//没有 方法打印的结果20
```

# Delegate和delegate的区别
`Delegate` 是C#中定义的一个类`System.Delegate` 它是所有委托类型的父类（基类） 提供了委托功能的基础实现
`delegate` 是一个关键字 用于声明委托类型


# 总结
总结
委托就是装载 传递 函数的容器而已
可以用委托变量 来存储函数或者传递函数的
系统其实已经提供了委托给我弄用
Action没有返回值 参数提供了1~16个委托给我们用
Func有返回值 也提供了16个给我们用