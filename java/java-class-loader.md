
java 的 class 只在需要的时候才内转载入内存, 并由 java 虚拟机的执行引擎来执行, 
而执行引擎从总的来说主要的执行方式分为四种:

第一种: 一次性解释代码, 也就是当字节码转载到内存后, 每次需要都会重新的解析一次.

第二种: 即时解析, 也就是转载到内存的字节码会被解析成本地机器码, 并缓存起来以提高重用性, 但是比较耗内存.

第三种: 自适应优化解析, 即将 java 将使用最频繁的代码编译成本地机器码, 而使用不频繁的则保持字节码不变,
一个自适应的优化器可以使得 java 虚拟机在 80%-90% 的时间里执行优化过的本地代码, 而只需要执行 10%-20%
对性能有影响的代码。

第四种: 一种能够利用本地方法直接解析 java 字节码的芯片.

在了解 java 虚拟机的类装载器之前, 有一个概念我们是必须先知道的, 就是 java 的沙箱, 什么是 java 的沙箱,
java 的沙箱总体上经历了这么一个过程, 从简单的 java1.0 的基础沙箱到 java1.1 的基于签名和认证的沙箱到后
来基于基础沙箱+签名认证沙箱的 java1.2 的细粒度访问控制。

java 的沙箱是你可以接受来自任何来源的代码, 但沙箱限制了它进行可能破坏系统的任何动作, 因为沙箱相对于系
统的总的访问能力已经被限制, 所以沙箱形象的说更像是一个监狱, 把有破坏能力的代码困住了.

java 沙箱的基本组件如下:

1. 类装载器结构(可以由用户定制)
2. class文件检验器
3. 内置的java虚拟机
4. 安全管理器(可以由用户定制)
5. java核心API


###运行时包

要了解运行时包, 我们先来设想一个问题, 如果你自己定义了一个 java.lang.A 的类, 能不能访问到 java.lang.String 类的 friend 成员?

###将代码归入某类(保护域)，该类确定了代码能够执行那些操作