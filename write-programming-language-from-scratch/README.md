## 绪言

之所以写这系列的文章，是我在2022年3月冒出了一个想法：将cpython internal这本教程阅读并进行实践。尽管我花了数个月将书籍浏览并进行实操，但是对了解python这门语言更多的知识，仍然是令人兴奋的。cpython的内部是如此复杂，光从书本上获取的知识，仍旧满足不了我的好奇心，于是我在2022年9月开始模仿cpython设计机制，来重写一门（在某种意义上）属于自己的编程语言，并对语法做一些更改已表现出它的特殊性。

## 关注编译器

cpython的编译器简述一下，可以分为front end和back end。front end通过分析source code来产生intermediate representation，简称IR，IR通常采用tree结构来表征，这种树结构常常被称为抽象语法树（Abstract Syntax Tree），简称AST，也有其他机器语言表达形式，这里不作深入；back end通过分析IR并进行一系列的优化后，最终利用代码生成（code-generation）技术，将IR转换成target language；

```shell
# frontend
scanning-->parsing-->semantic analysis-->IR(intermediate representation)
```


```shell
# back end
analysis-->optimisation-->code generation
```

## front end
通常至少需要三个部分组成front end，分别为：

- scanner/lexer --> 用来将source code分解为tokens
- parser/syntax analyzer --> 构建AST
- semantic analyzer --> 类型检查、对象绑定、

## back end
这一步需要关注的是，将IR表达成另一门语言，例如C，或者更进一步，直接生成汇编，但最终的目标都是生成一种可执行的表达；