## Flask

### Flask简介

- 基于Python实现的Web开发‘微’框架。
- 简单创建一个flask项目：



- flask以来的三个库：
  - jinja2 模板引擎
  - werkzeug WSGI工具类
  - Itsdabgeous 基于Django的签名模块

- Debugger：

  - 有一个PIN码：

  - 可以更方便调试，在页面中进行调试。需要输入PIN码！



### flask的优点

- 有非常齐全的官方文档
- 有很好的扩展机制和第三方扩展环境，工作中常见的软件都会有对应的扩展，自己动手实现扩展也很
- 社区活跃度很高
- 微型框架的形式给了开发者更大的选择空间。



### 虚拟环境安装

- 安装pip:  apt	install	python-pip
- 安装virtualenv:   pip  install   virtualenv
- 安装虚拟环境配置软件：apt  install virtualenvwrapper或 easy_install virtualenvwrapper


- 配置虚拟环境：在用户目录下创建一个隐藏文件   mkdir ~/.virtualenvs,编辑环境变量
- export  WORKON_HOME=~/.virtualenv
- soure     /usr/local/bin/virtualenvwrapper.sh



### 基础项目

```
from flask import Flask, abort

app = Flask(__name__)

@app.route('/')
def hello():
	return 'Hello Flask'

if __name__ == '__main__':
	app.run()
```

- 在启动的时候还可添加参数，在run()中：
  - debug：是否开启调试模式，开启后修改python代码会自动重启
  - threaded：是否开启多线程
  - port：启动指定服务器的端口号
  - host：主机，默认是127.0.0.1
- 代码结构：
  - static：静态资源文件
  - templates:模板文件
    - 模板渲染：
      - render_template(‘index.html’,  msg='睡觉')#**content，关键字参数
      - 本质是分为两部分：加载，渲染，即：
        - template = Template("\<h2>呵呵\<h2>")
        - template.render()
    - 静态使用：（相当于反向解析）
      - url_for('ststic', filename='hello.css')








### flask插件



#### flask-Script

- 可以添加Flask脚本的扩展库
- 添加命令行参数‘
- 使用
  - 安装：pip install flask-script
  - 初始化：使用app构建Manageer对象
  - 调用：
    - runserver
      - -d 	使用debug模式
      - -D     不适用debug模式
      - -r       重新加载
      - -p        不重新加载
      - --threaded
    - shell

```
from flask import Flask, abort
from flask_script import Manager

#init
#将创建app变成一个方法，
def create_app():
	app = Flask(__name__)
	
	init_router(app)
	return app

#manager
#去调用创建app函数
app = create_app()
Manager= Manager（app=app）

#view
#将路由变成一个方法去调用，从而把app当作参数传给他！
def init_router(app):
	@app.route('/')
	def hello():
		return 'Hello Flask'


if __name__ == '__main__':
	manager.run()
```







#### flask-blueprint

- 用来管理路由的蓝图

- 使用过程：
  - 安装 :pip install flask-blueprint
  - 初始化：
    - 需要创建蓝图对象
      - blue = blueprint('blue',\__name__),‘’内是蓝图的名字，当有多个蓝图对象时，名字不可重复。
      - name
      - 导入名字 \__name__
    - 需要使用app进行初始化
      - 注册在app上
  - 使用：
    - 和flask对象差不多
    - 直接作为装饰器用来注册路由

```
from flask import Flask, abort
from flask_script import Manager

#init
#将创建app变成一个方法，
def create_app():
	app = Flask(__name__)
	
	#取消了这种调用的方式，将使用蓝图的路由在这里注册,,需要 impoprt App.views imorpt demo
	###init_router(app)
	#
	##app.register_blueprint(demo)
	#当蓝图对象比较多时，我们要将  以上注册蓝图交给views自己管理，创建init_view函数，放在__init__里边，这里著需要调用，将app传给他
	init_view(app=app)
	
	return app



#去调用创建app函数
app = create_app()
Manager= Manager（app=app）


#view
###将路由变成一个方法去调用，从而把app当作参数传给他！
###def init_router(app):
###	@app.route('/')
###	def hello():
###		return 'Hello Flask'
################################这个方式不好， 取消以上方式，使用蓝图

##demo是实例化了一个蓝图    当有多个蓝图的时候，为了方便管理，让views自己管理自己的蓝图
将views转换成包， 将注册蓝图交给views自己
包   views/////////记得导包

#__init__
def init_view(app):
	app.register_blueprint(demo)
	app.register_blueprint(demo2)

#111
from flask import Blueprint
demo = Blueprint('blue', \__name__)
@demo.router('/demo/')
def hello():
	return 'Hello Flask'
#222
from flask import Blueprint
demo2 = Blueprint('demo', \__name__)
@demo.router('/demo2/')
def hello():
	return 'Hello Flask2'




if __name__ == '__main__':
	manager.run()
```





