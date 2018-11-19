> Book Name: 《JavaScript:The Good Parts》

> Author: Douglas Crockford

#### Chapter 2: Grammer

Javascript只有一种数字类型，它在内部被表示为64位的浮点数，和Java的double数字类型相同。

Javascript中的所有字符都是16位的。


#### Chapter 3: Object

`for in` 循环一个对象中的属性，其出现的顺序是不确定的。


#### Chapter 4: Functions

在Javascript中一共有4中调用模式: `方法调用模式，函数调用模式，构造器调用模式以及apply调用模式`。

- 方法调用模式： 当一个函数被当做是一个对象的一个属性是，被认为是一个方法。
- 函数调用了：普通的函数调用
- 构造器调用模式： new ABC()
- apply调用模式： add.apply(null, arguments)

`arguments`数组并非是一个真正的数组，它并没有`concat`方法的等。


#### Chapter 6: Arrays

Javascript提供了一个拥有一些类数组特性的对象，而并不是Java中数组的概念。


#### Chapter 7: Regular Expressions

使用`/^  $`来框定这个正则表达式

`(?:.....)`表示一个可选的非捕获分组，**通常用非捕获型分组来替代少量不优美的捕获型分组是很好的方法**


> Regexp Escape

`\f`是换页符 `\n`换行符 `\r`回车符 `\t`制表(tab)符 `\w` -> [0-9A-Z_a-z]


> Regexp Quantifier

`?`等同于{0, 1}  `*`等同于{0,} `+`等同于{1,}


#### Chapter 8: Methods

> array.sort(comparafn)

Javascript的默认比较函数把要被排序的元素都视为字符串。


#### Awful Parts

Javascript的问题不仅仅在于它允许使用全局变量，还是在于依赖于全局变量，Javascript中没有链接器(linker)，导致所有的编译单元都载入一个公共全局对象中。

> parseInt

- 它遇到非数字的时候就会停止
- 如果该字符第1个字符是0，那么该字符会基于八进制而不是十进制来求值。 `parseInt('08') === parseInt('09')`

### 感受

感觉十分的失望，本以为会是一本稍微进阶一点的书籍，但是没想到十分的基础，并且有一些需要深究的点并没有说的很详细，而是一笔带过，本来书籍章节就很少，再加上写的点十分的多，导致每个知识点都是草草带过。十分不推荐这本书。

2018.11.19