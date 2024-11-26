#常用泛型数据结构类
极其类似ArrayList但是List更好 因为少了装箱拆箱 非必要情况下可以不用Arraylist
# List的本质
List是c#为我们封装好的类
它的本质是一个可变类型的==[[泛型]]数组==
List类帮我们实现了很多方法
比如泛型数组的增删查改

# List的声明
/需要引用命名空间 `System.Collection.Generic`
`<变量类型>`
```csharp
List<int> list = new List<int>();
List<string> list2 = new List<string>();
List<bool> list3 = new List<bool>();
//————————————————————————Main

```

# 增删查改
## 增
```csharp

//————————————————————————Main
list.Add(1);
list.Add(2);
list.Add(3);
list.Add(4);

list2.Add("123");
//list2.Add("123");
//list2.Add("123");

List<string> listStr = new List<string>();
listStr.Add("你好");
list2.AddRange(listStr);  //加在数组最后
//foreach (string s in list2)
//{
//    Console.WriteLine(s);
//}

list.Insert(3, 321);  //插入
Console.WriteLine(list[3]);
```

## 删
```csharp

//————————————————————————Main
//1.移除指定元素
//Console.WriteLine(list[0]); //打印1
list.Remove(1);
//Console.WriteLine(list[0]);  //打印2
//2.移除指定位置的元素
list.RemoveAt(0);
//Console.WriteLine(list[0]); //打印3
//3.清空
list.Clear();


list.Add(1);
list.Add(2);
list.Add(3);
list.Add(4);
```

## 查
```csharp

//————————————————————————Main
//1.得到指定位置的元素
Console.WriteLine(list[0]);
//2.查看元素是否存在
if (list.Contains(1))
{
    Console.WriteLine("有的");
}
//3.正向查找
//找到返回位置 找不到返回-1
int index = list.IndexOf(2);
Console.WriteLine(index);
//4.反向查找
//找到返回位置 找不到返回-1
index = list.LastIndexOf(2);
Console.WriteLine(index);
```

## 改
```csharp

//————————————————————————Main
list[1] = 999;
Console.WriteLine(list[1]);
```

# 遍历
```csharp

//————————————————————————Main
//长度
Console.WriteLine(list.Count);
//容量
Console.WriteLine(list.Capacity);

Console.WriteLine("——————————————————");
//遍历
for (int i =0; i < list.Count; i++)
{
    Console.WriteLine(list[i]);
}

//foreach
Console.WriteLine("——————————————————");
foreach (int i in list)
{
    Console.WriteLine(i);
}
```

# 练习
-个Monster基类，Boss和Gablin类继承它   在怪物类的构造函数中，
将其存储到一个怪物List中遍历列表可以让Boss和Gabfin对象产生不同攻击
```csharp
abstract class Monster{
	//<Monster>指的是monster类及Monster类的子类
	public static List<Monster>monsters = new List<Monster>();
	public Monster{
		Monster.Add(this);//子类实例化时，会先默认使用父类的无参构造函数
		//this指的是monster类及Monster类的子类
	}
	public abstract void Atk();
}

class Boss:Monster{
	public override void Atk(){
		console.writeline("Boss的攻击");
	}
}
class Gablin : Monster{
	public override void Atk(){
		console.writeline("Gablin的攻击");
	}
}
//————————————————————————Main
Boss b = new Boss();
Gablin g = new Gablin();
Boss b2 = new Boss();
Gablin g2 = new Gablin();

for (int i = 0; i < Monster.mosnters.Count; i++)
{
    Monster.monsters[i].Atk();
}
```

# HackerRank1
“Alice 和 Bob 的问题”是指他们分别设计了一些挑战题目，每道题目都有三个评分指标：**题目清晰度 (clarity)**、**原创性 (originality)** 和**难度 (difficulty)**。Alice 和 Bob 的每道题目都会被评审打分，每个评分范围是 1 到 100，最终目的是比较他们的评分来确定谁的题目更好。
### 对题目的核心理解：
- **评分结构**：Alice 的题目有三个评分组成一个三元组，例如 a=[a[0],a[1],a[2]]a = [a[0], a[1], a[2]]a=[a[0],a[1],a[2]]，分别对应清晰度、原创性和难度。同样，Bob 的题目评分是 b=[b[0],b[1],b[2]]b = [b[0], b[1], b[2]]b=[b[0],b[1],b[2]]。
- **得分规则**：
    - 如果 a[i]>b[i]a[i] > b[i]a[i]>b[i]，Alice 得 1 分。
    - 如果 a[i]<b[i]a[i] < b[i]a[i]<b[i]，Bob 得 1 分。
    - 如果 a[i]=b[i]a[i] = b[i]a[i]=b[i]，双方都不得分。
- **任务**：计算 Alice 和 Bob 的最终得分，输出他们各自的分数。

简单来说，这个问题是一个 **评分比较问题**，核心是基于对评分的逐项对比，确定两人的优劣

```csharp
public static List<int> compareTriplets(List<int>a,List<int>b){
	int aliceScore = 0;
	int bobScore = 0;
	for(int i =0;i<3;i++){
		if(a[i]>b[i]){
			aliceScore++;
		}
		else if(a[i]<b[i]){
			bobScore++;
		}
	}
	return new List<int>{aliceScore,bobScore};
}
//————————————————————————Main

```