#### flask-sqlalchemy

- 用来更方便地对数据库进行操作

- 使用：

  - 安装：pip install flask-sqlalchemy

  - 初始化：

    - 需要使用app进行SQLAlchemy对象创建

      - 使用懒加载方法  init_app方法搞定

    - model = SQLAlchemy（app）

      - app.config

    - SQLALCHEMY_DATABASE_URI

      - 链接数据库的路径
      - URI格式
        - 数据库+驱动://用户名:密码@主机:端口/库

    - SQLALCHEMY_TRACK_MODELCATIONS

      - 将来添加进来的一个特性
      - 默认是False

    - 使用

      - 定制模型
        - 继承自Model
        - 创建字段

      - 创建库，创建表
        - 库需要手动创建
        - 表
          - SQLAlchemy对象 .create_all
          - 删除 .drop_all
          - 不能差量更新
      - 数据操作
        - 存储
          - 创建对象：user = User()
          - model(SQLAlchemy对象).session.add(user)
          - models.session.commit()
          - models.session.add_all()#存储多个
        - 删除：基于查询
          - delete()
          - commit()
        - 查询：query.XXX
          - get
          - first

```
from flask import Flask, abort
from flask_script import Manager

#init
#将创建app变成一个方法，
def create_app():
	app = Flask(__name__)
	
	#取消了这种调用的方式，将使用蓝图的路由在这里注册,,需要 impoprt App.views imorpt demo
	###init_router(app)
	#
	##app.register_blueprint(demo)
	#当蓝图对象比较多时，我们要将  以上注册蓝图交给views自己管理，创建init_view函数，放在__init__里边，这里著需要调用，将app传给他
	init_view(app=app)
	
	#本来这里需要配置一下使用的数据库，但是考虑到环境的改变，将配置全部移到settings中！
	#app.config['SQLALCHEMY_DATABASE_URL'] = 'sqllite:///sqllite.db'
    #app.config['SQLALCHEMY_TRACK_MODIFICATIONS'] = False
	
	
	##导入model，需要配置数据库，
	#调用init_model(),把app当作参数传给model，但是由于要将三方统一放在etc下，因此移到etc中
	#init_model(app)
	#只需要统一调用init_etc(app)
	init_etc（app）
	
	#加载配置
	app.config.from_object(envs,get(env))
	
	
	return app



#去调用创建app函数
app = create_app()
Manager= Manager（app=app）


#view
###将路由变成一个方法去调用，从而把app当作参数传给他！
###def init_router(app):
###	@app.route('/')
###	def hello():
###		return 'Hello Flask'
################################这个方式不好， 取消以上方式，使用蓝图

##demo是实例化了一个蓝图    当有多个蓝图的时候，为了方便管理，让views自己管理自己的蓝图
将views转换成包， 将注册蓝图交给views自己
包   views/////////记得导包
#__init__
def init_view(app):
	app.register_blueprint(demo)
	app.register_blueprint(demo2)

#111
from flask import Blueprint
demo = Blueprint('blue', \__name__)
@demo.router('/demo/')
def hello():
	return 'Hello Flask'
#222
from flask import Blueprint
demo2 = Blueprint('demo', \__name__)
@demo.router('/demo2/')
def hello():
	return 'Hello Flask2'



#model########对模型的操作放在views中！
从etc中导入models
建立模型

#setting:用来放一些配置，把原来的数据库的配置放在settings，同时配置了项目开发所需要的四套环境。



#etc，第三方库创建的对象，例如SQLAlchemy对象
models = SQLAlchemy()

def init_ext(app):
    models.init_app(app)






if __name__ == '__main__':
	manager.run()
```





#### flask-migrate

- 用来使用数据迁移的第三方库，在flask中像Django中一样进行模型迁移
- 使用：
  - 安装：pip install flask-migrate
  - 初始化：
    - migrat = Migrate()
    - migrate.init_app(app, models)
    - 使用app和db进行初始化
    - 可以使用懒加载方法
  - 使用
    - flask db指令
      - 第一次操作init
      - migrate
      - upgrade
    - 结合flask-script使用
      - 在manager添加一个管理指令
        - manageer.add_command('db',MigrateCommand)
      - python manage db

