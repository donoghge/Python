## Web服务模型

cs/bs:客户端和服务端的交互模型

client  browser

server web后端:python:django    flask

### MVC设计模式

软体架构风格：不是标准

将数据操作，业务处理，界面展示进行了拆分

核心思想：解耦合   松耦合 

- model：
  - 模型，封装数据的交互操作，CRUD（增删该查）
  - 是web应用程序中用来处理应用程序的数据逻辑部分，Model通常只提供功能性的借口，通过这些接口可以获取Model的所有功能。

- view：
  - 视图，负责数据的显示和呈现，View是对用户的直接输出。
  - 是用来将数据呈现给用户的。

- controller：控制器
  - 负责从用户段手机用户的输入，可以看成提供View的反向功能。主要处理用户交互。
  - 来协调model和view的关系，并对数据进行操作。

  ![](C:\Users\DELL\AppData\Local\Temp\1537541104347.png)

流程：控制器接受用户请求，调用模型，获取数据，控制器将数据展示到视图中。

![](C:\Users\DELL\AppData\Local\Temp\1537541458982.png)



### MTV模式简介

本质上就是MVC 变种

- Model：负责业务对象与数据库的对象。

- template 模板：负责把页面展示给用户

  只是一个人html充当的是MVC中view的角色，用来做数据展示

   views	视图函数

  - 负责业务逻辑，并在适当的时候调用Model和Template。





## Django简介

j基于python的超重量级web框架，2005开源，新闻站点

重量级   体开发者想了太多的事情，帮开发者做了很多选择，内置了很多的功能

适用版本1.11.x   LTS    以后学2.2

### 创建项目

	django-admin startproject XXX
	创建app
	django-admin startapp xxx     //   python manage.py startapp app


	
	启动项目  python  manage.py   runserver :
	使用开发者服务器启动项目
	默认会启动在本机的8000端口上
	还可以添加参数

### 项目结构

```
manage.py:管理整个项目的文件
	以后的命令基本都是通过它来调用
```

xxx：

```
__init__  
settings 项目全局配置文件
urls	跟路由
wsgi    用在以后项目部署上，前期用不到
```

### 虚拟化技术

```
虚拟机
虚拟容器
	docker
虚拟环境
	python专用
	将python依赖隔离
```



### 创建虚拟环境

```
windows安装：
pip install virtualenv
pip install virtualenvwrapper-win
创建虚拟环境
mkvirtualenv   虚拟环境名    //默认为系统环境变量配置
安装Django
1、进入虚拟环境，
2、pip install django==1.11.7


mkvirtualenv
deactivate
workon
rmvirtualenv

安装 pip install django:pip install django==1.11.7或者pip install django==1.11.7 -i http://pypi.douban.com/simple
```

另一种使用方式：

- virtualenv
- linux下：
  - virtualenv   XXX：创建虚拟环境
  - source：      bin/activate
  - deactivate
  - rm -rf xxx: 删除
  - 指令在那调用，虚拟就在哪生成
- windows下
  - virtualenv  
  - 激活： 进入activate所在目录， /xx/xx/activate
  - 退出：进入activate所在目录， /xx/xx/deactivate.bat

### 开发环境

```
VMware
	虚拟机软件
	Workstation
Ubuntu基本使用
	root
	普通用户
		申请root权限sudo
linux梓潼中有两种常用系统包管理工具yum和apt。
低版本中安装白使用apt-get  新的只需要写apt就可以了。
apt指令（兼容apt-get和apt-cache）
	apt install XXX  安装某种软件
	apt remove   XXX 移除XXX软件
	apt autoremove XXX 移除XXX软件和自动安装且不适用的包
```

#### ubantu基本使用快捷键

```
control+alt+	打开终端
cd     进入目录
tree	树形查看
mkdir	创建文件夹
rm		删除
touch	创建文件
control + p 参数提示
shift + f6 重命名，重构
.retu  快捷生成return
. if   
control+d	复制一行，插入到下面
alt+shift+↑	移动一行
```

### 模板配置

1、**在app中进行模板配置**

- 只需要在APP的目录创建templates文件夹即可

- 如果想要让代码自动提示，我们应该标记文件夹为模板文件夹

2、**在项目目录中进行模板配置（开发中使用这一种）**

- 需要在项目目录中创建templates文件夹并标记

- 需要在settings中进行注册

  ```
  os.path.join(BASE_DIR, 'templates'),
  ```

### APP的添加方法

- 直接添加	'App',
- 'Two.apps.TwoConfig',

### 路由器优化配置

- 项目如果逻辑过于复杂，可以进行拆分

- 拆分为多个app，，继而拆分路由  新建urls目录

  - 在APP中创建自己的urls，  
    - urlpatterns 路由规则列表
    - 在根urls中进行子路由的包含

  - 子路由使用
    - 根路由规则 + 子路由规则



### 链接mysql驱动

- msyqlclient
  - python2,3都能直接使用
  - 知名缺点
    - 对mysql安装有要求，必须指定位置存在配置文件
- python-mysql
  - python2支持很好
  - python3不支持
- pymysql
  - python2，3都支持
  - 它还可以伪装成前面的库

### 数据库配置

```
'ENGINE': 'django.db.backends.mysql',
'NAME': 'GP1HelloDjango',
'USER': 'root',
'PASSWORD': 'rock1204',
'HOST': '127.0.0.1',
'PORT': '3306',
```

- 生成迁移文件 python manage.py makemigrations
- 进行迁移  python  manage.py migrate





## Model

在企业开发中，我们通常都是从数据开始开发的。

Django对各种数据库都提供了很好的支持，对不同的数据，Django提供了统一调用的API。



### ORM

(Object Relational Mapping) 对象关系映射（理解为翻译机）

- 核心思想：解耦合
- 将业务逻辑和SQL进行了解耦合
  - object.save()
  - object.delete()

- 关系型数据库

  - DDL
  - 通过models定义实现，数据库表的定义

- 数据操作

  ```
  存储
  object.save()
  查看所有
  student.objects.all()
  查看单个
  student.objects.get()//不会报异常
  更新和删除都是基于查询
  
  ```



### 数据库中数据类型

- 字符串
- 数字
- 日期时间

### 定义属性

##### django根据属性的类型确定一下信息：

- 当前选择的数据库支持字段的类型
- 渲染管理表但是使用的默认html控件
- 在管理站点最低限度的验证
- Django会为表增加自动增长的主键列，每个模型只能有一个主键列，如果使用选项设置某属性为主键列后，则django不会在生成默认的主键列

##### 属性命名限制：

- 遵循表示规则。
- 由于Django的查询方式，不允许使用连续的下划线，

##### 库

- 定义属性时，需要字段类型，字段类型被定义在django,db.models.fileds目录下，为了方便实用，被导入到django.db.models中
- 使用方式：
  - 导入from django.db.  import models
  - 通过models.field创建字段类型的对象，赋值给属性
- 逻辑删除
  - 对于重要的数据都做逻辑删除，不做物理删除，实现方法是定义ISDELETE属性，类型为BooleanField，默认为False。

z



##### 字段类型

