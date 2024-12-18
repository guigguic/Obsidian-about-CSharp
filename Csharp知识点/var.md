`var` 是 C# 中的一个关键字，用于声明**隐式类型**的变量。
使用 `var` 让编译器根据变量的赋值内容来自动推断变量的类型。
这在编写代码时可以减少类型声明的冗长，
但变量的类型仍然是编译时确定的，不是动态类型。
它可以是任何类型
实例
```csharp
var age = 10; //编译器判断为int类型
var name = "alice";  //编译器判断为string类型
var array = new int[]{1,2,3};
var list = new List<int>();
```
- `var` 的优点是使代码简洁，特别是对于复杂类型和泛型类型时，能够减少代码冗长，简化类型声明。

- `var` 的缺点则在于可能降低代码可读性，特别是在类型不直观或推断失败时，可能会导致理解上的困难或错误。

# 匿名变量
`var`变量可以声明为自定义的匿名类型
```csharp
//————————————————————————Main
var v = new{age = 10,money = 11,name = "小明"};
Console.WriteLine(v.age);
Console.WriteLine(v.money);
Console.WriteLine(v.name);
```