```
在第三方里边创建：
migrate = Migrate（）

def init_ext(app):
	migrate.init_app(app,models)
	
#在manager中声明
在Manager('db', MigrateCommand)
```



#### flask-session

- 为了实现session数据持久化
- 为了改变session的位置，将session放在服务端
- 将数据存储服务器端，将数据对应的key存储在cookie中
- 嵌入级的，不需要修改源代码
- RedisSessonInterface
  - save_session
    - 将数据进行了pickle序列化
- 安装：pip install flask-session

```
切记：配置内容

SESSION_TYPE = 'redis'
SESSION_REDIS = redis.Redis(host='www.donogh.cn',port=6379,password='XXX')
```



- 使用：
  - Session（app）
  - 配置：
    - SESSION_TYPE：
    - SESSION_COOKIE_SECURE：默认False
    - SESSION_USE_SINGER：默认False
    - SESSION_REDIS: 默认：127.0.0.1:6379





#### flask-bootstrap

- 为了更方便地使用bootstrap

- 安装pip install flask-bootstrap

- 使用：
  - 初始化Bootstrap(app)
  - 继承自bootstrap/base.html.
  - 对content填坑就好了

  - html_attribs给整个html添加属性
  - html
    - head
      - title
      - metas
      - styles
    - body_attribs
    - body
      - navbar
      - content
      - scripts

#### flask -uploads

- 可以简化文件下载
- 安装：pip install  flask-uploads
- 使用：
  - UPLOAD_PHOTO_DEST = XXXXX
  - UPLOADED_PHOTO_ALLOW = IMAGE (可以点进去看有别的种类，默认为所有)
  - 创建对象：XXX = UploadSet('可以添加种类')
  - 注册加载配置：configure_uploads(app, XXXX)



#### flask-debugtoolbar

- 样式基本一致
- 安装：pip install  flask-debugtoolbar
- 初始化DebugToolbarExtension(app=app)



#### flask-cache

此版本随着flask版本更新没有升级，所以会出现bug，推荐使用flask_caching



#### flask-caching

- 使用caching

- 安装：pip install flask-caching

- 使用过程：

  - cache = Cache(config={

    	'CACHE_TYPE': “redis”

    })

  - 初始化：cache.init_app(app)

  - 使用：@cache.cached(timeout=60)



#### flask-mail

- 一个发送邮件的邮件
- 安装：pip install flask-mail
- 使用过程：
  - mail = Mail()    创建对象，
  - mail.init_app(app)     
  - 配置：
    - MAIL_SERVER = 'smtp.163.com'
    - MAIL_PORT = 25
    - MAIL_USERNAME = 'index_gt3518@163.com'
    - MAIL_PASSWORD = 'donogh1996'
    - MAIL_DEFAULT_SENDER = MAIL_USERNAME
  - 使用：
    - msg = Message('flask email',  "接受列表")
    - msg.body = "哈哈， flask 不过如此"
    - msg.html = "<h2>你真是个小天才<h2>"
    - mail.send(message = msg)





#### flask-restful

- 资源表征性转移！

- 安装：pip install flask-restful
- 使用过程：
  - 初始化：对app进行api的初始化
    - api = Api()
    - api.init_app(app)
  - 创建资源：继承自Rescoure
    - 和试图函数基本一致
    - CBV
  - 注册资源：



- 输出

  - 默认输出字典，可以直接进行序列化
  - 如果包含对象
    - 默认会抛出异常，对象不可JSON序列化
  - 使用格式化工具
    - marshal 函数
    - marshal_with 装饰器
    - 条件
      - 格式
        - 字典格式
        - 允许嵌套
        - value是fields.XXX
      - 数据
        - 允许任何格式
      - 如果格式和数据完全对应，数据就是预期格式
      - 如果格式比数据中的字段多，程序依然正常进行，不存在的字段是默认值
      - 如果格式比数据中的字段少，程序正常执行，少的字段不会显示
      - 以格式的模板为主
    - 结论：
      - 想要什么格式的返回
      - 格式工具（模板）就是什么样的
      - 和传入的数据没什么直接关系
    - 格式和数据的映射
      - 格式中的字段名和数据中的名需要一致
        - 也可以手动指定映射
        - Attribute=’property_name‘
      - 也可以对属性制定默认值
        - default
        - 指定默认值，值传递使用传进来的值
        - 未传递，则使用默认值

  - fields
    - Raw(object)
      - format()
      - output()
      - 调用顺序
        - 将数据传递进格式化工具，先获取值output，
        - 再对值进行格式化format
    - String（Raw）
      - 将value进行格式化，转成兼容的格式
      - format（）
    - Integer（Raw）
      - 重写了初始化，将default设置为0
      - format()
    - Boolean(Raw)
      - 重写了格式化，直接将value转换成bool
    - Nested（Raw）
      - 重写了output
        - 将返回值进行marshal
    - List(Raw)
      - 重写了output
        - 判断了你的类型
        - 对不同的类型进行了不同的处理
          - dict直接进行处理
          - list迭代处理
        - 重写format
          - 进行格式化
