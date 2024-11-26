# Haschtable的本质
Hashtable（又称散列表，哈希表）是基于键的哈希代码组织起来的  键/值对
它的主要作用是提高数据查询的效率
使用键来访问集中的元素

# 声明
引用命名空间 `System.Collections`
`Hashtable hashtable = new Hashtable();`

# 增删查改遍历

## 增
```csharp
hashtable.Add(1, "123");    //左边为键 右边为值
hashtable.Add("123", 2);
hashtable.Add(true,false);
hashtable.Add(false,false);
//注意：不能出现相同的键
```

## 删
```csharp
//1.只能通过键取删除
hashtable.Remove(1);
//2.删除不存在的键 没反应
hashtable.Remove(2);
//3.直接清空
hashtable.Clear();
hashtable.Add(1, "123");
hashtable.Add(2, "1234");
hashtable.Add(3, "123");
hashtable.Add("123123", 12);
```

## 查
```csharp
//1.通过键查看值  找不到会返回空
Console.WriteLine(hashtable[1]);
Console.WriteLine(hashtable[4]);    //null
Console.WriteLine(hashtable["123123"]);

//2.查看是否存在
//根据键去检测
if (hashtable.Contains(1))
{
    Console.WriteLine("存在键为1的键值对");
}
if (hashtable.ContainsKey("123123"))
{
    Console.WriteLine("存在键为123的键值对");
}

//根据值检测
if (hashtable.ContainsValue(12))
{
    Console.WriteLine("存在值为12的键值对");
}
```

## 改
```csharp
//只能改 键对应的值内容 无法修改键
Console.WriteLine(hashtable[1]);
hashtable[1] = 100.5f;
Console.WriteLine(hashtable[1]);
```

## 遍历
1.遍历所有的键
```csharp
foreach (object item in hashtable.Key){
	console.writeline("键" + item);
	console.writeline("值" + hashtable[item]);
}
```

2.遍历所有值
```csharp
foreach (object item in hashtable.values){
	console.writeine(item);	
}
```

3.键值对一起遍历（做了解）
```csharp
foreach(DictionaryEntry item in hashtable){
	console.writeline($"键{item.key},值{item.value}");
}
```

4.迭代器遍历法（做了解）
```csharp
IDictionaryEnumerator myEn = hashtable.GetEnmerator();
bool flag = myEn.MoveNext();
while(flag){
	console.writeline(myEn.Key + " " + myEn.value);
	flag = myEn.MoveNext();
}
```

# 装箱拆箱
同[[继承#万物之父&装箱拆箱|万物之父]]

# 练习
写一个怪物管理器 ，提供创建怪物，移除怪物的方法，每个怪物都有自己的为一ID[[封装#单例模式#实例|单例模式]]
```csharp
public class MonsterMgr
{
    // 静态变量，保存唯一的 MonsterMgr 实例，直接在声明时初始化
    private static MonsterMgr instance = new MonsterMgr();

    // 哈希表，用于存储怪物信息
    private Hashtable monstersTable = new Hashtable();

    // 私有构造函数，阻止类在外部被实例化
    private MonsterMgr()    
    {
        // 可以在这里进行初始化工作，如加载怪物数据等
    }

    // 静态属性，外部通过此属性访问唯一的实例
    public static MonsterMgr Instance   
    {
        get
        {
            // 返回唯一实例
            return instance;
        }
    }

	private int monsterId = 0;
	public void AddMonster()
	{
	    Monster monster = new Monster(monsterId);
	    Console.WriteLine($"创建了id为{monsterId}的怪物");
	    ++monsterId;
	    //哈希table的键 是不能重复的 所以一定是用唯一id
	    monstersTable.Add(monster.id,monster);
	}

	public void RemoveMonster(int monsterId)
	{
	    if (monstersTable.ContainsKey(monsterId))
	    {
	        (monstersTable[monsterId] as Monster).Dead();
	        monstersTable.Remove(monsterId);
	    }
	}
}

class Monster
{
    public int id;
	
    public Monster(int id )
    {
        this.id = id;
    }
	
    //移除
    public void Dead()
    {
        Console.WriteLine($"怪物{id}死亡");
    }
}
//————————————————————————Main
MonsterMgr.Instance.AddMonster();
MonsterMgr.Instance.AddMonster();
MonsterMgr.Instance.AddMonster();
MonsterMgr.Instance.AddMonster();
MonsterMgr.Instance.AddMonster();
MonsterMgr.Instance.AddMonster();

MonsterMgr.Instance.RemoveMonster(0);
MonsterMgr.Instance.RemoveMonster(3);
```