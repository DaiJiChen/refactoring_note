### 1、Pull Up/Down Field (值域上移/下移)

如果 subclass 中有相同的值域，则应将其移到 superclass 中。

如果 superclass 中的某个值域只被部分（而非全部）subclasses 用到，则应将这个值域遇到需要它的 subclass 中去。

### 2、Pull Up/Down Method (函数上移/下移)

如果有些函数，在各个 subclass 中产生完全相同的结果，则将该函数移至 superclass。但现实情况往往比这个复杂，你可能需要先重构各个 subclass 中的函数，使他们成为一样的函数，然后再将他们上移至 superclass。

如果 superclass 中的某个函数只与部分（而非全部）subclasses 有关，则将这个函数移到相关的那些 subclasses 去。


### 3、Pull Up Constructor Body (构造函数本体上移)

如果各个 subclass 的构造函数几乎完全一致，则应该在 superclass 中新建一个构造函数，并在 subclass 的构造函数中调用它。

但是，如果构造过程较为复杂，则可以考虑转而使用 Replace Constructor with Factory Method

### 4、Extract Subclass (提炼子类)

当 class 中的某些特性之被部分实例用到，则应该新建一个 subclass，将上述所说的那一部分特性移到 subclass 中

### 5、Extract Superclass

当两个 classes 有相同的特性，则可以为他们建立一个 superclass，将相同特性移至 superclass

### 6、Extract Interface (提炼接口)

如果多个 class 都对外提供一批相同的方法，用以代表某一类功能。那么应该考虑将这些方法抽出一个 interface。

### 7、Collapse Hierarchy (折叠继承关系)

当 superclass 和 subclass 之间无太大差别时，应该将他们合为一体。

### 