- 输入过滤
  - Request Parser
  - 使用过程：

    - 先定义一个request_parser对象 ：parser = reqparse.RequestParser()
    - 向对象中添加字段，parser.add_argument()
    - 从对象中后取字段。0

  - 对象在添加的参数的时候，可实现数据的预校验

    - required = True
    - 数据的类型
    - help=’please input‘，可以设置错误提示

    - 接受多个值，action="append"
    - 也可以指定别名 dest=""
    - location可以指定参数的来源

- 格式化


### 路由的管理

- 使用的时候容易出现循环引用的问题
- 使用懒加载的方法
  - 使用函数调用的形式进行加载
- 使用新方案解决
  - 蓝图
    - 代表的一种规划
  - 路由的规划
- flask-blueprint





### 项目结构

- 原版
  - HelloFlask.py
- 改良：
  - 三阶改装
  - manage.py
    - 项目管理文件
  - App
    - \__init__
      - 初始化文件
    - settings
      - config
      - 全局项目配置
    - ext
      - extensino扩展库
      - 除了和路由相关
    - views
      - apis
      - 路由，视图函数
    - models
      - 定制模型





### 公司开发环境

- 开发环境
  - 开发人员使用
- 测试环境
  - 测试人员使用
- 演示环境
  - 给产品看的
  - 做演戏，彩排
- 生产环境，线上环境
  - 真实环境
  - 给用户看的





### Views

#### route

- 路由：将从客户端发送过来的请求分发到指定函数上。
- 格式：\<>
  - 语法：\<converter:name>
    - int
    - float
    - string
      - 以/作为结尾。
    - path
      - 从path修饰开始，后面的东西都是我们的
      - /没有作用了。
    - uuid:
      - 只接受uuid字符串，唯一码，一种生成规则
    - any：
      - 可以同时指定多种路径，进行限定

- blue.route('/user/\<int:id>/')

- 视图函数
  - 默认支持GET，HEAD，OPTIONS
  - 其余请求默认都不支持，需要手动添加。
  - 想支持某种请求，需要手动注册
  - methods = ['GET','POST','PUT','DELETE']
  - url_for(反向解析)：url_for('函数名'， 参数名=value)

#### 异常处理

- 异常处理
  - 可以提升程序交互
  - 让程序变得友好
  - 注册errorhandler

```
@app.errorhandler(404)###全局
def hello(e):
	return 'SERVER BUSY'
	
@blue.errorhandler(404)###蓝图只能捕获本蓝图
def hello(e):
	return 'SERVER BUSY'
```





#### 终止处理

- abort
  - 本质上就是一个exception
- HttpException
  - 子类指定两个属性即可实现
  - code
  - description





#### flask文件上传

```

<form action="" method="post" enctype="multipart/form-data">
    <p>
        <input type="file" name="file">
        <input type =submit value="upload">
    </p>
</form>
```



```
def upload():
    if request.method=='POST':
        f = request.files["file"]
        base_path = path.abspath(path.dirname(__file__))
        upload_path = path.join(base_path,'static/uploads/')
        file_name = upload_path + secure_filename(f.filename)
        f.save(file_name)
        return redirect(url_for('upload'))

```



### Template

- 模板是呈现给用户的界面
- 模板组成：
  - 静态html
  - 模板语法
    - {{ var }}
      - views中传递
      - 在表达式中生成的
    - {% exp %}
      - 条件分支，可以使用简单的表达式
      - 循环 for   
        - 循环器loop

#### Jinia2

- flask中使用jinja2模板引擎
- 优点：
  - 速度快，被广泛使用
  - HTML设计和后端python分离
  - 减少Python复杂度
  - 非常灵活，快速和安全
  - 提供了控制，继承了高级功能

