---
title: Mybatis和IBatis的区别
date: 2017-03-30 16:04:08
tags: Mybatis
---

1. Mybatis比IBatis比较大的几个改进是什么

        a.有接口绑定,包括注解绑定sql和xml绑定Sql ,
        b.动态sql由原来的节点配置变成OGNL表达式,
        c. 在一对一,一对多的时候引进了association,在一对多的时候引入了collection节点,不过都是在resultMap里面配置

2. 什么是MyBatis的接口绑定,有什么好处

        接口映射就是在IBatis中任意定义接口,然后把接口里面的方法和SQL语句绑定,我们直接调用接口方法就可以,这样比起原来了SqlSession提供的方法我们可以有更加灵活的选择和设置.

3. 接口绑定有几种实现方式,分别是怎么实现的?

        接口绑定有两种实现方式,一种是通过注解绑定,就是在接口的方法上面加上
        @Select@Update等注解里面包含Sql语句来绑定,另外一种就是通过xml里面写SQL来绑定,在这种情况下,要指定xml映射文件里面的namespace必须为接口的全路径名.

4. 什么情况下用注解绑定,什么情况下用xml绑定

        当Sql语句比较简单时候,用注解绑定,
        当SQL语句比较复杂时候,用xml绑定,一般用xml绑定的比较多

5. MyBatis实现一对一有几种方式?具体怎么操作的

        有联合查询和嵌套查询,联合查询是几个表联合查询,只查询一次,
        通过在resultMap里面配置association节点配置一对一的类就可以完成;
        嵌套查询是先查一个表,根据这个表里面的结果的外键id,去再另外一个表里面查询数据,也是通过association配置,但另外一个表的查询通过select属性配置

6. MyBatis实现一对多有几种方式,怎么操作的

        有联合查询和嵌套查询,联合查询是几个表联合查询,只查询一次,通过在resultMap里面配置collection节点配置一对多的类就可以完成;
        嵌套查询是先查一个表,根据这个表里面的结果的外键id,去再另外一个表里面查询数据,也是通过配置collection,但另外一个表的查询通过select节点配置

7. MyBatis里面的动态Sql是怎么设定的?用什么语法?

        MyBatis里面的动态Sql一般是通过if节点来实现,通过OGNL语法来实现,但是如果要写的完整,必须配合where,trim节点,where节点是判断包含节点有内容就插入where,否则不插入,trim节点是用来判断如果动态语句是以and 或or开始,那么会自动把这个and或者or取掉

8. IBatis和MyBatis在核心处理类分别叫什么

        IBatis里面的核心处理类交SqlMapClient,
        MyBatis里面的核心处理类叫做SqlSession

9. IBatis和MyBatis在细节上的不同有哪些

        在sql里面变量命名有原来的#变量# 变成了#{变量} 
        原来的$变量$变成了${变量},
        原来在sql节点里面的class都换名字交type
        原来的queryForObject queryForList 变成了selectOne selectList 
        原来的别名设置在映射文件里面放在了核心配置文件里

10. 讲下MyBatis的缓存

        MyBatis的缓存分为一级缓存和二级缓存,
        一级缓存放在session里面,默认就有,二级缓存放在它的命名空间里,默认是打开的,
        使用二级缓存属性类需要实现Serializable序列化接
        口(可用来保存对象的状态),可在它的映射文件中配置<cache/>

11. MyBatis(IBatis)的好处是什么

        ibatis把sql语句从Java源程序中独立出来，
        放在单独的XML文件中编写，给程序的维护带来了很大便利。
        ibatis封装了底层JDBC API的调用细节，并能自动将结果集转换成Java Bean对象，
        大大简化了Java数据库编程的重复工作。
        因为Ibatis需要程序员自己去编写sql语句，
        程序员可以结合数据库自身的特点灵活控制sql语句，
        因此能够实现比hibernate等全自动orm框架更高的查询效率，能够完成复杂查询。.