---
layout: post
title: 领域驱动设计-读书笔记
comments: false
keywords: 读书,DDD, 领域驱动设计
category: 设计
---
#让领域模型发挥作用.              

1,消化知识.
  模型-->深层模型.

2,交流及语言的使用.
  将模型作为通用语言的骨干.

3, 将模型与实现绑定.

#模型驱动设计的构建块.

4,分离领域

  一般认为, 软件行业确定了分层架构作为软件系统关注点分离的首选方案.基本原则是,每一层中元素只能依赖同一层的其它元素,或直接下层元素.
  在面向对象的程序中,用户界面(UI),数据库和其他支持代码,经常写在业务对象中.在UI和数据库脚本中嵌入额外的业务逻辑.  这在短期来看是最容易的方式.
  当领域相关的代码和大量其它代码混杂在一起时,就很难阅读并理解了.  对UI的简单的改动就会影响业务逻辑. 改变业务逻辑规则就可能需要小心跟踪UI代码,数据库代码或其它程序元素.  实现一致的模型驱动对象变得不切实际. 自动化测试也难以使用.如果程序的每个行为都包含了所有的技术和逻辑,那么它必须很简单,否则会难以理解.   分离还可以有助于分布是系统的部署,可以灵活的把各层放在不同的物理机器上.
  
  用户界面层/
  应用层/    定义软件可以完成的工作, 并且指挥具有丰富含义的领域对象来解决问题.这个层所负责的任务对业务影响深远,对跟其它系统的应用层进行交互非常必要,要保持简练.不包含业务规则和知识,只是给下层领域对象协调任务,委托工作. 在这层中不反映业务情况的状态,但反映用户或程序任务进度的状态.
  领域层/    负责表示业务概念,业务状况的信息以及业务规则.尽管保存这些内容的技术细节由基础结构层来完成.反映业务状况的状态在该层中被控制和使用.这层是业务软件的核心.
  基础设施层/

  将层连接起来而不影响分离给设计带来的好处,是许多设计模式追求的.层是一种松散关联结构,因为设计的依赖是单向的,上层可以直接使用或操作下层元素,这可以通过直接调用下层的公共接口,维护对它们的引用或使用常规的交互方法来完成.但当下层对象需要跟上层对象通信时,我们需要另一种机制,采用架构模式把各层联系起来,如回调或Observer
  连接用户界面,应用层和领域层的模式通常是MVC及它的衍生者.  基础架构层通常不在领域层发其动作, 这种技术能力通常以服务的方式提供.另一种形式是技术组件设计为直接支持其它层的基本功能.如某某领域对象的具体实现.
  在智能UI和分层架构之间还有其它的解决方案,如Fowler的事务脚本. 它不提供一个对象模型,但把用户界面分离出来.

  如果一个结构隔离了与领域相关的代码,同时允许内聚的领域设计与系统的剩余部分保持一种松散的关联,那么这就是领域驱动设计.   必须在复杂性和灵活性做出考虑,权衡.

 5, 软件中的模型描述.

  将用来表述模型的模型元素分为4类:  实体/值对象/服务/DomainEvent
  一个对象所代表的事物是一个具有连续性和标识的概念,还是只是用来描述事物的某种状态的属性?  这就是实体和值对象的最基本区别.  
  值对象具有不变性, 除了构造方法, 其它操作都是无副作用函数.

  服务:
  如果用行为或操作来描述会比用对象描述更加清晰,  那么最好用服务来描述, 尽管这与面向对象建模理念稍有抵触.   服务常用来封装技术层的功能, 在领域中则用于对必须完成的一些活动建模,但与状态无关.
  服务执行的操作涉及一个领域概念，这个领域概念通常不属于一个实体或者值对象,      被执行的操作可能涉及到领域中的其他的对象

  操作是无状态的

  模块:
  将相关领域模型提炼分类，分而治之
  将高关联度的模型分组到一个模块以提供尽可能大的内聚（以能完整完成任务为准）
  模块是垂直划分(Domain内部)/分层是水平划分

  关联, 现实世界中存在着大量的多对多双向关系,   这种复杂的关联会给程序开发和维护带来很大的困难. 尽可能的约束关联使其反映领域的使用偏向是非常重要的,至少有3中方法可以使关联变得相对简单.
    指定一个导航的方向
    双向关联意味着只有两个对象同时放在一起才能被理解.  如果应用并不要求双向交互, 则指定一个方向则可以简化设计,如国家和元首是典型的1对多双向关联, 但我们未必需要查询华盛顿是哪国的元首,仅维护国家到元首的连接通常是足够的.此时,也就不需要单独的元首类了,个人类就可以了.否则需要一个GetCountryOfThePresdent()方法.getNationality()并不能精确体现业务.
    加入限定符来有效减少关联的多重性.
    国家和元首是典型的1对多关联, 但国家某个时期的总统则将关联转为一对一.
    清除不必要的关联  
    如果关联不是任务的本质,或者不能反映模型对象的基本含义,  取消它. 不是所有的现实关联都是在类变量中维护的,如账户的交易明细,  可以是账户类中保存一个到交易列表的引用; 也可以是在账户中有一个查询交易的方法,而方法去外部存储中查询.提供导航或是依赖查询,是一种设计上的决定,取决于我们在查询的解耦与关联的内聚之间如何权衡.当出现循环引用时尤其需要仔细考虑.

 6, 领域对象的生命周期
    管理对象有两个挑战,
    1. 在生命周期维护对象的完整性.
    2. 避免模型由于管理生命周期的复杂性而陷入困境.
    三个模式来处理这些问题.   Aggregate/Factory/Repository
      聚合:
      根实体具有全局标志, 并最终负责对不变量的检查.
        边界内的实体具有本地标志, 仅在聚合内唯一.
        聚合边界外的任何对象仅能引用根实体,  根实体可以把内部实体的实例副本传递给外部, 但那只是一个副本,已经和聚合不再关联了.
        推论, 能通过数据库查询得到的只有聚合根, 其他只能通过导航关联访问.

        聚合内的对象可以持有其它的聚合根.
        删除操作必须一次性删除聚合边界的所有对象.
        当聚合边界内发生的任何对象修改被提交时, 整个聚合的所有不变量必须都被满足.
        当一个实体实例可以被多个其它实体实例共享时, 它一定是根实体.

      工厂:
        组件的创建和组装大多与领域概念无关, 将创建与操作组合起来是不合适的,  最好分离. 但有时对象创建是有领域意义的,如"开设银行账户"

      仓储:
        工厂封装了对象在创建和重建时的生命周期, 还有一种变迁, 它在技术上的复杂性也会导致领域设计陷入混乱,那就是对象和存储的双向转换,这种转换是另一种领域设计构造---仓储.  

      工厂创建新的对象, 仓储寻找旧的对象,仓储让客户觉得那些对象好像就在内存中.

      Specification/isSatisfiedBy(T)/ Pattern, 

      Query Objects Pattern ,  refer to JPA CriteriaQuery,Predicate....

 7, 使用语言:扩展示例  货物运输系统
 8, 突破
      模型的重构: 微重构/模式重构/模型重构
      细微的改进,连续的每次精化使我们对模型的理解节节进步.我们必须努力消化领域知识,并提炼出一套稳定通用语言,着眼于根本,得到深度模型.
 9, 隐含概念转变为显式概念
      深层模型包含领域的中心概念和抽象, 能够简洁灵活的表达用户活动,问题及解决方案的本质知识.
      如何建模不太明显的概念
      显式的约束/作为领域对象的流程/规格
      Specfication用于3个目的: 验证一个对象/从集合筛选对象/在创建对象时指定该对象必须满足的要求.
 10,柔性设计
      软件最终目的是为用户服务, 但它必须首先为开发人员服务.
      设计灵活的东西,往往是简单的, 但简单不是唾手可得的.
      释意接口Intention Revealing Inteface  类和操作应该表达出其效果和目的, 名字需要与通用语言一致.这也是封装的目的,无须理解组件的实现即可通过名字获悉组件的含义.
      无副作用函数. 返回结果而不产生副作用.  值对象可以在查询中创建出来, 返回给调用者, 然后删除.
      命令, 确保引起状态改变的方法不返回任何领域数据,并尽可能的简单.  可以使用断言或单元测试规范契约.
      如果一个操作把逻辑(或计算)与状态修改混在一起,那么应该重构为两个分离的操作.   但这只是针对实体, 值对象就不会有命令操作.
      修改变元(参数)是个糟糕的行为,  只在必要的时候使用, 一定考虑命名, 且不要既输入又输出.
      软件与现实的不同是,   拷贝操作没有副作用. 用多个对象构建一个复合对象时,源对象可以不变,复制一份而构建新对象或只是根据源对象某些属性构建.使用副本或是源对象引用取决于领域逻辑,  当模拟混合两桶颜料, 得到混合颜料时,  领域关注混合颜料结果,  甚至原来颜料状态,  但不关注后来的颜料桶是否空了.  这时可以将源颜料体积相加, 颜色配比,生成新颜料, 但源颜料不发生变化.   当软件模拟订单采购时,  Order.fill(wareHouse),   wareHouse就必须减少库存. 领域关注源对象.
      概念轮廓
      操作封闭