- marco 宏定义。

  - jinja2引入的比较独特的东西，可以实现使用函数

  ```
  {% marco hello（name）%}
  	{{name}}
  {% endmarco%}
  ```



- 模板路径
  - 默认在app下的路径
  - 如果自己想指定模板路径
    - flask创建时，指定template_folder
    - 在蓝图创建时，指定template_folder

- 可以指定url前缀作为区分
  - /xx      （记得前边有斜杠）
  - 模板中反向解析和在蓝图中使用一样





#### 静态资源

- 静态资源在falsk中是默认支持的
- 默认路径在和flask同级别的static中
- 想要自己指定
  - 可以在flask创建的时候指定static_folder
  - 也可以在蓝图中指定
- 静态资源依然是有路由的
  - endpoint是static
  - 参数有一个filename

- {{url_for('static'   filename=’XXX‘)}}



- 在模板中如果使用链接{{ url_for('blue.get_dogs_with_page') }}?page={{ page }}&per_page={{ per_page }}



### Model

- 模型
- 用来封装数据操作

#### ORM：

- ，对象关系映射，flask不存在ORM，使用插件 flask-sqlalchemy

- 将对对象的操作转换为原声SQL
- 优点：
  - 易用性，可以有效减少重复SQL
  - 资源消耗少
  - 设计灵活，可以轻松实现复杂查询
  - 移植性好
- 字段类型
  - Integer
  - SmallInteger
  - BigInteger
  - Float
  - Numeric
  - String
  - Text
  - Unicode
  - Unicode Text
  - Boolean
  - Date
  - Time
  - DateTime
  - Interval
  - 等等……
- scoped
- 约束：
  - 主键约束，
  - 外键
  - auto_increment
  - index
  - unique
  - nullable

#### 模型信息指定

- 表名

  - \__tablename__
- 模型继承：
  - 默认：不会报错，将所有数据存到一个表中，数据错乱
  - 抽象的模型是不会产生映射的！
  - 添加属性    \__abstract__ = True
  - 模型文档：flasksqlachemy

#### 数据查询

- 获取单个对象
  - first
  - get: 只能是主键。
  - get_or_404
- 获取结果集
  - all
    - 特殊，特例
    - 列表
  - filter
  - BaseQuery对象
    - \__str__输出的是这个对象数据的SQL
    - 条件
      - 类名.属性.魔术方法(临界值)
      - 类名.属性名      操作符运算符  临界值
      - offset和limit不区分顺序。都是先执行limit
      - order_by调用必须在offset和limit之前。
    - filter_by
      - 用在级联数据上
      - 条件语法精准
      - 字段 = 值
    - 级联数据
      - 获取
        - 手动实现获取
        - 使用relationsship进行级联查询
          - 反向引用
      - 关系
        - 1：1
          - Foreign Key + Unique
        - 1：M
          - ForeignKey
        - M:N
          - 额外关系表
            - ForeignKey
            - ForeignKey
  - 筛选在flask-sqlalchemy中，all如果使用只能放在最后
- 运算符：
  - contains
  - startswith
  - endwith
  - in_
  - like
  - \__gt__
  - \__ge__
  - \__lt__
  - \__le__

- 返回json数据：return jsonify(data)



#### 数据库连接池

- 怎么连接
- 连接多少个
- 默认都是有数据库连接池的

     	数据库连接池在初始化时将创建一定数量的数据库连接放到连接池中，这些数据库连接的数量是由最小数据库连接数制约。无论这些数据库连接是否被使用，连接池都将一直保证至少拥有这么多的连接数量。连接池的最大数据库连接数量限定了这个连接池能占有的最大连接数，当应用程序向连接池请求的连接数超过最大连接数量时，这些请求将被加入到等待队列中。 

		连接池基本的思想是在系统初始化的时候，将数据库连接作为对象存储在内存中，当用户需要访问数据库时，并非建立一个新的连接，而是从连接池中取出一个已建立的空闲连接对象。使用完毕后，用户也并非将连接关闭，而是将连接放回连接池中，以供下一个请求访问使用。而连接的建立、断开都由连接池自身来管理。同时，还可以通过设置连接池的参数来控制连接池中的初始连接数、连接的上下限数以及每个连接的最大使用次数、最大空闲时间等等。也可以通过其自身的管理机制来监视数据库连接的数量、使用情况等。





#### 分页器

- paginate

