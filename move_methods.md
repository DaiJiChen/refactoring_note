### 1、Move Method（搬移函数）

若一个 method 使用另一个对象的次数比使用当前对象的次数还多，则可以考虑将其移动到另一个对象中。这样可以减少类间的调用关系。

### 2、Move Field（搬移值域）

若一个 field 被另一个 class 中的函数更多地用到，则应将其移动到经常使用它的类中去。

### 3、Extract Class（提炼类）

若某个 class 做了两个 classes 应该做的事，则因该新建一个 class，并将相关 field 和 method 搬运到新 class 中去。
注：搬运 metthod 时先搬运较低层的函数，再搬运较高层的函数。

### 4、Inline Class（将类内联化）

与 Extract Class 刚好相反，如果一个 class 承担的责任太少，没有单独存在的意义，则可以将其 field 和 method 全部塞到 absorbing class（接收这个萎缩class 的 class）中去，并将对这个 class 的全部引用都换成对 absorbing class 的饮用。

### 5、Hide Delegate（隐藏委托关系）

若 client class 绕过 server class 直接调用 delegate class，则应该取消这种直接调用关系。例如 MVVM 模式中的 View 不应该绕过 viewModel 直接操作 Repo。如下图：
**动机：**封装意味着每个对象都应该尽可能少地了解其他的对象。如此一来，一旦某个 calss 发生变化，相应地需要修改的 class 就会比较少。

### 6、Remove Middle Man（移除中间人）

与 Hide Delegate 相反，如果 server class 做了太多的简单委托动作，则应该让 client class 直接调用 delegate class。

**问题：如果你想为某个 class 添加一个方法，但是又不能直接修改这个 class 的源码（比如你想为 java 库里的Date.class 添加一个名为 nextDay 的方法），以下 7、8 两种方法可以考虑使用。**
### 7、Introduce Foreign Method（引入外加函数）

在 client class里新建一个函数，并将这个不能修改的 class 做为参数传进去。

### 8、Introduce Local Extension（引入本地扩展）

新建一个 class，让这个 class 成为你想要扩展的 class 的 subclass 或 wrapper。
