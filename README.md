# YuanNews
 基于用户兴趣标签的新闻推荐系统（毕业设计）

#2016.04.06-07
 * 新闻系统大改版
    * 1.　采用新的开发模式　－　idea 多个module进行　ssm 开发；
    * 2. 　还是采用　maven 的方式进行环境配置和相关module直接的配置；
    * 3. 多module 配置有些类似　asp.net 类库的配置，所以需要借鉴配置思想；
    * 4. 多module 开发是的各个模块之间耦合性降低，方便开发，十分方便；

---
 #小结
 　　news - 第一版,开发平台是idea,通过maven 进行的环境搭建，其实挺方便的；
 ```
      基本的开发思路是:　mapper -> service -> controller -> jsp ;
 ```
  当然，第一版是在一个project 中进行开发的，随着代码的编写，类，接口等越来越多，看起来非常不爽！就想到了Android Studio 开发的时候，可以多模块，
  进行开发Android。故，就尝试了在news上就行大改版，使用idea进行多个module（web,config,contorller,dao,model,service,common　）七个module,
  单独的module进行如果需要其它的module，需要进行maven依赖配置。通过maven，将多个module进行配置，然后进行每个模块的单独开发！当然由于没有经验，
  配置了１天多的时间，中间思考了很多，就想起来了asp.net开发的时候dll类库的时候，故就其思想，进行了依赖配置，结果成功了！稍后，将在csdn博客上进行配置总结，
  当然　使用gradle应该基本一致！
  　
  　



---
news-第一版完结　
---

#2016.04.04
　 * 数据层－后台管理－基本实现
  * 数据层　－　用户端　－　添加接口
  * 业务层　－　后台管理　－　添加接口

#2016.04.03
 添加评论表（信息图），点赞表 （❤）
 * 评论表设计 ：
    * id 评论id
    * content 评论内容
    * uid 评论用户id
    * nid 评论新闻id
    * status 评论状态
 * 创建评论表
   ```
    create table comment(
       id int(11) not null primary key auto_increment,
       content text not null,
       uid int(11) not null default '0' , FOREIGN KEY (uid) REFERENCES user(id),
       nid int(11) not null default '0' , FOREIGN KEY (nid) REFERENCES news(id),
       status int(4) not null default '0'
    )DEFAULT CHARSET=utf8;
   ```

 * 点赞表 ：
    * id 点赞id
    * uid 用户id
    * nid 新闻id
    * status 点赞状态 0,没有点赞，1,点赞
 * 创建点赞表
    ```
      create table liked(
             id int(11) not null primary key auto_increment,
             uid int(11) not null default '0' , FOREIGN KEY (uid) REFERENCES user(id),
             nid int(11) not null default '0' , FOREIGN KEY (nid) REFERENCES news(id),
             status int(4) not null default '0'
          )DEFAULT CHARSET=utf8;
    ```

#2015.04.01
 * 后台管理，数据访问实现 ；
 * 添加信息来源表 ；
   ```
      create table source(
               id int(11) not null primary key auto_increment,
               source varchar(100) not null
             )DEFAULT CHARSET=utf8;

   ```


#2016.03.31
 * 测试静态文件和动态jsp页面加载情况；
 * 测试mybatis，单元测试，进行加载数据；
 * 初始化后台界面，准备开启数据后台管理；
 * D3.js 的学习 ；

#2016.03.30
  重新初始化工程，数据库不变！

