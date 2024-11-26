[[List列表|List基本知识]]

其实在c#中已经为我们提供了list排序的方法 但是其涉及到*委托*的知识点 所以单独列出来了
，且使用非常简单
**关键字** ： `.Sort();`
# List自带的排序方法
声明`Add`
```csharp
//————————————————————————Main
List<int> list = new List<int>();
list.Add(3);
list.Add(2);
list.Add(6);
list.Add(1);
list.Add(4);
list.Add(5);
for (int i = 0; i<list.Count;i++){
	Console.WriteLine(list[i]);
}   //打印3 2 6 1 4 5
```
***List提供的方法***`.Sort();`
```csharp
//————————————————————————Main
list.Sort();  //这个就是排序的关键字 现在已经排序好了
for (int i = 0; i < list.Count; i++)
    Console.WriteLine(list[i]);  //打印1 2 3 4 5 6
```
*`ArrayList`也有一样的 方法*

# 自定义类排序
此方法是通过继承`IComparable接口`来重写`CompareTo`的方法让我们能直接使用`Sort`
*声明*
```csharp
class Item: IComparable<Item> {
	public int money;
	public Item(int money){  //构造函数 表示传入的钱
		this.money = money;
	}

	public int CompareTo(Item other){
		if(this.Money > other.money){
			return 1;
		}
		else{
			return -1;
		}
		~~return 0;~~  /*可有可无*/
	}
}
//————————————————————————Main
List<Item> itemList = new List<Item>();
itemList.Add(new Item(45));
itemList.Add(new Item(10));
itemList.Add(new Item(99));
itemList.Add(new Item(24));
itemList.Add(new Item(100));
itemList.Add(new Item(12));
//在Item自定义函数中重写了 CompareTo函数 就可以直接使用Sort方法了
itemList.Sort();
//打印结果10 12 24 45 99 100
```

# 通过委托函数进行排序
*声明*
```csharp
class ShopItem{
	public int id;
	public ShopItem(int id){
		this.id = id;
	}
}
//——————————————————————Main
List<ShopItem> shopItems = new List<ShopItem>();
shopItems.Add(new ShopItem(1));
shopItems.Add(new ShopItem(6));
shopItems.Add(new ShopItem(3));
shopItems.Add(new ShopItem(5));
shopItems.Add(new ShopItem(2));
shopItems.Add(new ShopItem(4));
```

*方法1 `.Sort();` 中传入函数*
```csharp
static int SorShopItem (ShopItem a,ShopItem b){
	if(a.id > b.id){
		return 1;
	}
	else{
		return -1;
	}
}
//————————————————————————Main
shopItems.Sort(SorShopItem);  //委托的知识点 装载函数
```

*方法2 通过[[匿名函数]]*
```csharp
//————————————————————————Main
shopItems.Sort(delegate(ShopItem a,ShopItem b){
	reutrn a.id > b.id ? 1: -1;  //三目运算符 
}
```

*方法3 通过`Lambad表达式`*
```csharp
//————————————————————————Main
shopItems.Sort((a,b)=>{
	reutrn a.id > b.id ? 1: -1;  //三目运算符 
});
//或者
shopItems.Sort((a,b) =>{reutrn a.id > b.id ? 1: -1;});  //一行 显得高大上
```

***遍历***
```csharp
//————————————————————————Main
for(int i = 0; i<shopItems.Count;i++)
	Console.WriteLine(shopItems[i].id);
```

# 总结
系统自带的变量（int,float.double...）一般都可以直接Sort
自定义类Sort有两种方法
1.继承结构 IComparable
2.在Sort中传入委托函数

传入的两个对象 为列表中的两个对象
进行两两的比较 用左边的和右边的条件 比较
返回值规则 和之前一样 0做标准 负数在左（前） 正数在右（后）

# 练习
## 练习1
写一个怪物类 创建十个怪物将其添加到List中对List列表进行排序
根据用户输入数字进行排序
1. 攻击排序
2. 防御排序
3. 血量排序
4. 反转

