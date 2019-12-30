title: TDD、BDD、MDD、UDD、FDD
tags: []
categories:
  - 软件工程专业课
date: 2019-07-03 16:13:00
author:
---
### TDD、BDD、MDD、UDD、FDD、DDD
小学期请了[这家公司](http://www.metashare.com.cn/)给我们讲MDD模型驱动开发。因此，除了在技术创新上研究外。软件开发的方法论也是应该考虑的了。

1. [TDD (Test-Driven Development) 测试驱动开发](#TDD)
2. [BDD (Behavior-Driven Development) 行为驱动开发](#BDD)
3. [MDD(Model-Driven Development) 模型驱动开发](#MDD)
4. [UDD(Usecase-Driven Development) 用例驱动开发](#UDD)
5. [FDD(Feature-Driven Development) 特性驱动开发](#FDD)
6. [DDD(Domain-Driven Development) 领域驱动开发](#DDD)

<!--more--> 
<span id="TDD"> </span>
###### 1.TDD (Test-Driven Development) 测试驱动开发
是敏捷开发中的一项核心实践和技术，也是一种设计方法论。 <font color="red">TDD的原理是在开发功能代码之前，先编写单元测试用例代码，测试代码确定需要编写什么产品代码。</font>TDD虽是敏捷方法的核心实践，但不只适用于XP（Extreme Programming），同样可以适用于其他开发方法和过程。

<span id="BDD"> </span>
###### 2.BDD (Behavior-Driven Development) 行为驱动开发
是一种敏捷软件开发的技术，<font color="red">它鼓励软件项目中的开发者、QA和非技术人员或商业参与者之间的协作。</font>BDD最初是由Dan North在2003年命名，<font color="red">它包括验收测试和客户测试驱动等的极限编程的实践，作为对测试驱动开发的回应。</font>在过去数年里，它得到了很大的发展。
<span id="MDD"> </span>
###### 3.MDD(Model-Driven Development) 模型驱动开发
一种新型软件设计方法——面向模型的分析设计方法，<font color="red">系统一开始我们就首先确立实体模型Entity Model，以及它们之间的关系，进而可以交由程序员分别实现表现层、业务服务层和持久层</font>，通过使用Jdon Framework（以下简称JF）等模型驱动框架，结合FDD等模型驱动的工程方法，从而正确无误地、且快速高质量地完成一个软件开发过程。
<span id="UDD"> </span>

###### 4.UDD(Usecase-Driven Development) 用例驱动开发
Jacobson在《Object-Oriented Software Engineering : A Use Case Drivern Approach》中给出的定义是这样的：
>当希望改变系统的行为时，重建相对应的参与者和用例模型。整个系统的基础架构将由用户所希望使用系统所进行的操作来控制。由于控制了所有模型，因此可以根据新需求修改系统。我们向用户询问他们希望改动的地方，也就是用例，兵直接找出这些改变在其他模型的什么部分实现。

<font color="red">用例驱动指的是所有开发过程的活动围绕用例来完成。</font>比如分析是做系统中的各个用例的分析、而设计是在设计并考虑各个用例的具体实现的方式。
<span id="FDD"> </span>
###### 5.FDD(Feature-Driven Development) 特性驱动开发
是敏捷软件开发过程中的一种，是由Jeff de Luca 、Eric Lefebvre、Peter Coad共同开发的。<font color="red">它强调特性驱动，快速迭代，即能保证快速开发，又能保证适当文档和质量，非常适合中小型团队开发管理。它提出的每个功能开发时间不超过两周，为每个用例user case限定了粒度，具有良好可执行性，也可以对项目的开发进程进行精确及时地监控。它抓住了软件开发的核心问题领域，即正确和及时地构造软件。</font>FDD还打破了传统的将领域和业务专家/分析师与设计者和实现者隔离开来的壁垒。分析师被从抽象的工作中解脱出来，直接参与到开发人员和用户所从事的系统构造工作中。 

<span id="F、DDD"> </span>
###### 6.DDD(Domain-Driven Development) 领域驱动开发
<font color="red">领域驱动设计是一种通过将实现连接到持续进化的模型来满足复杂需求的软件开发方法。</font>领域驱动设计的前提是： 把项目的主要重点放在核心领域和域逻辑 把复杂的设计放在有界域的模型上 发起一个创造性的合作之间的技术和域界专家以迭代地完善的概念模式，解决特定领域的问题 该词是由埃里克・埃文斯在其同名书中创造。