```
·AutoField
	·一个根据实际ID自动增长的IntegerField，通常不指定如果不指定，一个主键字段将自动添加到模型中
CharField(max_length=字符长度)
	·字符串，默认的表单样式是 TextInput
TextField
	·大文本字段，一般超过4000使用，默认的表单控件是Textarea
IntegerField
	·整数
DecimalField(max_digits=None, decimal_places=None)
	·使用python的Decimal实例表示的十进制浮点数
	·参数说明
		·DecimalField.max_digits
			·位数总数
		·DecimalField.decimal_places
			·小数点后的数字位数
FloatField
	·用Python的float实例来表示的浮点数

BooleanField
	·true/false 字段，此字段的默认表单控制是CheckboxInput

NullBooleanField
	·支持null、true、false三种值

DateField([auto_now=False, auto_now_add=False])
	·使用Python的datetime.date实例表示的日期
	·参数说明
		·DateField.auto_now
			·每次保存对象时，自动设置该字段为当前时间，用于"最后一次修改"的时间戳，它总是使用当前日期，默认为false
		·DateField.auto_now_add
			·当对象第一次被创建时自动设置当前时间，用于创建的时间戳，它总是使用当前日期，默认为false
	·说明
		·该字段默认对应的表单控件是一个TextInput. 在管理员站点添加了一个JavaScript写的日历控件，和一个“Today"的快捷按钮，包含了一个额外的invalid_date错误消息键
	·注意
		·auto_now_add, auto_now, and default 这些设置是相互排斥的，他们之间的任何组合将会发生错误的结果

·TimeField
	·使用Python的datetime.time实例表示的时间，参数同DateField

·DateTimeField
	·使用Python的datetime.datetime实例表示的日期和时间，参数同DateField

·FileField
	·一个上传文件的字段

·ImageField
	·继承了FileField的所有属性和方法，但对上传的对象进行校验，确保它是个有效的image
```

##### 字段选项

- 通过字段选项，可以实现对字段的约束。
- 在字段对象时通过关键字参数指定

```
·null
·如果为True，Django 将空值以NULL 存储到数据库中，默认值是 False

·blank
·如果为True，则该字段允许为空白，默认值是 False

·注意
·null是数据库范畴的概念，blank是表单验证证范畴的

·db_column
·字段的名称，如果未指定，则使用属性的名称

·db_index
·若值为 True, 则在表中会为此字段创建索引

·default
·默认值

·primary_key
·若为 True, 则该字段会成为模型的主键字段

·unique
·如果为 True, 这个字段在表中必须有唯一值
```

##### 关系

```
分类
ForeignKey：一对多，将字段定义在多的端中
ManyToManyField：多对多，将字段定义在两端中
OneToOneField：一对一，将字段定义在任意一端中

用一访问多
格式
对象.模型类小写_set
示例
grade.students_set

用一访问一
格式
对象.模型类小写
示例
grade.students

访问id
格式
对象.属性_id
示例
student.sgrade_id
```

### 迁移

- 迁移原理
  - 生成迁移
  - 执行迁移
- 迁移原理
  - 根据既有迁移进行对比，生成新的迁移文件
  - 去数据库中查询执行局路，直接过滤掉已执行过的迁移文件
  - 执行未执行的迁移文件，并记录

### 模型过滤

- filter

- exclude

- 连续使用

	链式调用
	Person.objects.filter().filter().xxxx.eclude().exclude().yyyy

### 切片

- 和python中的切片不太一样
- QuerySet[5：15]获取第5条到第十五条数据
  - 相当于SQL中limit和offset

### 方法

- 对象方法 
  - 可以调用对象的属性，也可以调用类的属性
- 类方法
  - 不能调用对象属性
- 静态方法
  - 啥都不能调用，不能获取对象属性，也不能获取类属性
  - 只是寄生在我们这个类上而已

### 状态码

- 2XX：请求成功
- 3XX：转发或重定向
- 4XX：客户端错误
- 5XX：服务端错了

### 查询条件

属性\ __运算 = 值

- gt
- lt
- gte
- lte
- in      在某一集合中
- contains   类似于    模糊查询    like
- startswith       以XX开始    本质也是like
- endswith        以XX结束，  本质也是like
- exact 
- 前面同时添加i，ignore   忽略
  - iexact
    - icontains
    - istartswith
    - iendswith
- django中查询条件有时区问题
  - 关闭django中自定义的时区
  - 在数据库中创建对应的时区表

### 缓存集

filter

exclede

all

- 都不会真正去真正的查询数据库
- 只有我们在迭代结果集，或者获取单个对象属性的时候，他才会去查询数据库
- 懒查询
  - 为了优化我们结构和查询

### Q

- 可以对条件进行封装
- 封装以后，可以支持逻辑运算
  - 与	&	and
  - 或     |       or
  - 非       ~     not

### F

- 可以获取我们属性的值
- 可以实现一个模型的不同属性的运算操作
- 还可以支持算术运算

### 模型关系

- 1：1：

  - 使用models.OneToOneField()进行关联

  - class Card（models.Model）:

    	person = models.OneToOneField(Person)

  - 绑定卡余人的一对一关系，默认情况下，当人被删除的情况下，与人绑定的卡就也删除了，这个可以使用on_delete进行调整

  - on_delete

    - models.CASCADE		默认值
    - models.PROTECT          保护模式
    - models.SET_NULL        置空模式
    - models.SET_DEFAULT      置默认值
    - models.SET()                   删除的时候重新动态指向一个实体

  - 访问对应元素     person.pcard

- 1：N

  - 直接使用外键实现		models.ForeignKey
  - 主从：多是从
  - 级联对象获取
    - 从获取主	：显性属性
    - 主获取从:隐形属性
      - 默认是：级联数据_set

- M ：N

  - ManyToManyField

  - 两张以上表之间的关系

  - 会产生额外的关系表：

    - 表中使用多个外键实现
    - 外间对应关系表中的主键

  - 数据获取：

    - 两种表的结构完全一样

    - 从获取主：

      - Manager对象
        - all
        - filter
        - exclude
        - 操作级联数据
          - add
          - remove
          - clear
          - set

      - 显性属性

    - 主获取从

      - 隐形属性
      - Manager对象

- 模型继承

  - 默认一个模型在数据库映射一张表
  - 如果模型存在继承的时候，父模型产生表映射
    - 子模型对应的表会通过外间和父表产生关联
  - 关系型数据库性能：
    - 数据量越大性能越低
    - 关系越多越复杂型性能越低
  - 抽象模型
    - 在model的元信息中添加abstract = True
    - 抽象的模型不会再数据库中产生表
    - 子模型拥有夫模型中的所有字段



### 模型成员

- 显性属性：开发者手动书写的属性。

- 隐形属性：
  - 开发者没有书写，ORM自动生成的
  - 如果你把隐形属性手动声明了，系统就不会为你产生隐形属性了。

### 静态资源

- 静态文件配置

动静分离

创建静态文件夹

在setting中注册STATICFILES_DIRS=[]

在模板中使用

	先加载静态资源{% %}
	
	使用{%  static ‘XXX %}

仅在debug模式可以使用



## template

在Django框架中，模板是可以帮助开发者快速生成呈现给用户页面的工具

	模板的设计方式实现我们MVT中VT的解耦，VT有着N：M的关系，一个V可以调用任意一个T，一个T可以供任意V使用。

模板处理分为两个过程：

1、加载

2、渲染

### 模板主要有两个部分

	1、HTML静态代码
	
	2、动态插入的代码段（挖坑，填坑）

模板中的动态代码段除了做基本的静态填充，还可以实现一些基本的运算，转换和逻辑。

### 模板中的变量：

	1、试图传递给模板的数据
	2、遵守标识符规则
	3、语法{{ var }}
	4、如果变量不存在，则擦汗如空字符串

