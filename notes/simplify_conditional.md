### 1、Decompose Conditional (分解表达式)

动机：含有 if else 语句的函数往往特别冗长，因为每个判断语句下面都跟了一整个代码块。
做法：将每个判断语句下的代码块都抽离成一个独立的函数。

### 2、Consolidate Conditional Expression (合并表达式)

如果多个判断语句下的代码块是一样的，则应该将这几个条件语句合并在一起，用 “or” 连接。

### 3、Consolidate Duplicate Conditional Fragments (合并重复的条件判断)

如果条件式的每个分支上都有相同的代码段，则应该把相同的部分搬移到条件式之外。

### 4、Remove Control Flag (移除控制标记)

在循环语句中，如果某个变亮带有 「控制标记」的作用。那么应该直接用 break 或 return 语句替代控制标记。

例如，下方的 `done` 语句应该直接用 `break` 替代：
```
set done to false 
while not done 
	if (condition) 
		do something 
		set done to true 
	next step of loop
```

### 5、Replace Nested Conditional with Guard Clauses (用卫语句取代嵌套条件式)

多重判断条件的嵌套会影响可读性，卫语句不仅清晰明了，而且减少了圈复杂度。

如下：第二段代码采用卫语句，明显增加了可读性
```
double getPayAmount() { 
	double result; 
	if (_isDead) result = deadAmount(); 
	else {
		if (_isSeparated) result = separatedAmount(); 
		else {
			if (_isRetired) result = retiredAmount(); 
			else result = normalPayAmount(); 
		}; 
	} 
	return result; 
};
```

```
double getPayAmount() { 
	if (_isDead) return deadAmount(); 
	if (_isSeparated) return separatedAmount(); 
	if (_isRetired) return retiredAmount(); 
	return normalPayAmount(); 
};
```

### 6、Replace Conditional with Polymorphism (用多态取代条件式)

如果一串 `if-elif-else` 语句根据对象类型二选择不同的行为，
那么应该将每个分支下的语句快放进一个 subclass 内的覆写函数中，然后将原始函数申明为抽象函数。

对于下面一段代码，应该在三种对象的公共父类中申明抽象函数 getBaseSpeed()，然后在三个对象中分别实现，这样就避免了这个switch语句。
```
double getSpeed() { 
	switch (_type) { 
		case EUROPEAN: 
			return getBaseSpeed(); 
		case AFRICAN: 
			return getBaseSpeed() - getLoadFactor() * _numberOfCoconuts; 
		case NORWEGIAN_BLUE: 
			return (_isNailed) ? 0 : getBaseSpeed(_voltage); 
	}
	throw new RuntimeException ("Should be unreachable"); 
}
```

### 7、Introduce Null Object (引入Null对象)

`很有趣，值得关注`

**为了解决的问题：**我们在进行某些操作前，往往需要检查对象是否存在，这样的检查会出现很多次。例如我们会请求获取 person 对象，然后再判断 person 是否为空，然后再调用 person 对象的某个函数。

**什么是Null Object：** Null Object 往往和某个真正的 object 拥有一样的接口，但是返回的都是默认的值。

**如何做：**
- 为source class 建立一个subclass ，使其行为像source class 的null 版本。在source class 和null class 中都加上 isNull() 函数，前者的isNull() 应该返回false，后者的isNull() 应该返回true。 
- 下面这个办法也可能对你有所帮助：建立一个nullable 接口，将isNull() 函数放在其中，让source class 实现这个接口。
- 另外，你也可以创建一个testing 接口，专门用来检查对象是否为null。 
- 编译。 
- 找出所有「索求source object 却获得一个null 」的地方。修改这些地方，使它们改而获得一个null object。 
- 找出所有「将source object 与null 做比较」的地方。修改这些地方，使它们调用isNull() 函数。 
- 你可以每次只处理一个source object 及其客户程序，编译并测试后， 再处理另一个source object 。 
- 你可以在「不该再出现null value」的地方放上一些assertions（断言）， 确保null 的确不再出现。这可能对你有所帮 助。
- 编译，测试。 
- 找出这样的程序点：如果对象不是null ，做A动作，否则做B 动作。 
- 对于每一个上述地点，在null class 中覆写A动作，使其行为和B 动作相同。 
- 使用上述的被覆写动作（A），然后删除「对象是否等于null」的条件测试。编译并测试。


