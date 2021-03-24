#### django学习

静态文件配置时路径的static是静态文件别名，不是static文件夹，所以导入什么都是用/static/开头



"./登录界面_files/(.*?.css)"

"/static/css/$1"



form表单

1. form标签的属性action 指定提交的地址（不写默认当前地址），method请求方式（默认get）

2. input要有name属性， 有的标签还需要有value

3. 有一个button按钮或者type=‘submit’的input



目前要提交post请求的必要操作：

在setting.py中注释一个中间件

```python
MIDDLEWARE = [
    'django.middleware.security.SecurityMiddleware',
    'django.contrib.sessions.middleware.SessionMiddleware',
    'django.middleware.common.CommonMiddleware',
    #'django.middleware.csrf.CsrfViewMiddleware',
    'django.contrib.auth.middleware.AuthenticationMiddleware',
    'django.contrib.messages.middleware.MessageMiddleware',
    'django.middleware.clickjacking.XFrameOptionsMiddleware',
]
```



```
1.ctrl+c  复制

​     2.ctrl+d  快速复制上行的内容至下一行

​     3.Ctrl+shift+n   通过文件名快速查找工程内的文件

​     4.ctrl +a    全选

      5.Ctrl+alt+l  调整代码格式

​     6.Alt+enter  导入模块

​     7.Ctrl+z  回退

​     \8. ctrl+x  剪贴
 
 \9. ctrl+/   注释，去注释

​     10.shift +Tab  往移动

​    11.shift +enter  自动回车，跳入下一行

​     12.ctrl +enter  自动回车，跳入上一行
```



request:

request.method :请求方式 GET或POST

request.POST：form表单提交post请求的数据

request.GET：url上窗体参数（查询参数）?user=sds&pwd=dsd 账号密码都泄露了 安全性不高



创建app：

python manage.py startapp app01

app中的东西

admin.py: admin的物理后台

apps.py: app

models.py: orm 与数据库有关，我感觉相当于数据库啦里面存了表

views.py 函数



执行数据库迁移

```
python manage.py makemigrations #检测所有app下的models.py文件有什么变化，将变更记录制作成迁移文件
python manage.py migrate #根据迁移文件做数据库迁移，将变更记录同步到数据库中
```



类---》表

对象--》元组

属性---》字段（属性值）



```python
import pymysql

pymysql.install_as_MySQLdb()
```

习惯写与项目名同名文件夹__init__.py里面

返回页面用render 

返回字符串用HttpResenpose

> **render()**
>
> 此方法的作用---结合一个给定的模板和一个给定的上下文字典，并返回一个渲染后的 HttpResponse 对象。
>
> 通俗的讲就是把context的内容, 加载进templates中定义的文件, 并通过浏览器渲染呈现.
>
> **help文档中render描述**
>
> **render(request, template_name, context=None, content_type=None, status=None, using=None)
> **
>
> **参数：**
>
> **request: 是一个固定参数**
>
> **template_name: templates中定义的文件，注意路径名。比如："templates/polls/index.html", 则参数这样写："\**polls/index.html\**"**
>
> **context: 要传入文件中用于渲染呈现的数据, 默认是字典格式**
>
> content_type: 生成的文档要使用的MIME 类型。默认为DEFAULT_CONTENT_TYPE 设置的值。
>
> status: http的响应代码,默认是200.
>
> using: 用于加载模板使用的模板引擎的名称。



```python
return render(request,'publisher_list.html',{'all_publishers': all_publishers})
```

]

```html
<body>
{#{{all_publishers}}#}
<table border="1">
    <thead>
    <tr>
        <th>序号</th>
        <th>id</th>
        <th>出版社名称</th>
    </tr>
    </thead>
    <tbody>
    {% for i in all_publishers %}
       <tr>
        <td>{{ forloop.counter }}</td>
        <td>{{ i.id }}</td>
        <td>{{ i.name }}</td>
        </tr>
    {% endfor %}

    </tbody>
</table>

</body>
```



form表单

post请求是提交的

get请求是获取页面的 输入地址回车就是get请求







```python
for book in all_books:
    print(book)
    print(book.name)
    print(book.publisher)#书籍所关联的出版社对象
    print(book.publisher_id)#书籍所关联的出版社对象id
```



html

option标签是下拉选择框