模板中的语法 grades      grade

	字典查询
	
	属性或者方法	grade.gname
	
	索引	grades.0.gname

模板中的标签：

	语法{% tag %}

### 静态资源

- 动静分离

- 创建静态文件夹

- 在setting中注册        

  ```
  STATIC_URL = '/static/'
  STATICFILES_DIRS = [
      os.path.join(BASE_DIR, 'static')
  ]
  ```

  在模板中使用

  ```
  示例：
  {% load static %} #第一步，先加载静态文件，之后调用静态，就不用写绝对全路径
  
  src="{% static 'js/login.js' %}"
  ```

- 坑点
  - 仅在Debug模式可以使用
  - 以后需要自己单独处理



### 给模板加CSS，js

js，css添加到static中

- 先挖坑

  - {%  block  ext_css%}            

     {%   endblock %}

  示例：

  ```
  {% block ext_css %}
  {#    <link rel="stylesheet" href="/static/css/home_mine.css">#}
      <link rel="stylesheet" href="{% static 'css/home_mine.css' %}">
  {% endblock %}
  ```



结构标签





### 结构标签

- block
  - 块，用来规划我们的布局（挖坑）
  - 首次出现，代表规划
  - 第二次出现，代表填充以前的规划
  - 第三次出现，代表填充以前的规划，默认动作是覆盖
    - 如果不想覆盖，可以添加{{  block.super  }}
    - 这样就实现了增量式操作
- extends
  - 继承
  - 可以获取夫模板中的所有结构
- block+entends
  - 化整为零
- include
  - 包含
  - 可以将页面作为一部分，嵌入到其他页面中
- include   +   block
  - 由零聚一
- 三个标签也可以混着用，能用block+extends搞定的，就尽量不要使用include
- 如果我们继承自一个覆膜板，子模版自由直接重写页面结构是不生效的。



## views

### 视图概述：

- Django中的视图主要是用来接收web请求，并作出响应。 

- 视图的本质就是一个Python中的函数
- 视图的响应分为两大类：
  - 以json数据形式返回
  - 以网页的形式返回
    - 重定向到另一个网页
    - 错误视图
- 视图响应过程：浏览器输入->django获取信息并去掉IP：端口，剩下路径->urls路由匹配

->视图响应->回馈到浏览器

### urls

- 路由匹配规则：
  - 按照列表德尔书写顺序进行匹配的，从上到下，没有最优匹配的概念
- 路由规则编写
  - 匹配的正则前方不需要加反斜线
  - 我们通常直接指定以^开头，在结尾处直接添加反斜线
- 路由中的参数使用（）进行获取
  - 一个圆括号对应试图函数中的一个参数
  - 接收参数
    - 路径参数
    - 位置参数：
      - 按照书写顺序进行匹配
      - 参数个数和试图函数上的参数一致
    - 关键字参数：
      - 按照参数名称匹配，和顺序就无关了。
      - 可以在圆括号指定参数名字
  - 参数个数必须和试图函数中参数个数一致（除了默认的request以外）

### url：

	根路由会使用include形式将整个子路由添加进来
	第一个参数：正则匹配的路径
	第二个参数	包含那个路由
	第三个参数	namespace
	在子路由中，前后两个参数一致
	示例：
	url（r'^index',views.index,name='index'）
	
	导入其他url配置
	
	from django.conf.urls import include
	url(r'^XXX/', include('app.urls'))


### 获取url路径上的参数

```
url（‘^grade/(\d+)$’, views.getStudent）,
注意：
	url匹配中添加了（）取参，在请求调用的函数中必须接受
def  getStudents(request, classld)


也可以使用关键字参数
url（r'^news/(?P<year>\d{4})/(?P<month>\d+)/',views.getNews）
```



### 反向解析

- 在模板中使用

```
{% url 'namespace:name'%}

如果存在位置参数
{% url  'namespace:name' value1  value2……  %}

如果带有关键字参数
{% url  'namespace:name' key1=value1  key2=value2 %}
```

- 根据根路由中注册的namespace和在子路由中注册name，这两个参数来动态获取我们的路径。



### Request

- 内置属性：包含了请求各种信息
  - method：get     post
  - path：请求的完整路径
  - encoding：编码方式：常用UTF8
  - GET：
    - 类字典结构
    - 一个key允许对应多个值
    - get、 getlist
  - POST
  - FILES：类似字典的参数，包含了Cookie
  - Session：类似字典：表示会话
  - META：  客户的元信息：包括远端访问IP（REMOTE_ADDR）
- 方法：
- is_ajax()判断是否是Ajax（），通常用在移动端和JS中

### 图片上传

- 文件数据存储在request.FILES属性中

- form表单上传文件需要添加enctype='multipart/form-data',文件上传必须使用POST请求方式。

- 存储：

  - 在static文件夹下创建uploadfiles用于存储接收上传的文件
  - MEDIA_ROOT=os.path.join(BASE_DIR,r'static/uploadefiles')

  示例代码：

  ```
  <form method='post' action='xxx' enctype='multipart/form-data'>
  	{% csrf_token %}
  	<input type='file' name='icon'>
  	<input type='submit'  value='上传'>
  <form>
  
  def savefIcon(request):
  	if request.method == 'POST'
  		f = request.FILES['icon']
  		filePath = os.path.join(settings.MEDIA_ROOT,f.name)
  		with open(filePath,'wb) as fp:
  			for part in f.chunks():
  				fp.write(part)
  
  ```





### HttpRequest

- 视图的本质就是一个函数

- 视图参数

  - 一个HttpRequest的实例
  - 通过正则表达式获取过来的参数

- 位置：通常在应用下的Views.py中定义

- 自定义错误视图，

  - 在工程的templates文件夹下创建对应的错误文件
  - 获取亲求路径{{request_path}}
  - 在文件中定义自己的错误样式
  - 注意需要再关闭Debug的情况下才可以
  - 没有关闭Debug的情况下会在界面直接显示Log

- 服务器在接收到Http请求后，会根据报文创建HttpRequest对象

- 视图中的第一个参数就是HttpRequest对象


### Response

```
HttpResponseRedirect: 响应重定向，暂时，可以实现服务器内部跳转。
	return HttpResponseRedict('/grade/2017')
使用的时候推荐使用反向解析

JsonResponse
返回Json数据的请求，通常用在异步请求上
JsonResponse（dict）
也可以使用\ __init__(self,data)设置数据

Content-type是application/json

```

- locals
  - 内置函数
  - 将局部变量使用字典的方式进行打包.
  - key是变量名，value是变量中存储的数据。





### HttpResponse

- 服务器返回给客户端的数据
- HttpResponse由程序员自己创建
  - 不使用模板，直接HttpResponse（）
  - 调用模板，进行渲染
    - 先Load模板，在渲染
    - 直接使用render一步到位
- 参数：
  - request：请求体对象
  - 模板路径
  - 字段参数，用来填坑
- 属性：
  - content：返回的内容
  - charset：编码格式
  - status_code:响应状态码
  - content-type：MIME类型
- 方法：
  - init:初始化内容
  - write(XXX):直接写出文本
  - flush():冲刷缓冲区

