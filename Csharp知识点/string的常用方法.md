# string的常用方法
[[变量类型#^1df315|字符串]]
[[封装#^665670|索引器]]
[[数组]]
	[[数组#一位数组的增删查改|数组的增删查改]]

字符串本质是char数组
```csharp
string str = "曾同学";
Console.WriteLine(str[0]);
//打印结果为"曾"
```

转为char数组
```csharp
char[] chars = str.ToCharArray();
```

获取字符长度
```csharp
str.Length
```

字符串拼接
```csharp
str = string.Format("{0}{1}",1,222);
```

正向查找字符位置 
```csharp
str = "我是曾同学？";
int index = str.IndexOf("曾");
//返回 2 字符串的索引 , 找不到就会返回-1
```

反向查找字符位置
```csharp
str = "我是曾同学苏同学？";
index = str.LastIndexOf("曾同学");
//返回 5 从后面开始查找词组就返回第一个字的索引，找不到就返回-1
```

移除指定位置后的字符
```csharp
str = "我是曾同学苏曾学";
str = str.Remove(4);
//返回 "我是曾同"
```

执行两个参数进行移除 参数1开始的位置 参数2字符个数
```csharp
str = "我是曾同学陈同学";
str = str.Remove(3,3);
//返回"我是陈同学" 
```

替换指定字符串
```csharp
str = "我是曾同学陈同学";
str = str.Replace("曾同学","李同学");
//返回"我是李同学陈同学" 
```

大小写转换
```csharp
str = "abcdefg";
str = str.ToUpper();
//返回"ABCDEFG"
str = str.ToLower();
//返回"abcdefg"
```

字符串截取 截取从指定位置开始之后的字符串
```csharp
str = "曾同学陈同学";
str = str.Substring(3);
//返回 "陈同学"
//重载 参数1开始位置 参数2指定个数
str = "曾同学陈同学曾同学";
str = str.Substring(3,3);
//返回 "陈同学"
```

字符串切割 指定切割符号来切割字符串
```csharp
str = "1|2|3|4|5|6|7|8";
string[] strs = str.Split("|");
//返回 string[]{1,2,3,4,5,6,7,8}
```

# StringBuilder
==解决多次修改string性能消耗问题== : [[值和引用类型#特殊的引用类型string|有什么性能消耗]](每次重写赋值或者拼接会分配新的内存空间)
如果一个字符串经常改变会非常浪费空间
引用命名空间 : System.Text
关键字 : StringBuilder
容量问题 每次增加时都会自动扩容
无法直接赋值要先清空在清空
完全具备[[值和引用类型#^db7e81|值类型]]的特征,没有值类型特征了
```csharp
using System.Text;
//------------------ Main
StringBuilder strb = new StringBuilder("123132132");
//获得容量
int a = strb.Capacity;
//默认为16现在已经用了9 自动扩容会x2 变成32 64 128....
```

## 增删查改替改
声明
```csharp
StringBuilder strBui = new StringBuilder("123123123");
```

增
```csharp
strBui.Append("444");
//结果为  "123123123444"
strBui.AppendFormat("{0}{1}",555,666);
//结果为  "123123123444555666"
```

插入 参数1插入的位置 参数2插入的内容
```csharp
strBui.Insert(0,"曾同学");
//结果为  "苏同学123123123444555666"
```

参数1删除开始的位置 参数2删除的个数
```csharp
strBui.Remove(0,3);
//结果为  "123123123444555666"
```

清空
```csharp
strBui.Clear();
//结果为 ""
```

重新赋值 先清空再增加 
```csharp
strBui.Clear();
strBui.Append("曾同学");
```

查 和数组一样
```csharp
strBui[1];
//结果为 "同"
```

改 和数组一样
```csharp
strBui[0]='李';
//strBui结果为 "李同学"
```

替换 参数1被替换的字符  参数2要替换的内容
```csharp
strBui.Replace("同学","老师");
//strBui结果为 "李老师"
```

判断是否相等
```csharp
strBui.Equals("李老师");
//返回为 true
```