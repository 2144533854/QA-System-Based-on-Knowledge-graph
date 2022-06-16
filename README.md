### 基于知识图谱的会展知识问答系统
#### 项目环境
* Django==2.2.7
* django-ranged-response==0.2.0
* django-simple-captcha==0.5.12
* Pillow==6.2.1
* pytz==2019.3
* six==1.13.0
* sqlparse==0.3.0
* jinja2==2.10
* pyecharts==1.9.1
* py2neo== 2021.2.3
* matplotlib==3.0.2
* redis==2.10.6
* pyahocorasick==1.4.4


#### 软件
* JetBrains PyCharm 2019.2.3 x64

#### 数据库设计
1、redis数据库设计 

使用Redis数据库存放了用户的用户名、密码、登陆状态、验证码失败次数和禁止登陆时间，其中密码使用md5加密算法中，sha256安全散列算法，以非明文方式存储。禁止登陆时间使用Redis数据库中expire函数，在用户禁止登陆后，生成倒计时。用户所有数据使用Redis中哈希这个数据结构来实现，详细设计情况如下所示。

字段名	含义	备注

username	用户名	用户唯一标识

password	密码	sha256安全散列算法加密

fail_time	验证码失败次数	失败次数大于5次禁止登陆

login_status	登陆状态	负责检验登陆状态和注入session

forbiddentime	禁止登陆时间	默认不存在，当禁止登陆后在当前用户哈希表中自动生成

send	发送验证码次数	10分钟内最多发送5次

2、ne4j数据库设计

Neo4j存储了7类实体节点，6类实体间的关系和11类实体属性。
#### 运行
* python manage.py runserver

#### 路由设计
URL|视图|模板|说明
-|-|-|-
index|login.views.index|index.html|主页
login|login.views.login|login.html|登录
register|login.views.register|register.html|注册
logout|login.views.logout|NAN|登出
