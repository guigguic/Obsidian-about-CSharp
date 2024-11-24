#常用泛型数据结构类
Dictionary/字典
# Dictionary的本质
可以将Dictionary理解为 拥有[[泛型]]的[[Hashtable哈希表|Hashtable]]
它也是基于键的哈希代码组织起来的 键/值对
键值对类型从Hashtable的object变为了可以自己定制的泛型

# 申明
需要引用`System.Collection.Generic`
需要填两个 一个键的类型 一个值的类型
`Dictionary<int,string> dictionay = new Dictionary<int,string>();`

# 增删查改
## 增
==注意：不能出现相同的键==
也需要填两个 一个键 一个值
```csharp
//————————————————————————Main
dictionay.Add(1, "123");
dictionay.Add(2, "222");
dictionay.Add(3, "333");
```

## 删 
```csharp

//————————————————————————Main
//1.只能通过键去删
//  删除不存在的键是没反应的
dictionay.Remove(1);
//2.清空
dictionay.Clear();

dictionay.Add(1, "123");
dictionay.Add(2, "222");
dictionay.Add(3, "333");
```

## 查
```csharp

//————————————————————————Main

//1.通过键查看值
//找不到会返回空
Console.WriteLine(dictionay[2]);
Console.WriteLine(dictionay[1]);

//2.查看是否存在
//  根据键检测
if (dictionay.ContainsKey(1))
{
    Console.WriteLine("有的");
}
//  根据值的
if (dictionay.ContainsValue("123"))
{
    Console.WriteLine("有的");
}
```

## 改
```csharp

//————————————————————————Main
dictionay[1] = "10086";
```

# 遍历
遍历所有键
```csharp

//————————————————————————Main
foreach(int item in dictionay.Keys)
{
    Console.WriteLine(item);
}
```

遍历所有值
```csharp

//————————————————————————Main
foreach (string item in dictionay.Values)
{
    Console.WriteLine(item);
}
```

键值对一起遍历
```csharp

//————————————————————————Main
foreach (KeyValuePair<int,string> item in dictionay)
{
    Console.WriteLine($"键{item.Key} 值{item.Value}");
}
//——————————————————————————————或者
foreach(var item in dictionary.keys){
	console.writeline($"键{item}值{dictionay[item]}");
}
```

^1b421e

# 练习1
使用字典存储0~9的数字对应的大写文字
提示用户输入一个不超过三位的数，
提供一个方法，返回数的大写例如: 306，返回参零陆
```csharp
static string Sum(int num){
	Dictionary<int,string> dic = new Dictionary<int,string>();
	dic.Add(0, "零");
	dic.Add(1, "壹");
	dic.Add(2, "贰");
	dic.Add(3, "叁");
	dic.Add(4, "肆");
	dic.Add(5, "伍");
	dic.Add(6, "陆");
	dic.Add(7, "柒");
	dic.Add(8, "捌");
	dic.Add(9, "玖");

	string str = "";
	//得到百位
	int b = num /100;
	str += dic[b];
	//得到十位
	int s = num %100 /10;
	str += dic[s]
	//得到个位
	int g = num %10;
	str += dic[g];

	return str;
}
//————————————————————————Main
console.writeline(Sum(int.parse(console.readline())));
```

# 练习2
计算每个字母出现的次数“Welcome to Unity World!
"使用字典存储，最后遍历整个字典，不区分大小写

```csharp
//————————————————————————Main
//<字母,次数>
Dictionary<char,int> dic = new Dictionary<char,int>();
string str = "Welcome to Unity World";
str = str.Tolower();  //将str转成小写
for(int i = 0; i <str.length;i++){
	if(dic.ContainsKey(str[i])){  //如果字典中没有查到键就进else
		//如果dic用键查找找到了str的第i个元素比如Welcome的e
		//就进这个逻辑
		dic[str[i]] +=1;
		//dic[str[i]] = dic[str[i]] + 1;
		//dic的第str[i]的键值对+1
	}
	else
	{
		dic.add(str[i],1);  //增加一个键，默认次数为1
	}
}
foreach(char item in dic.Keys)
{
	console.writeline($"字母{item}键{dic[item]}");
}
```
