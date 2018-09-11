### 一级缓存



Mybatis中一级缓存是`SqlSession`级别的缓存。即同一个`SqlSession`执行2次相同查询（条件也相同），Mybatis只会在第一发送sql从数据库中查询数据，然后将数据缓存起来，第二次就会从`SqlSession`中返回数据。Mybatis默认开启了一级缓存。

~~~java
@Test
public void testOneLevelCache() {
    SqlSession sqlSession = sqlSessionFactory.openSession();
    UserMapper userMapper = sqlSession.getMapper(UserMapper.class);
    User user1 = userMapper.findUserById(1);
    User user2 = userMapper.findUserById(1);
    System.out.println(user1);
    System.out.println(user2);
}
~~~

![1536655016308](D:\GitRepositories\Article\Article\Mybatis缓存1.png)



上述代码中虽然对`User`对象执行了2次查询，但是Mybatis只发送了一次sql从数据库中进行查询。