```
HttpResponseRedirect	重定向，暂时	302 简写	redirect
JsonResponse	以Json格式返回数据 指定content_type 为application/json
HttpResponsePermanentRedirect	重定向，永久性	301
HttpResponseBadRequest 	400
HttpResponseNotFound	404
HttpResponseForbidden 	403		被禁止
HttpResponseNotAllowed 	405
HttpResponseServerError 500		服务器内部错了
Http404
  - Exception
  - raise 主动抛异常出来
```

	

### MIME

- 作用：制定传输数据使用哪种形式打开

- 格式：大类型/小类型

### 会话技术

- 出现场景：
  - 服务器如何识别客户端
  - Http在WEB开发中基本都是短链接

- 请求生命周期：Request开始，  Response结束。

#### cookie

客户端会话技术：数据存储在客户端 \ __ init__

	键值对存储
	支持过期时间
	默认Cookie会自动携带，本网站所有Cookie
	Cookie不能跨域名，不能跨网站
	通过HttpResponse
	Cookie默认不支持中文
	可以加盐
		加密
		获取的时候需要解密

#### Session

	服务端会话技术
	
	数据存储在服务器
	
	默认Session存储在内存中
	
	Django中默认会把Session持久化到数据库中
	
	Django中Sessoin的默认过期时间是14天
	
	主键是字符串
	
	数据是使用了数据安全
		使用的base64
		在前边添加了一个混淆串
	Session依赖于Cookie

删除

- del request.session['username']

- response.delete_cookie(session_id)

session、 cookie一起删除

- request.session.flush()



#### Token

```
服务端会话技术
自定义的Session
如果web页面开发中，使用起来和Session基本一致
如果使用在移动端或客户端开发中，通常以json形式传输，需要移动端自己存储Token，需要移动端自己存储Token，
需要获取Token关联数据的时候，主动传递Token


Cookie和Session。Token对比
Cookie使用更简洁，服务器压力更小，数据不是很安全
Session服务器要维护Session，相对安全
Token拥有Sesson的所有优点，自己维护略微麻烦，支持更多的终端。

```

### csrf

- 防跨站攻击，

- 防止恶意注册，确保客户端是自己的客户端

- 使用了cookie中的crsftoken进行验证，传输

- 服务器发送给客户端，客户端将cookie获取过来，还要进行编码转换（编码安全）

**如何实现？**

	在我们存在csrf_token标签的页面中，响应会自动设置一个cookie，csrftoken。
	
	当我们提交的时候，会自动验证crsftoken。
	
	验证通过，正常执行以后流程，验证不通过，直接403.



### 算法：

- 编码解码

  - Base64，  Unicode

- 摘要算法，指纹算法，杂凑算法，
  - MD5，SHA

	MD5默认128的二进制
	
	32位的十六进制
	
	32位的Unicode

单项不可逆的

不管输出多正常，输出都是固定长度

只要输入有意思的变更，输出都会发生巨大的变化

加密：

	对称加密：DES   AES
	
		一把钥匙
	
		加密解密效率高
	
		钥匙一旦丢失，所有数据就全玩完了
	
	非对称加密 RSA  PGP
	
		两把钥匙
	
		公钥和私钥
	
		安全性最高

算法复杂，需要的时间长：支付宝，微信都是RSA

### Json

- jsonobject
  - {}
  - key-value
- JsonSrray
  - []
  - 列表中可以是普通数据类型也可以是JsonObject
- JosnObject和JsonArray可以嵌套
- 给移动端的json
- 给Ajax
  - 前后端
  - DRF



## REDIS工具

- 存储中间数据的一种介质

- 提升服务其相应速度

- 将执行过的操作数据存储下来，在一定时间内，再次获取数据的时候，直接从缓存获取。
- 比较理想的方案，缓存使用内存级缓存
- Django内置缓存框架

### cache缓冲区

- 缓存框架的和性能目标

  - 较少的代码
    - 缓存应该尽可能快
    - 因此围绕缓存，后端的所有框架代码应该保持在绝对最小值，特别是对于获取数据
  - 一致性：
    - 缓存api应该是提供跨越不同缓存后端的一致接口
  - 可扩展性
    - 基于开发人员的需求，缓存API应该可以在应用程序级别扩展

- 缓存：几种常用的缓存。

  -  基于Memercached缓存

  -  使用数据库进行缓存

  - 使用文件系统进行缓存

  -  使用本地内存进行缓存

  -  提供缓存扩展接口

- 缓存配置

  - 1、创建缓存表：

  python   manage.py    createcachetable   my_cache_table

  - 缓存配置：

```
CACHES = {
    'default': {
        'BACKEND': 'django.core.cache.backends.db.DatabaseCache',
        'LOCATION': 'my_cache_table',
        'TIMEOUT': 60 * 5
    },
    
	#如果配置redis
	'redis_backend': {
        "BACKEND": "django_redis.cache.RedisCache",
        "LOCATION": "redis://127.0.0.1:6379/1",
        "OPTIONS": {
            "CLIENT_CLASS": "django_redis.client.DefaultClient",
            "PASSWORD": 'XXXXXX',
        }，
        //可以添加默认过期时间，也可以不设置！
        TIMEOUT：24 * 60 * 60
    }，
    
}
```

使用装饰器的用法

```
@cache_page(30)   #括号内是保存时间
def news(request):
    sleep(3)
    students = Student.objects.all()
    data = {
        "students":students
    }
    response = render(request,'news.html',context=data)
    return response
```

- 如果是redis数据库

```
@cache_page(60, cache='redis_backend')   #######
def jokes(request):

    sleep(5)
    return HttpResponse('JokeList')
```

不使用装饰器：

```
def news(request):

    result = cache.get("news")  #从缓存获取：news
    if result:					#存在
        return HttpResponse(result)

    sleep(3)

    students = Student.objects.all()

    data = {
        "students":students
    }
    response = render(request,'news.html',context=data)

    cache.set("news",response.content, timeout=60)  #设置缓存

    return response
```









### 存储session：

pip install django-redis-session(有坑)

```
SESSION_ENGINE = 'redis_sessions.session'
SESSION_REDIS = {
    'host': 'localhost',
    'port': 6379,
    'db': 4,
    'password': 'yxgw',
    'prefix': 'News_hodge',
    'socket_timeout': 60*6
}

```







## 中间件

- 是一个轻量级的，底层的插件，可以介入Django的请求和相应过程（面向切面编程）。
- 中间件的本质是一个Python类。
- 面向切面编程，简称AOP，AOP的主要实现目的是针对业务处理过程中的切面进行提取，她锁面对的是处理过程中的某个步骤或阶段，以获取逻辑过程中各部分之间低耦合的隔离效果。



### 中间件的可切入点

client  ->process_request[]

逐一进行process

process_request -> urls

urls ->process_view[]

逐一进行process_view

process_view->views

views ->models

models ->views

views ->response

response ->process_response[]

逐一进行process_response



URL

1.DNS解析，abcde.com------>12.23.45.56

2.跟服务器简历TCP连接

	1.三次握手

3.封装，请求报文。

4. 将报文发送给浏览器
5. HTTP Server就收数据
6. WSGI处理数据
7. WSGI讲请求数据，封装成HTTP Request对象
8. 将HTTP Request对象交给Web Server处理
9. URL Mapping ->views
10. view内部进行逻辑，数据等相关处理->得到结果数据
11. 模板渲染
12. 将最终结果封装成HTTP Response对象
13. WSGI 将HTTP Response对象封装成‘’响应报文“
14. HTTP Server将保温数据返回给浏览器
15. 客户端断开连接
    1. 四次挥手
       1. client->FIN->sever
       2. client<-ACK<-server
       3. client<-FIN<-server
       4. client->ACK->server