#2016.03.29
  设置mysql字符编码集,已修改为 utf-8：
  添加测试数据:
   * 分类表 ：
     ```
      insert into cate(content) values('社会');
      insert into cate(content) values('科技');
      insert into cate(content) values('经济');
      insert into cate(content) values('趣闻');
      insert into cate(content) values('情感');

     ```

   * 用户表
    ```
    insert into user(unum,nick,pass) values('15036518579','LABELNET','123456');
    insert into user(unum,nick,pass) values('15000000001','yuan','123456');

    ```

   * 兴趣表
   ```
     insert into taste(label,uid) values('手机',1);
     insert into taste(label,uid) values('小米',1);
     insert into taste(label,uid) values('电影',1);
     insert into taste(label,uid) values('刘亦菲',1);
     insert into taste(label,uid) values('围棋',1);
     insert into taste(label,uid) values('NBA',1);

   ```

   * 新闻表
   ```
     insert into news(title,content,dt,img,rnum,cid,sid) values('Uber招程序员有新招：车上玩个游戏就行'
     ,'据悉，应用内的游戏共包含三项挑战，用户必须在60秒内搞定每个挑战。如果得分够高，就可以直接通过应用联系Uber的人力资源部，并通过email收到相关的工作申请链接。
               　　Uber发言人表示：“我们一直在利用各种新方式接触潜在的人才，Uber希望与它们一起解决各种有趣的问题。如果你生活的城市拥有非常浓的科技气息，就可以在Uber应用中找到"路上的代码"挑战。只要你有一技之长，肯定会觉得这项挑战非常有趣，它不但能帮你找工作，还能让你的旅途不再枯燥。”
               　　很多程序员看到这项有趣的挑战后，纷纷发起了挑战。未来，该公司将会把这项挑战推向全美多个城市，以挖掘人才。此外，Uber也解释称，这项挑战并不是想利用个人信息来对用户进行定位',
               '2016-03-29','http://i3.hexunimg.cn/2016-03-29/183020755.jpg',212,4,1);

    insert into news(title,content,dt,img,rnum,cid,sid) values('习近平出席捷克总统泽曼举行的欢迎仪式','新华社布拉格3月29日电（记者王丰丰）29日，国家主席习近平出席捷克总统泽曼在布拉格总统府举行的隆重欢迎仪式。
                                                                                              初春的布拉格，阳光明媚，绿草如茵。春光下的总统府，旌旗招展，鲜花绽放，等待着中国贵宾的到来。
                                                                                              当地时间上午10时许，习近平抵达总统府3号院。旗手沿红地毯整装列队。泽曼在军乐队前迎接习近平。两国元首面向总统旗站立，军乐队奏中捷两国国歌，鸣礼炮21响。习近平在泽曼陪同下检阅仪仗队，仪仗队由捷克军队和总统府警卫部队组成。
                                                                                              检阅毕，习近平用捷克语问候捷克士兵“战士们好”，捷克士兵齐声响亮回应“好”。两国元首登上检阅台，共同检阅分列式。
                                                                                              王沪宁、栗战书、杨洁篪等出席欢迎仪式。','2016-03-29','http://upload.cankaoxiaoxi.com/2016/0329/1459243945740.jpg',1021,1,2);
  * 来源表

   ```
        insert into source(source) values("腾讯新闻");
        insert into source(source) values("搜狐新闻");
        insert into source(source) values("中关村在线");
        insert into source(source) values("百度新闻");


   ```

  基本pojo对象属性：
   * 用户
   ```
     private Integer id;
     private String unum;
     private String head;
     private String nick;
     private String pass;
     private Integer sex;
     private Integer status;

   ```

   * 兴趣
      ```
      private Integer id;
      private String label;
      private Integer uid;

      ```
   * 分类
      ```
      private Integer id;
      private String content;

      ```
   * 新闻
      ```
      private Integer id;
      private String title;
      private String content;
      private String dt;
      private String img;
      private Integer rnum;
      private Integer cid;
      private Integer sid;

      ```


#2016.03.26
 系统环境 ubuntu 14.04 , 基本实现 mysql安装,数据库设计与创建,mybatis的基本操作
 * 数据库 mysql5.5
 * 数据库设计 ： newssysdb 设计第一版
    * user 用户表
        * id 用户id
        * unum 账号
        * head 头像
        * nick 昵称
        * pass 密码
        * status 状态(暂时不分析)
        * sex 性别 默认0 为男，1为女
    * taste 兴趣表
        * id 兴趣id
        * label 兴趣标签
        * uid 外键（用户id） -> user/id

    * cate 分类表
        * id 分类id
        * content 内容

    * news 新闻表
        * id 新闻id
        * content 新闻内容
        * title 新闻标题
        * sid 来源 -> source/id
        * cid 分类id  -> cate/id
        * dt 发布时间
        * rnum 阅读次数

---
 * 创建数据库和表

 （1）创建数据库

      ```sql

      create database newssysdb  character set utf8;


      ```
 （2）创建用户表

      ```sql

       create table user(
         id int(11) not null primary key auto_increment,
         unum varchar(15) not null,
         head varchar(200) default '/images/moren.jpg',
         nick varchar(100),
         pass varchar(100) not null,
         sex int(4) not null default '0',
         status int(4) not null default '0'
       )DEFAULT CHARSET=utf8;

      ```

（3） 创建兴趣表

     ```sql

        create table taste(
          id int(11) not null primary key auto_increment,
          label varchar(100) not null,
          uid int(11) not null default '0',
          FOREIGN KEY (uid) REFERENCES user(id)
        )DEFAULT CHARSET=utf8;

     ```
（4） 创建分类表

     ```sql

        create table cate(
          id int(11) not null primary key auto_increment,
          content varchar(100) not null
        )DEFAULT CHARSET=utf8;

     ```
（5）创建新闻表

     ```sql

        create table news(
            id int(11) not null primary key auto_increment,
            title varchar(200),
            content text,
            dt varchar(100),
            img varchar(200) default '/images/moren.jpg',
            rnum int(11) not null default '0',
            cid int(11) not null default '0' , FOREIGN KEY (cid) REFERENCES cate(id),
            sid int(11) not null default '0', FOREIGN KEY (sid) REFERENCES source(id)
          )DEFAULT CHARSET=utf8;

     ```

#2016.03.17
 使用maven进行就行构建
 * spring            4.2.5.RELEASE
 * spring mvc        4.2.5.RELEASE
 * mybatis           3.3.0
 * mybatis-spring    1.2.4
 * log4j             1.2.17
 * mysql-connector-java 5.1.38
 * fastjson          1.2.7
 * junit             3.8.1

