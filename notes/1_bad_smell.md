### Duplicate Code

如果你在一个以上的地点看到相同的程序结构，就应该考虑将它们合而为一。通常做法是 Extract Method。
### Long Method

如果能给函数都起个好名字，读者就可以通过名字了解函数的作用，根本不必去看其中写了些什么。
每当感觉需要以注释来说明点什么的时候，我们就把需要说明的东西写进一个独立函数中，并以其用途（而非实现手法）命名。通常做法是 Extract Method.
### Large Class

如果一个class很熟过大例如超过500行，就说明它做了太多的事情，需要考虑运用 Extract Class 将变量和方法提炼至新的 class里。
对于 Android 代码来说，使用 MVVM 结构将UI操作和数据操作分离是最常用的方式。
### **Long Parameter List**

太长的参数列难以理解、不易使用。通常做法是 Introduce Parameter Object，或 Replace Parameter with Method。
### Divergent Change

指一个class承担了多个不同的任务，通常做法是 剥离成两个 class 分别负责不同的任务
### Shotgun Surgery

与 Divergent Changes 相反，指每遇到某种变化，你就必须再许多不同的classes内做小修改。如果需要修改的代码散布四处，你不但很难找到它们，也很容易忘记某个重要的修改。通常做法是吧相关的 fieled 和 method 移到同一个 class。
### **注**：

Divergent Change是指「一个class受多种变化的影响」，
Shotgun Surgery则是指「一种变化引发多个classes相应修改」。
这两种情况下你都应整理代码，使「外界变化」与「修改的类」呈现一对一关系的理想境地。
### Feature Envy

指一个 method 引用了过多不属于它的 host class 的数据。通常做法是将这个 method 移到另一个 class 里，或者运用 Extract Method 抽出一个函数放到另一个 class里。
### Data Clumps

如果某些数据总是容易同时出现，那么就可以考虑运用 Extract Object 将他们整合进一个新的 class 里。这可以有效缓解 Long Parameter List。之后你还可以寻找 Feature Envy，把某些 method 移到这个新的class里。
### Primitive Obsession

指开发人员不愿意将一些紧密相关的值域集合成一个小对象。例如一个range的起始值合结束值。
### Switch Statement

要尽量避免使用switch语句。通常做法是用多态代替switch判断。
### Parallel Inheritance Hierarchies

是 Shutgun Surgery 的一种特殊情况，指的是每当你为一个class添加一个subclass的时候，你都必须再为另一个class添加一个subclass。通常做法是让其中一个class引用另一个class，再运用 move metod 和 move field 拆散两个 class 间的联系。
### Lazy Class

每个class都会耗费开发人员的精力去理解和维护，那些没有承担太多工作，不太必要的 class 就是lazy class。这种class需要想办法消灭，比如运用 Collapse Hierarchy，或替换成 inline class。
### Speculative Generality

指未来应付某种可能出现的场景而写的class 或 method，实际上这些功能最终很可能用不上。这违背了YAGNI原则，遇到这种代码就应该想办法删除掉。
### Temporary Field

指class 内存在大量的，只有少数method才会使用的field。成因往往是因为开发人员不想给这些 method 传太多的参数，所以把这些参数否放在了类的值域里。解决方案是你可以把这些 field 和相关 methld 提到一个单独的 class 里，这个 class 此时只负责对外提供这几个方法。
### Message Chains

指一个对象A向另一个对象B索要对象C，对象C再向对象D索要。这在程序中通常表现为一长串的 getXXX()。通常解决方法是先观察最终需要的到底是哪个对象，再把获取这个对象的功能提成一个函数放在这些class都能拿得到的地方。
### Middle Man

指一个 class 中很大一部分函数都只是在简单地调用另一个 class 的方法，而没有实现自己的逻辑。通常解决方法是删除这个middle man，让调用方和实际被调用方接触，或将这些函数变成 inline method。如果希望保存其他的函数，则可以让 middle man 继承被调用方，然后专心实现自己的函数就可以了。
### Inappropriate Intimacy

指两个 class 对对方的 private field 太过于感兴趣，通常发生在subclass 和 superclass 之间。可以通过移动方法和变量使他们划清界限，或让他们从双向依赖变成单向依赖。也可以将两者共同点提炼到一个新的类中，让二者引用这个新的类。
### Alternative classes with different interfaces

指两个class从外在看来不同，但实际却实现了类似的功能，是一种 duplicate，违背了 DRY 原则。解决方法是提炼二者的共同点作为他们二者的 superclass。
### Incomplete Library Class

指功能无法满足要求的 Library Class。如果只希望修改一两个函数的表现，可以自己实现一个函数来包裹library 的方法。如果希望修改的函数很多，可以继承 Library Class.
### Data Class

指纯数据类，没有对内部数据进行保护和封装，也没有集成任何相关的操作函数。我们需要对这种类进行完善：看看Collection类的值域是否被良好封装；修改数据可见性，移除不当的set方法；查看是哪些方法在使用这些数据，把它们种常用的部分提取成函数放到这个类中。
### Refused Bequest

指subclass继承了superclass，但是又不希望使用superclass的一些值域或方法或接口。一种解决方法是将subclass不需要的部分从superclass里抽出来，成为一个siblingClass，让superclass只保留两者共同的部分。另一种方法是 Replace Inheritanc With Delegation，让 原superclass 成为 原subclass 一个值域不过这会造成更复杂的继承体系。所以并不意味着每次都要重构，一般来说如果仅仅是不需要某几个值域或方法，其实不必重构，但是如果不想要父类的接口函数，那么就得考虑重构了。
### Comments

很多时候，大段注释之所以存在是因为代码很糟糕，不易理解。所以当你感觉需要撰写注释，请先尝试重构，试着让所有注释都变得多余。