16. 客户端解析响应报文
17. 页面渲染





### 切入函数

```python
__init__:没有参数，服务器响应第一个请求的时候自动调用，用户确定是否启用该中间件。

process_request(self,request）：在执行视图前被调用，每个请求上都会调用，不主动进行返回或返回HTTP Response对象。

process_view(self,request,view_func,view_args,view_kwargs)：调用视图之前执行，每个请求都会调用，不主动进行返回或返回HttpResponse对象。

process_template_response(self,request,response):在视图刚好执行完后进行调用，每个请求都会调用，不主动进行返回或返回HttpResponse对象。

process_response(self,request,response):所有响应返回浏览器之前调用，每个请求都会调用，不主动进行返回或返回HttpResponse对象。

process_exception(self,request,exception):当视图抛出异常时调用，不主动进行返回或返回HttpResponse对象。
```

### AOP中间件

- 1、实现统计功能
  - 统计Ip
  - 统计浏览器
- 实现权值控制：
  - 黑名单
  - 白名单
- 实现反爬：
  - 反爬虫：十秒之内只能搜索一次
  - 实现频率控制
- 界面友好化
- 应用交互友好化





### 自定义中间件流程

- 1、在工程目录下创建middleware目录

- 2、在目录创建一个Python文件

  - 文件名（LearnMiddle.py）

- 3、在Python文件导入中间件的基类

  ```
  from django.utils.deprecation import MiddlewareMixin
  
  class HelloMiddle（MiddlewareMixin）：
  	pass
  ```

- 4、注册

  ```
  MIDDLEWARE = [
  	'middleware.LearnMiddle.HelloMiddle',
  	####  middleware.文件名.类名
  ]
  ```

- 5、在类中根据功能需求，创建切入需求类，重写切入点方法

  ```
  class LearnAOP(MiddlewareMixin):
  		def process_request(self,request):
  			print('request的路径',request.GET.path)
  ```

#### 示例1：

```
class HelloMiddle(MiddlewareMixin):
    def process_request(self,request):
        print(request.META.get("REMOTE_ADDR"))

        #可以根据不同的路由编写不同的需求
         if request.path == "/newapp/news/":
             return HttpResponse("测试")
```



#### 示例2   防止爬虫关进小黑屋：

```
 if request.path == "/app/search/":
             result = cache.get(ip)
             if result:
                 return HttpResponse("您的访问过于频繁，请10秒之后再次搜索")
             cache.set(ip, ip, timeout=10)

         black_list = cache.get('black',[])
        
         if ip in black_list:
             return HttpResponse("黑名单用户，凉凉")
        
         requests = cache.get(ip, [])
        
         while requests and time.time() - requests[-1] > 60:
             requests.pop()
        
         requests.insert(0, time.time())
         cache.set(ip, requests, timeout=60)
        
         if len(requests) > 30:
             black_list.append(ip)
             cache.set('black', black_list, timeout=60*60*24)
             return HttpResponse("小爬虫小黑屋里呆着吧")
        
         if len(requests) > 10:
             return HttpResponse("请求次数过于频繁，小爬虫回家睡觉吧")
```





### 分页

- django提供了分页的工具，存在于django.core中
  - Paginator：数据分页工具
  - page：具体的某一页面
- Paginator：

  - 对象创建：Paginator（数据集，每一页数据数）
  - 可以获取某一页，也可以获取所有页码，也可以获取有多少数据，多少页
  - 属性：
    - count对象总数
    - num_pages:页面总数
    - page_range:页码列表，从1开始
  - 方法：
    - page（整数）：获得一个page对象
  - 常见错误：
    - InvalidPage：page（）传递无效页码
    - PageNotAnInteger：page（）传递的不是整数
    - Empty：page（）传递的值有效，但是没有数据



- Page
  - 对象获得，通过paginator的Page（）方法获得

  - 属性
    - object_list:  当前页面上所有的数据对象
    - number：当前的页码值
    - paginator：当前page关联的Pageinator对象
  - 属性
    - has_next(): 判断是否有下一页
    - has_previous():判断是否有上一页
    - has_other_pages():判断是否有上一页或下一页
    - next_page_number():返回下一页的页码
    - previous_page_number():返回上一页的页码
    - len():返回当前页的数据的个数

```
原生分页：需要传值：  page   per_page
def get_students(request):
    page = int(request.GET.get("page", 1))
    per_page = int(request.GET.get("per_page", 10))


    students = Student.objects.all()[per_page*(page-1): page * per_page]
    data = {
        "students": students
    }
    return render(request, 'students.html', context=data)
```

- 框架实现分页





### 验证码（画布）

- 验证码需要使用绘图pillow：   pip  install  Pillow
- 核心：Image   ImageDraw   ImageFont

```
#随机一个色调
def get_color():
    return random.randrange(256)
    
#随机四位字符
def generate_code():
    source = "qwertyuiopasdfghjklzxcvbnm1234567890QWERTYUIOPASDFGHJKLZXCVBNM"
    code = ""
    for i in range(4):
        code += random.choice(source)
    return code
```

-- -- 上边是工具类

```
def get_code(request):
    #初始化画布，初始化画笔
    mode = “RGB”
    size = （100， 100）
    
    red = get_color()
    green = get_color()
    blue = get_color()
    
    
    #生成画布颜色
    color_bg = (red,green,blue)
    #画布
    image = Image.new(mode=mode, size=size, color=color_bg)
    #画笔
    imagedraw = ImageDraw（image，mode=mode）
    #字体设置
    imagefont = ImageFont.truetype(setting.FONT_PATH,100)
    
    #随机生成了一个四位字符
    verify_code = generate_code()
    #设置session，方便登陆验证！！
    request.session['verify_code'] = verify_code
    
    ###fill为填充
 	for i in range(4):
    	fill = (get_color(), get_color(), get_color())
    	imagedraw.text(xy=(50*i, 0),text=verify_code[i],font=imagefont,fill=fill)
    
    #背景干扰点
    for i in range(10000):
        fill = (get_color(), get_color(), get_color())
        xy = (random.randrange(201), random.randrange(100))
        imagedraw.point(xy=xy, fill=fill)
    
    
    fp = BytesIO（）#造一个字节的IO流
    #fp()存的位置       第二个参数是格式
    image.save(fp,  "png")

    return HttpResponse(fp.getvalue(), content_type = "image/png")

```

设置字体需要配置

![img](E:/%E6%9C%89%E9%81%93%E4%BA%91%E7%AC%94%E8%AE%B0/index_gt3518@163.com/b8fb125aece446b8bd092790229c7437/clipboard.png)





验证码点击切换的js

```
$(function () {
    $("img").click(function () {
        console.log("点到我了");
        $(this).attr("src", "/app/getcode/?t=" + Math.random());
    })

})
```





**csrf_exmpt	豁免** post请求需要添加

### 富文本

- Rich Text Format，是由微软开打的跨平台文档格式，大多数的文字处理软件都讷讷感读物和保存RTF文档，起始就是可以添加央视的文档，和HTML有很多相似的地方。

- tiny插件

- django的插件

  - pip install django-tinymce

- 用处大约有两种

  - 在后台管理中能够使用
  - 在页面中使用，通常用来做博客