*声明*
```csharp
class Monster{
	public static int SortType = 1;  //输入一个静态的排序种类

	public int atk;
	public int def;
	public int hp;

	public Monster(int atk,int def,int hp){  //声明一个构造函数
		this.atk = atk;
		this.def = def;
		this.hp = hp;
	}

	public override string ToString(){  //重写ToString方法
		return string.Format
			($"怪物信息，攻击力{atk}，防御力{def}，血量{hp}");
	}
}
//————————————————————————Main
List<Monster> monsters = new List<Monster>();
Random r = new Random();  //随机数
for(int i = 0;i<10;i++){  //声明十个怪物
	monsters.Add(new Monster
		(r.Next(5,21).r.Next(100,201),r.Next(2,10)));
}
try{
	Console.WriteLine("请输入1-4的数字进行排序");
	Console.WriteLine("1：按攻击力进行排列");
    Console.WriteLine("2：按防御力进行排列");
    Console.WriteLine("3：按血量进行排列");
    Console.WriteLine("4：反转");
}
catch{

}
```

*方法1*
List反转的API`.Reverse();`  反转List的内容
```csharp

//————————————————————————Main
try{
	int inputIndex = int,Parse(Console.ReadLine());
	switch(inputIndex){
		case 1:
			monsters.Sort((a,b)=>{return a.atk > b.atk> 1: -1;});
			break;
		case 2:
			monsters.Sort((a,b)=>{return a.def > b.def> 1: -1;});
			break;
		case 3:
			monsters.Sort((a,b)=>{return a.hp > b.hp> 1: -1;});
			break;
		case 4:
			monsters.Reverse();
			break;
	}
}
catch{
	Console.WriteLine("请输入数字");
}
```

*方法2*
利用静态成员变量 + 函数
```csharp
static int SortFun(Monster m1,Monster m2){
	switch(Monster.SortType){
		case 1:
		    return m1.atk > m2.atk ? 1 : -1;
		case 2:
		    return m1.def > m2.def ? 1 : -1;
		case 3:
		    return m1.hp > m2.hp ? 1 : -1;
	}
	return 0;
}
//————————————————————————Main
try{
	Monster.SortType = int.Parse(Console.ReadLine());
	if(Monster.SortType)
		monsters.Reverse();
	else
		monsters.Sort(SortFun);
}
catch{
	Console.WriteLine("请输入数字");
}
```

## 练习2
写一个物品类(类型，名字，品质)，创建10个物品添加到List中
同时使用类型、品质、名字长度进行比较
排序的权重是:类型>品质>名字长度

*声明*
```csharp
class Items{
	public int type;
	public string name;
	public int rank;
	public Items(int type,string name,int rank){
		this.type = type;
		this.name = name;
		this.rank = rank;
	}
	public override string ToString(){
		return string.Format
			($"物品类型{type}，物品名称 {name}，物品品质{rank}");
	}
}
//————————————————————————Main
List<Items> item = new List<Items>();
Random r = new Random();
for(int i = 0; i<10;i++){
	item.Add(new Items
		(r.Next(1, 6), "itme" + r.Next(1,255),r.Next(1,6)));
}
```

*方法1*
```csharp
//————————————————————————Main
itmes.Sort((a,b) =>{
	if(a.type != b.type){  //按种类比较
		return a.type > b.type ? -1 : 1;	
	}
	else if(a.rank != b.rank){  //按品质比较
		return a.rank > b.rank ? -1 ; 1;
	}
	else{  //按名称长度比较
		return a.name.Length > b.name.Length ? -1 : 1;
	}
});
```

## 练习3
请尝试利用List排序方式对Dictionary中的内容排序提示:
得到`Dictionary`的所有键值对信息存入List中
这个知识点会用到另一个语言的对象 `linq `就是`SQL`数据库的东西
[[Dictionary字典#^1b421e|KeyValuePair]]
```csharp
//————————————————————————Main
Dictionary<int,string> dic = new Dictionary<int,string>();
dic.Add(2, "123");
dic.Add(5, "123");
dic.Add(1, "123");
dic.Add(4, "123");
dic.Add(6, "123");
dic.Add(3, "123");

List<KeyValuePair<int, string>> keyValues =
    new List<KeyValuePair<int, string>>();

foreach (KeyValuePair<int,string> item in dic)
{
    keyValues.Add(item);
    Console.WriteLine(item.Key + "_" +item.Value);
}
Console.WriteLine("--------------");
keyValues.Sort((a, b) =>
{
    return a.Key > b.Key ? 1 : -1;
});

for (int i = 0; i < keyValues.Count; i++)
{
    Console.WriteLine
        (keyValues[i].Key + "_" + keyValues[i].Value);
}
```