- 默认可以接受两个参数
  -  page
  - per_page

- Pagination
  - items
  - page
  - pages
  - prev
  - has_prev
  - pre_num
  - next
  - has_next







### flask四大内置对象

#### Response

- 服务器封装给客户端的对象

- 创建Response的三种方式
  - 直接返回字符串
  - make_response
    - 使用传递进来的资源直接构建Response。

- 参数设置
  - -data :内容
  - -code: 状态码

- render_template

  - 帮助把模板变成html字符串

- 重定向
  - redirect
  - 反向解析 url_for




#### Request

- 服务器在接受到客户端的请求后，会自动创建Request对象，由flask框架创建，是不可变对象

- 存储额是客户端的请求报文。
- 属性:
  - url：去完整请求地址
  - base_url:去掉GET参数的URL
  - host_url:只有主机和端口号的URL
  - path:路由中的路径
  - method：请求方法
  - remote_addr:请求的客户端地址
  - args:GET请求参数
  - form:POST请求参数
  - files：文件上传
  - headers:请求头
  - cookies:请求中的cookie

- args：
  - 请求参数
  - query_string
  - query_params
  - get请求参数
  - 他并不是get专属，所有的请求都能获取这个参数
- from
  - 表单数据
  - post请求参数
    - 直接支持put,patch
  - immutableMultiDict
    - 与字典得起别，可以存在相同的键。
    - args 和form都是这个类型
    - dict子类
    - 获取指定key对应的所有值
    - dict.getlist('uname')





#### Session， 会话技术

- 会话技术
  - 跨请求共享数据
  - 出现原因
    - web开发中http都是短链接
    - http请求是无状态的
  - cookie，客户端会话技术
    - 不能跨域名，不能跨浏览器
    - response.set_cookie(key,value,max_age=None,exprise=None),       
    - request.cookie.get(key)
    - max_age:整数，指定cookie过期时间。，如果为0，浏览器关闭失效。设置为None，永不过期
    - expries:整数，指定过期时间，可以指定一个具体日期。
    - response.delete_cookie(key)
    - flask中进行了默认的中文处理
  - session,服务器端会话技术，
    - session['key'] = 'value'
    - get(key,default=None)根据键获取会话的值
    - pop(key)删除某一值
    - clear()清除所有
  - flask中的session
    - 将session存储在cookie中
    - 对数据进行序列化
    - 还进行了base64
    - 还进行了zlib压缩
    - 还传递了生成签名，hash
    - 组装在一条数据
  - session时间是31天
- token







#### g

- 用来传递数据的！

- 可以跨函数传递数据





#### Config(app)

- 在模板中config
- 在python代码中,  app.config

- python  current_app
  - 一定是在项目启动之后







### 反爬

- 数据加密
- 在服务端对数据进行特定算法的加密
- 在客户端进行数据的解密
  - 在浏览器还是可破解的
  - Android或IOS移动端，破解

- 对数据进行编码
- 把数据变成动态加载。



- html中数据加密：
  - 页面数据加载修改成动态，
  - javaScript实现
  - 数据在服务端进行加密
  - 数据在客户端进行解密
  - 动态加载js
  - 控制台：集成了JavaScript环境
    - jiangnizhenggehtml加载进行







### 钩子函数

- AOP

- 面向切面编程
- 类似于Django中的中间件
- 动态介入请求流程
- 位置
  - app，优先级更高
  - blue：默认只能处理本蓝图中的。
- befor_request_request:在处理第一个请求之前
- after_request：在处理每次请求之后
- before_firest：在处理每次请求之前执行


- tardown_request:注册一个函数，同样在每次请求之后运行，注册的函数至少需要一个参数



### flask数据安全

generate_password_hash

check_password_hash

#### property

- 将函数转换成属性
- 动态敢于数据的存取







### 用户激活

- 邮箱 - flask-mail
  - 异步发送邮件
  - 在邮件中包含了激活地址
    - 激活地址接受一个一次性的token
    - token是用户注册的时候生成的，存在cache中
    - key-value
      - key token
      - value 用户的唯一标识
- 短信：- 网易云信
  - 看API文档
    - 接口路径
    - 请求方法
    - 请求参数
      - 通用header
      - CheckSum
    - 请求结果
  - 同步操作
  - request
- 登陆
  - 消息闪现
    - 基于session
    - flash（XXX）
    - get_flashed_messages()



- 数据安全
  - property：
    - 介入数据的存储过程
    - 将函数变成属性
    - setter