- 后台中使用：

  - 配置settings.py文件
    - INSTALLED_APPS添加tinymce应用
    - 添加默认配置

  ```
  TINYMCE_DEFAULT_CONFIG = {
  		'theme':'advanced',
  		'width':800,
  		'height':600,
  }
  ```

  - 创建模型类

```
from tinymce.models import HTMLField
	class Blog(models.Model):
		sBlog = HTMLField()	
```

- 

  - 配置站点

  ```
  admin.site.register
  ```

- 在视图中使用：

  - 使用文本域盛放内容

  ```
  <form method='post' action='url'>
  		<textarea></textarea>
  	</form>
  ```

  - 在head中添加script

  ```
  <script src='/static/tiny_mce/tiny_mce.js'></script>
  	<script>
  		tinyMCE.init({
  			'mode':'textareas', 'theme':'advanced',
  			'width':800,'height':600,
  		})
  	</script>
  
  ```





## AXF项目设计

### 技术部：

- 产品经理

  - 留证据

    产出PRD（Product Requirement Document）

    原型图：（七十九和真是网站长得差不多）

- 后端：
  - 后端人基本上最多的
  - 最少2个
    - Python
    - JAVA
    - PHP
    - Node
    - Go
  - 根据需求进行表结构设计
  - 有哪些表？
  - 表中有哪些字段
  - 表有哪些关系

- UI
  - UD：用户界面设计
  - UE：用户体验

- 前端

  - MTV

  - HTML5WEB前端一个
  - Android
  - IOS

- 测试：
  - 黑盒测试
    - 功能测试
    - （Excel，Check_List）
  - 功能测试
    - 不会正向开发，可以写代码猜测是你的代码
    - 高级开发，专门用来查找BUG

- 运维
  - 上线
  - 维护稳定运转
- 版本迭代：产品

### 软件开发的一些知识点

- 主页面显示
  - 最简单的，数据查询，显示
- 商品数据展示
  - 级联查询，排序
- 用户系统：
  - 核心系统

- 购物车系统
  - 商品和用户的关系
  - 订单系统
    - 购物车数据转换成订单
  - 支付系统
    - 接口调用

- 扩展：
  - 地址管理系统
  - 积分系统
  - 会员级别
  - 评价系统
  - 优惠劵系统
  - 数据安全
  - 过滤器
  - 反爬
  - 权限
    - 用户角色
- 部署
  - 动静分离部署



### 前端基础架构

- base模板

  - 导入通用资源
    - reset.css

- 前端适配

  - 推荐百分比不推荐固定尺寸
  - 适配单位
    - px
    - em
      - 默认相对于父级元素
      - 默认1em = 16px
    - rem
      - 相对单位
      - 相对于根据元素
      - 默认大小1rem=16px
  - 弹性盒模型
  - 响应式布局

- 项目中

  - 屏幕宽度的之分之一作为rem的基本单位


### 数据展示

- 建立数据
  - 先见表
  - Model->SQL
- 插入数据
- 数据查询



### 程序调试

- 打印日志
  - print
  - log
    - logging
- debug
  - 断点调试
  - 解决稳定复现BUG的好方案

- 统计工具

- DjangoDebugToolbar
  - Django调试工具条
  - 拥有极强的调试功能，在页面动态注入一个控制面板



## Thefuck

当指令在输入错误的时候，我们可以通过fuck进行弥补。

使用：

- 安装前置依赖python-dev
- python3-pip
- 安装thefuck, pip install thefuck
- 修改别名，在环境变量汇中修改别名



## ajax请求的一些问题

发送ajax请求：

- $.getJSON('第一个参数url'， {第二个参数是字典}，function(data){第三个参数为callback函数 })
- $.ajax({
  		type:"POST",
  		url:"http://127.0.0.1:8000/axf/getmainwheels/",
  		data:{
  			},
  		dataType:"json",
  		success:function(data,status){
  			console.log(data["msg"])
  			console.log(status)
  		}
  	})
- 跨域问题

```

在返回的response中添加
response = JsonResponse(data=data)
response["Access-Control-Allow-Origin"] = "*"
response["Access-Control-Allow-Methods"] = "POST, GET, OPTIONS"
response["Access-Control-Max-Age"] = "1000"
response["Access-Control-Allow-Headers"] = "*"
return response
```





- 在实现界面中个人收藏的字段效果不同时，可以在页面加载时添加一个ajax事件；

根据返回的数据找到。



- 在实现存储密码时，可以封装一个加密的函数进行调用



- 在提交按钮中可以用onsubmit 来控制是否可以进行点击，用函数的返回值来控制。



- 在找元素的时候可以进行拼接， 例如 $("#"+ 变量值) 

- 在选择孩子节点时，$(this).children("span").last()
- 类型转换使用parseInt.
- color  的返回值为rgb模式  'rgb(255, 0, 0)'



- 把查询集用JSON文件返回时，许哟啊进行序列化，可以循环遍历，把值放到列表中

- 接受后需要再进行遍历一次，把值取出





版本升级：策略不兼容

- 第一版本，注册之后密码是明文
- 第二版本，注册之后是hash值
- 第三版本，注册的时候，密码时hash+时间散列
- 假定目前处于第三版本，同时兼容第一版本第二版本
  - 对你请求的参数添加版本号，每天记得就是旧版本
  - 对于版本使用特定认证，认证完，在绘画中将低版本的版本号触怒出下来
    - 小米版本兼容





购物车

购物多对多的关系

- 关系
  - 用户
  - 商品

			订单：

  - 订单和以购买商品是一对多的关系

  - 表关系

    - 订单表
      - 属于哪个用户
    - 订单商品表
      - 购物车里
    - 地址
      - 每个订单对应一个地址
      - 一个地址可以对应多个订单
      - 订单汇集联手或地址表

    - 优惠卷

- 添加购物车
  - 需要用户
    - 未登录，直接跳转登陆
  - 需要商品
    - 传递商品唯一标识
  - 添加的合法性
    - 不存在，创建
    - 存在，添加

购物车全选

- 默认状态
  - 全选按钮是选中
    - 内部所有商品是选中的
  - 全选按钮未选中
    - 内部商品只要存在未选中，全选就应该是未选中
- 点击全选
  - 原状态是选中
    - 全选和所有商品都变成未选中
  - 原状态是未选中
    - 全选和所有商品都变成选中
- 点击单个商品
  - 商品由选中变成未选中
    - 全选一定变成为未选中
  - 











获取属性：

- js获取jquery对象属性：
  - $add.attr（'class'）
  - prop：只能获取内置属性。



多块逻辑拥有相同操作

- 封装一个函数
- 装饰器
- 中间件



浏览器行为

- 重定向
- 跨域



ajax请求， 返回的数据不能直接进行重定向，必须再ajax里对返回数据进行判断，

Windows.open()打开新的网页。



四大器：

生成器

迭代器

装饰器

描述器



- 支付
  - 官方文档
  - 常见支付
    - 支付宝
      - 企业资质
      - 营业执照
    - 微信
      - 要求同支付宝
      - 要认证，一次200，一次收一次。
    - 银联
    - 百度钱包
    - 京东钱包

支付宝支付：

- 支付宝开放平台
  - 蚂蚁金服



- python 第三方支付插件
- pip install python-alipay-sdk   --upgrade

