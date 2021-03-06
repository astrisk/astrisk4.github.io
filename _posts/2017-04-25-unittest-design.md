---
title:  "UNITTEST-testcase Design"
date:   2017-04-25 17:21:50
categories: UNITTEST
---

当我们在做单元测试的时候，很多同事都会提到这样一个问题：如何设计单元测试用例，应该从哪些角度或者维度来设计测试用例？

用测试的思维来看待单元测试，就是我们首先要理解需求，清楚需求，然后才能知道怎么去设计用例，写测试用例。其实对于单元测试，也是一样的。只不过需求的表现或者表达方式不一样而已。

那什么是单元测试的需求呢？以及从哪些方面来进行单元测试用例设计？这就是本篇post的主题。

## **理解单元测试需求**

单元测试的被测试对象是类的公共接口（我们对private方法不做要求）。如果需要比较完整地理解一个类的职责，最好不要孤立地去考虑被测试类/方法，而应该从模块等比较高的层面去理解类的行为，用角色、职责和协作者的关系来思考被测试对象，理解了被测对象扮演的角色，有什么样的职责，以及需要的协作对象。具体到被测试的方法，需要清楚：1. 被测试方法的使用场景；2.方法的行为以及上下文（输入，输出）；3. 输入输出的限制条件；4. 异常处理；5. 返回值类型等。

那这些需求从哪里获取呢？主要有几个来源：1. 概要设计 2. 详细设计 3. 类接口文档 4. 源代码

我在做单元测试的时候，会去看源码，但是比较少用白盒测试方法去做用例设计，更多地是使用黑盒用例设计方法。我们把对外接口用契约方式来相互协作，开发者只要满足契约即可，内部的实现可以使用不用算法。这样设计的单元测试用例健壮性比较好，只要接口契约不改，用例一般不会有问题。

## **单元测试用例设计**

在理解了测试需求后，我们就可以来进行单元测试用例设计。一般我们要求开发者大致需要考虑以下几个方面的测试用例。

- 功能用例
	- 需要编写一个或多个用例来验证功能正确实现。例如：有个Login方法，需要编输入正确用户名和密码成功登陆的用例。

- 反向用例
	- 反向用例来用验证输入非法值或错误值时，代码是否处理。例如：Login方法，编写输入错误用户名或密码的用例(用户名和密码都为Null)

- 异常用例
	- 异常用例用来验证代码是否对异常进行处理。例如：Login方法中，编写数据层接口返回异常(数据库异常等)的用例。

- 边界用例
	- 边界用例用来验证代码对边界情况的处理是否正确。例如：Tracker采样率为(0,1]。测试解析方法时，需要编写两个边界用例(采样率为0和采样率为1时的场景)来验证代码正确处理

- 综合用例
	- 通过结合不同的使用方式来实现API的一些复杂行为。综合测试表现复杂行为，这样能发现更多的问题。这类型的测试在更切合现实的条件下，模拟API的使用。例如：有个stack，往stack push 3个对象后，pop掉2个对象,需要验证stack内保留的对象数目是否为1

当然并不是说每个被测试方法的单元测试用例都要覆盖以上五个方面。这里更多地是起到指导作用，同时在做UT review时，我们也要从这个方面来考虑用例是否完整。而且一个方面也不一定是一条case，有可能需要多条case。

