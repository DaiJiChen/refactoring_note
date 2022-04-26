### 1、Pull Up/Down Field (值域上移/下移)

如果 subclass 中有相同的值域，则应将其移到 superclass 中。

如果 superclass 中的某个值域只被部分（而非全部）subclasses 用到，则应将这个值域遇到需要它的 subclass 中去。

### 1、Pull Up/Down Method (函数上移/下移)

如果有些函数，在各个 subclass 中产生完全相同的结果，则将该函数移至 superclass。但现实情况往往比这个复杂，你可能需要先重构各个 subclass 中的函数，使他们成为一样的函数，然后再将他们上移至 superclass。

如果 superclass 中的某个函数只与部分（而非全部）subclasses 有关，则将这个函数移到相关的那些 subclasses 去。