```
def alipay(request):
    # 构建支付的客户端  AlipayClient
    
    alipay_client = AliPay(
        appid=ALIPAY_APPID,
        app_notify_url=None,  # 默认回调url
        app_private_key_string=APP_PRIVATE_KEY,
        alipay_public_key_string=ALIPAY_PUBLIC_KEY,  # 支付宝的公钥，验证支付宝回传消息使用，不是你自己的公钥,
        sign_type="RSA",  # RSA 或者 RSA2
        debug=False  # 默认False
    )
    
    # 使用Alipay进行支付请求的发起

    subject = "i9 20核系列 RTX2080"

    # 电脑网站支付，需要跳转到https://openapi.alipay.com/gateway.do? + order_string
    order_string = alipay_client.api_alipay_trade_page_pay(
        out_trade_no="110",
        total_amount=10000,
        subject=subject,
        return_url="http://www.1000phone.com",
        notify_url="http://www.1000phone.com"  # 可选, 不填则使用默认notify url
    )

    # 客户端操作

    return redirect("https://openapi.alipaydev.com/gateway.do?" + order_string)
```











## 部署

- django中自带开发者服务器
  - runserver
    -  路由处理功能，动态资源处理
    - 如果是debug的话，静态资源粗合理功能
  - 功能健壮，性能是比较低的，仅适用于开发！





- 部署不会使用单一服务器
  - Apache

  - Nginx

    - HTTP服务器
      - 处理静态资源
    - 反向代理

    - 邮件服务器
    - 流媒体服务器



## Nginx

### Nginx安装

1、源码构建安装

2、包管理工具安装

- 添加钥匙
- 向源中添加nginx
- 更新源
- 安装nginx

- 默认nginx会直接启动，

  - 默认配置：/etc/nginx/xxx
  - 内置的一些模块也再次

- 控制nginx

  - 尽量使用nginx指令控制
    - nginx -s signal  quit/stop/reload
    - nginx
    - nginx -c configpath
    - nginx -t -c configpath   只会检测配置语法正确

  - 使用系统也能控制

- 配置文件

  -  nginx核心
  - 格式
    - 格式类似于json
    - 分为指令和块指令
      - 指令就是key value;单value可能是多个
      - 块指令 key {}, value市大括号没有分号、
    - main
    - events:工作模式，工作进程处理的最大连接数
    - http：
      - upstream
      - service，location，路由匹配

- 配置过程

  - 使用nginx处理静态资源
  - 单独使用uwsgi处理动态资源
    - 安装使用uesgi
    - key=value
    - 自u该工程位置和wsgi位置即可
  - 对接Nginx，只需将配置中的Http模式修改为socket模式



### 云服务器部署：

- python环境

- mysql

- redis
  - 源码安装
  - 下载源码
  - make
  - make test
  - utils/install_server.sh
- 安装虚拟环境依赖
  - 导出所有以来pip freeze > requirements.txt
  - 安装所有依赖   pip install -r requirments.txt
- 压力测试
  - ApacheBench
  - ab [opstions]  url  -n



### 项目配置

config.conf

```

user  nginx;
worker_processes  1;


error_log  /var/log/nginx/error.log warn;
pid        /var/run/nginx.pid;


events {
    worker_connections  1024;
}


http {
    include       /etc/nginx/mime.types;
    default_type  application/octet-stream;

    log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
                      '$status $body_bytes_sent "$http_referer" '
                      '"$http_user_agent" "$http_x_forwarded_for"';

    access_log  /var/log/nginx/access.log  main;

    sendfile        on;
    #tcp_nopush     on;

    keepalive_timeout  65;

    #gzip  on;

    server {
	    listen       80;
	    server_name  localhost;

        root   /var/www/AXF;

	    location /static {
		    alias /var/www/AXF/static;
	    }

	    location / {
	        include /etc/nginx/uwsgi_params;
	        uwsgi_pass 127.0.0.1:8888;
	    }
    }

}

```

uwsgi.ini

```
[uwsgi]
# 使用nginx连接时 使用
socket=0.0.0.0:8888

# 直接作为web服务器使用
# http=0.0.0.0:8888
# 配置工程目录
chdir=/var/www/AXF

# 配置项目的wsgi目录。相对于工程目录
wsgi-file=GPAXF/wsgi.py

#配置进程，线程信息
processes=4

threads=10

enable-threads=True

master=True

pidfile=uwsgi.pid

daemonize=uwsgi.log

```



### 反向代理

- 在config.conf下的server中添加location

```
location /	{
    proxy_pass  http://127.0.0.1:9000
}
```

- 对接Gunicorn

```
pip install gunicorn
//开启
gunicorn AXF.uwsgi
//更改端口
gunicorn -b 0.0.0.0:9000 AXF.uwsgi
```



### upstream负载均衡

在server上方添加：

```
upstream  myproject{
	ip_hash;
    server 127.0.0.1:8000;
	server 127.0.0.1:8001 down;
	server 127.0.0.1:8002 weight=3;
	server 127.0.0.1:8003 backup；
	fair；
    }
    
    {
	server vwww.donogh.cn

}
```

下方的代理使用反向代理：

```
location / {
    proxy_pass http://my_server
}
```



### 模拟请求：

- postman

- 安装httpie
  - sudo  apt



### 远程撸代码

使用Pycharm中SFTP

本质上就是FTP



### 统计：

- 实现网站统计，访问统计，来源统计
- 第三方
  - 百度统计
  - 友盟统计
  - 激光统计

- web：
  - 将统计代码放到head中
  - 全站统计放到base中
- APP



## restful

软件架构风格，是一种思想。用来客户端和服务端这种模型中。

实现的就是前后端分离。

- 表现层状态转换
- 表整形状态转移
- 缺少主语，资源（Resource）
- 客户端实现状态转换，通过请求谓词，
  - GET
  - POST
  - PUT
  - DELETE
  - PATCH
- api设计原则
  - 协议http（s）
  - 专属域名或前缀
  - 可以包含版本
  - 在QueryString中包含过滤信息！
  - 路径通常是明此复数传输协议Json
  - 尽量带有超链接。
  - 认证使用Oauth2.0

- 简单实现
  - 针对一个接口的不同请求
  - GET/collection/
  - GET/collections/id/
  - POST/collection/
  - POST/collection/id/
  - PUT
  - PATCH
  - DELETE/collection/id/
- 前端交互
  - web：ajax
- 接口测试工具，模拟请求
  - Pycharm自带的
  - Postman
  - httpie



## 类视图函数

- 继承自View

  - views.BookCBV.as_view(),变成了一个函数

- as_view()

  - 继承自object

- 入口：
  - 不能使用轻轻方法的名字作为参数的名字
  - 只能接受已经存在的属性对应的参数
  - 定义了一个View
    - 创建了一个类视图对象
    - 保留，拷贝传递进来的属性和参数
    - 调用dispatch方法
      - 分发
      - 如果请求方法在我们允许的列表中
        - 从自己这个对象中获取请求方法名字雄安写对应的属性，如果没找到，会给一个默认值：http_method_not_allowed.
        - 如果请求方法不在我们的允许列表中，直接就是http_method_not_allowed
        - 之后将参数传递，调用函数
- 默认实现了options
  - 获取接口信息，可以获取接口都允许什么请求
- 简化版流程
  - as_view
  - dispath
  - 调用实现请求方法对应的函数名。

### 类视图的种类

- view
  - 核心
  - dispatch
- TemplateView
  - 多继承的字类
  - View
    - 分发
    - 函数dispatch()
  - ContextMixin
    - 接受上下文
    - 从试图函数传递到模板的内容
    - get_context_data
  - TemplateResponseMixin
    - 将内容渲染到模板中
    - template_name
    - template_engine
    - response_class
    - content_type
    - 函数render_to_response