### RESTful

- 软体架构风格
- 实现的前后端分离
- 让后端开发者只关注数据
- flask-RESTful

- 路径是名词复数
- 不饿能出现动词
- 每个url代表一种资源
- 通过HTTP的请求为此实现资源转换
  - GET
  - POST
  - PUT
  - PATCH
  - DELETE



### 公司

- 找工作途径
  - 投递简历
    - 至关重要
    - 一定自己写
  - 内推

- 人力
  - 人力资源
    - 人员招聘
    - 员工考核
    - 社保公积金
    - 人员关系
    - 薪资管理
- 行政
  - 打杂
  - 收发快递
  - 接待访客
  - 交物业水电
  - 拉拉网线
  - 设备采购



- 技术
  - 产品经理
    - PRD
  - 项目经理CTO
  - UI（UD，UE）
  - DBA数据库工具
    - 后端
    - 移动端
    - 数据分析
  - 数据分析师
    - 爬虫
      - 金融量化交易
      - 信息采集
  - 后端
    - WEB
  - 前端
    - HTML
    - 移动端
  - 测试
    - 黑盒测试
    - 白盒测试
  - 运维



- 财务
  - 发工资
    - 工资构成
      - 全额交税和五险一金
        - 百分之十
      - 基本工资+津贴+报销款
      - 基本工资 + 绩效 + 现金
  - 期权
  - 股权



- 运营推广
  - 网络推广
    - 百度竞价
    - 各大IT论坛，贴吧
  - 线下推广
    - 地铁推广
    - 去指定区域推广
    - 小区推广
  - 口碑运营（公关）
- 销售
  - 渠道
  - 线上销售
    - 网络销售
    - 电话销售
  - 线下销售
    - 实体店（体验店）
    - 院校
    - 班主任
- 售后
  - 客服
  - 就业老师
  - 品保
    - 班主任
    - 就业老师
    - 教务
      - 稽查
      - 回访电话
- 法务
  - 律师团队





### 开发流程

- 产品经理提出需求
- 开会讨论，评审
- 要做的功能，周期
- 数据库开始
  - DBA
  - 架构师
  - 后端经验丰富的工程
  - 自己设计
- 建库建表
  - 模型建立
  - 对数据进行操作。
  - CRUD
  - 和前端进行联调
    - 前端需要请求接口
    - 接口对接
      - API文档
      - 接口地址
      - 接口所需参数
        - 哪些是必须的，那些事非必需的，哪些是通用参数
      - 接口返回数据
        - 数据字段
        - 状态码
        - 错误码
- 设计操作权限
  - 登陆才能操作
  - 权限级别
- 送测：
  - 测试工程师会有bug反馈。
- 架构
  - 框架选型
- 数据库开始







### 加班

- 弹性制工作
  - 晚到晚走
  - 最近比较忙，需要加班
    - 吃饭，交通
    - 加班费
    - 加班有统计，可以调休
  - 996
    - 早九晚九上六天



### 公司

- 常规公司
  - 通过融资进行发展的公司

- 外包公司
  - 驻地开发
    - 出差
  - 在自己公司开发

- 国企



### 公司开发历程

- 天使投资
  - PPT产品
  - 固定页面
- A轮
  - 扩大规模
- B轮
  - 优化产品
  - 占领市场
  - 对赌
- C轮
- D轮
- E轮
- IPO上市





### 淘票票：

- 

- 通用

  - 电影
    - 淘票票后端
      - 增删改查
    - 逃票票影院端
      - 查询
    - 淘票票客户端
      - 查询

  - 影票：
    - 淘票票后端
      - 增删该查
    - 影院端
      - 增
    - 客户端
      - 增查
  - 排档
    - 淘票票后端
      - 增删改查
    - 影院端
      - 增删改查
    - 客户端
      - 增删查

- 淘票票后端
  - 管理淘票票用户
  - 淘票票影院管理
  - 电影
- 淘票票影院端
  - 后端购买来的电影播放权
    - 电影
  - 放映厅



- 可扩展
  - 优惠卷
  - 积分系统
  - 影院会员系统
  - 评价系统
  - 套餐
  - 定位（手机，浏览器）
  - 地址系统
    - 后端规划好的
    - 影院端

- 系统设计
  - 客户端
    - 用户系统
    - 订单系统

### 端

- 一个项目至少有两端
  - 用户端
  - 后台管理端