- ListView
  - MultipleObjectTemplateResponseMixin
    - TemplateResponseMixin
    - 获取模板名字
      - 首先根据template_name
      - 如果没找到
        - 自己根据应用的名字，关联模型的名字，_list.html上去查找
        - App/book_list.html
  - BaseListView
    - MultipleObjectMixin
      - ContextMixin
      - get_queryset
      - model
    - View
    - 默认实现get，渲染成了response
- DetaView
  - SingleObjectTemplateResopnseMixin
    - TemplateResponseMixin
    - 重写了获取模板名字的方法
  - BaseDetilView
    - view
    - singleObjectMixin





## 重量级REST framework

### 简介

### 序列化器

- seializers.Serializer 原生序列化
  - 需要手动编写每个序列化字段。
  - 手动创建实现对象创建和更新。
- serializers.ModelsSerializer 模型序列化
  - 指定模型和字段
    - fields
    - exclude
- serializers.HyperLinkedModelSerializer 带超链接的模型序列化
  - 指定模型和字段
  - 字段扩充了 url

#### 模型序列化

- 正向序列化：将模型转换成模型
- 反向序列化：将Json转换成模型

```
#继承自serializers.Serializer##需要手动进行序列化

class PersonSerializer(serializers.Serializer):
    id = serializers.IntegerField(read_only=True)
    p_name = serializers.CharField(max_length=32)
    p_age = serializers.IntegerField(default=1)
    p_sex = serializers.BooleanField(default=False)

    def create(self, validated_data):
        return Person.objects.create(**validated_data)

    def update(self, instance, validated_data):

        instance.p_name = validated_data.get('p_name', instance.p_name)
        instance.p_age = validated_data.get('p_age', instance.p_age)
        instance.p_sex = validated_data.get('p_sex', instance.p_sex)
        instance.save()

        return instance
```

```
#继承自serializers.ModelSerializer

class XXX（serializers.ModelSerializer）：
	class Meta:
		model = user
		fields =('username', 'email')
```

```
#继承自serializers.HyperlinkedModelSerializer #####超链接，当带上url参数时可以实现跳转。

class XXX（serializers.HyperlinkedModelSerializer）：
	class Meta:
		model = user
		fields =('url','username', 'email')
```



### router注册路由

- 注册模型
- 模型序列化
- 建立视图函数
  - GameViewSet
  - 继承自viewsets.ModelViewSet
    - serializer_class 
    - queryset

- 注册路由
  - router = DefaultRouter()
  - router.register(r'game', GameViewSet)

- url(r'rest/',include(router.urls)),











### 双R

Resquest：
- rest_framework重新定义的一个类
- 扩充django中的request,将django中的Response作为了自己的一个属性_request
- 属性和方法
  - content_type
  - stream
  - query_params
  - data:
    - :POST,PUT,PATCH请求方法的参数
  - user :登陆的用户
    - 可以直接在请求上获取用户
    - 相当于在请求上添加一个属性，用户对象
  - auth：用户的令牌
    - 认证
    - 相当于请求上添加了一个属性，属性值是token

### 书写规范

- 杜绝中文，空格，特殊字符，关键字，留字在命名和路径中

- 拒绝数字开头，拒绝$开头
- 小写字母开头或大写字母开头，驼峰命名，
- 使用框架，注意远离框架的名字！

### helloREST

- 序列化器
- 视图函数
  - 视图集合
- 路由
  - routers.DefaultRouter
- 记得在installed_apps添加rest_framework
- runserver
  - 所有api变成可视化
  - 超链接
    - HyperLinkeModelSerialiZer
  - 对数据集合实现了
    - 路由 /users/, /groups/
    - get
    - post
  - 对单个实现了
    - 路由   /users/id/ ,/groups/id/
    - get
    - post
    - put
    - delete
    - patch
  - viewsets做了试图函数的实现
  - router做了路由的注册

### Admin

- django内置后台管理
- user和Group
- 自带权限



注意在开发接口时，如果是继承自ListCreateView时，在显示子界面的时候不能给外边的路由使用命名空间，否则post会出错，不能找到name-detail!



### 用户模块

- 用户注册
  - RESTFUL
  - 数据开始
    - 模型，数据库
    - 创建用户
      - 用户身份
        - 管理员
        - 普通用户
        - 删除用户
  - 注册实现
    - 添加了超级管理员生成
- 用户登陆
  - 验证用户名密码
  - 生成用户令牌
  - 出现和注册供用post冲突
    - 添加action
    - path/?action=login
    - path/?action=register
  - 异常捕获尽量精确
- 用户认证
  - BaseAuthentication
    - authenticate
      - 认证成功会返回一个元组
        - 第一个元素是user
        - 第二元素是令牌token , auth
- 用户权限
  - Basepermisson
    - has_permission
      - 是否具有权限
      - True拥有权限
      - false未拥有权限
- 用户认证和权限
  - 直接配置在视图函数上就ok了



### 级联数据

- 用户和收获地址

1、创建模型，UserModel,  AdressModel

2、创建序列化模型，

3、视图函数

4、模型中需要在关联数据中添加related_name='address_list'

5、序列化模型： many=True, read_only=True

### 节流器

控制频率，访问次数

1、setting中设置REST_FRAMEWORK：

```
REST_FRAMEWORK = {
    "DEFAULT_THROTTLE_CLASSES": (
        # 此处是设置的throttle的路径
        "RESTEnd.throttles.ChildThrottle",
    ),
    "DEFAULT_THROTTLE_RATES": {
        
        # 此处的child对应的是scope的值
        'child': "5/m"
    }
}
```

2、定义一个throttle类，继承自Simple Throttle。

3、重写get_cache_key方法

```
class ChildThrottle(SimpleRateThrottle):

    scope = 'child'              #child

    def get_cache_key(self, request, view):
        if isinstance(request.user, ChildModel):
            ident = request.auth
        else:
            ident = self.get_ident(request)

        return self.cache_format % {
            'scope': self.scope,
            'ident': ident
        }
```



## celery

- 分布式任务系统
- 消息队列
  - 异步任务
  - 定时任务

- 需要选择安装消息容器
  - RabbitMQ
  - Redis（数据库，缓存，消息容器）
  - Others brokers： 

- 安装celery
- 开启工作进程并调用任务
- 记录工作状态



安装redis消息模块：pip install -U celery['redis']

安装celery：pip instll celery





pip install django-cerely-results



- log
  - info
  - debug
  - waring
  - error
  - critical



## django-suit



![1540453280052](C:\Users\DELL\AppData\Local\Temp\1540453280052.png)

## Django-事务

```
def hello_transaction(request):
	try:
		with transaction.atomic():
			pass
	except 
```

savepoint():保存点：

```

```



## django-扩容

- 执行原生sql
  - object.raw("sql")
- 想做字段选择：
  - defer
    - 不要哪些字段
  - only
    - 只要哪些字段



## 日志

import   logging：

logging

- 日志有级别

- 四大组成：
  - logger
    - 和代码直接对接的对象
  - handler
    - 处理者
    - 日志处理策略
  - filters
    - 过滤器
  - formatters
    - 格式化
- 日志有级别。



### 日志处理流程

- 通过Logger对象进行输出
- 交给handler处理者进行处理
  - 处理者可以对输出央视进行格式化
  - 也可以对数据进行过滤