- 大部分项目都是有三端的
  - 用户端：
    - web
    - 移动端
      - Android
      - IOS
    - 微信端
  - 商家端
    - web
    - 移动端
    - 微信端
  - 后台管理
    - web
    - 移动端
    - 微信端
- 我们实现使用的restful
  - 用户端的接口
  - 商家端的接口
  - 后台管理接口





### 权限

- 两种设计
  - 单个字段实现所有权限
    - Linux高格调权限设计
    - 每一种权限使用一个不重复的二进制确定
      - 2的n次幂的值
    - 优点：
      - 各种权限互不干扰
    - 包含模式权限
      - 值越大权限越多，包含值小的所有权限
  - 多表实现权限
    - 用户表
    - 权限表
    - 用户权限表（用户表和权限表多对多的关系）

数值交换

- python    a,b = b,a
- 
  - temp = a
  - a = b
  - b = temp

- 



二进制判断权限：

- r4：100

- w2：010

- x1:    001

使用值去和以上权限与，若

5：  101           



### 特殊登陆

- 扫码登陆
  - 前置条件
    - 有一个登陆好的账号
  - 使用登陆好的账号中的token来访问自己登陆接口
    - 常规登录接口
      - 用户名
      - 密码
      - 手机号
      - 邮箱
    - 特殊登录接口
      - 直接可以通过token进行登陆
    - 扫码扫出来的就是那个特殊登陆接口
- 跨应用登陆
- 三方登陆



### 城市导入脚本

- 获取城市信息
- 把数据信息读取出来

```
with open ('./data/cities.json', 'r') as city_json_file:
	#print(city_json.read())#
	cities_json_str = city_json_file.read()
	cities_json = json.loads(cities_json_str)
	return cities_json
```

- 把数据拿出来

```
insert_cities:
	cities = cities_json.get('returnValue')
	
	keys = cities.keys()    #类型就是字典
	for key in keys:
		cities_letter = cities_letter:
		
		for city in cities_letter:
			print("")
	
```

- 链接数据库

```
db = pymysql.Connect()

cursor = db.cursor()

#插入命令
cursor.excute('')

#提交
db.ocmmit()
```





### 装饰器：

面向切面编程的一部分

在不修改源代码的情况加，添加功能，添加逻辑控制

装饰器上内部函数

- *args，用来接受位置参数
  - 关键字参数默认值会自动处理
  - 如果传递关键字参数，就需要我们自己处理
    - 接收参数
    - 传递参数
  - 如果原函数拥有返回值
    - 默认只有调用的话，返回值就会被丢弃
    - 像接受返回值，要进行数据的返回



### SQLAlchemy

查询：quer

- db.session.query(Movie).get(id)
- db.session.query(Movie).join(Movie.hall_movies)

- 级联：
  - mo
  - movie



results = db.session.query(Movie.id, Movie.showname, func.sum())













### Pyinstall库

安装：pip install pyinstaller

-h 查看帮助

--clean 清理打包过程中的临时文件

-D，生成dist文件夹

-F: 

过程：

1、

2、



pyinstaller -F



pip install 



### 并发加锁

- 变并行为串行， 最烂的解决方式

- 加锁

  - 悲观锁

    - 给数据加索
    - 使用：
      - db.session.with_lockmode（mode）
      - 对此次操作加锁db.session.Query(MOvieOrder).with_lockmode('update')
      - db.session.commit()

  - 乐观锁

    - 读取的获得数据
    - 操作完成再读一遍，和预期一样

    - 使用：
      - 可以在读数据时加锁，可以在存数据的时候加锁。
      - 



### 事务

- 保证代码完整执行
- 事务开启，提交，回滚
- db.session.rollback()



try:

	movieorder = MovieOrder.query.get(1)
	
	movieorder = MovieOrder.query.get(2)

except Exception as e:

	print(e)
	
	db.session.rollback()

else:

	db.session.commit()



### 支付

- 如何确保付款

- 核心逻辑第三方平台不会暴露给后端服务器的
- 直接和支付平台对接的是客户端
- 客户端可以但会给服务器一个支付状态
  - 客户端并不可信
  - 还要有一个确保策略
  - 接受支付宝回调
    - notify_url
      - 已付款待确认就是客户端告诉你成功，但是还没有收到支付宝的回调



### flask中sqllite数据库配置



















## LINUX

### 环境变量



## 作业

爬楼梯问题

- 共有N级台阶
- 其中有M‘级是坏的，不可走的
- 人每次可以爬j-K级台阶

