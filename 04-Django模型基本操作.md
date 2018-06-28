### Django模型基本操作

#### 开发流程

* 配置数据库
* 定义模型类
* 生成迁移文件
* 执行迁移生成数据表
* 使用模型类进行增删改查

#### ORM

* 概述：对象——关系——印射

* 任务：

  根据对象的类型生成表结构；

  将sql语句查询到的结果转换为对象、列表

* 优点：减少工作量，无需因数据库变更而修改代码



#### 定义模型

* 模型、属性、表、字段之间的关系：

  模型——>数据表

  属性——>字段

* 定义属性

  详情见：《定义属性.txt》

* 创建模型类

  ```python
  from django.db import models
  
  class Grades(models.Model):
      gname = models.CharField(max_length=20)
      gdate = models.DateTimeField()
      gboynum = models.IntegerField()
      ggirlnum = models.IntegerField()
      isDelete = models.BooleanField(default=False)
  
      class Meta:
          db_table = 'grades'
  
  class Students(models.Model):
      sname = models.CharField(max_length=20)
      sgender = models.BooleanField(default=True)
      sage = models.IntegerField
      scontend = models.CharField(max_length=20)
      isDelete = models.BooleanField(default=False)
  
      sgrade = models.ForeignKey('Grades')
  
      class Meta:
          db_table = 'students'
          ordering = ['id']
  ```

* 元选项

  db_table——定义数据表名（不写默认为小写项目名_小写类名

  ordering——对象的默认排序字段，获取对象列表时使用（默认为升序）

  ```python
      class Meta:
          db_table = 'students'
          ordering = ['id']
      # 注意：ordering = ['id']为升序，-id为降序
  ```

#### 模型成员

* 类属性：

  1. object——manager类型的一个对象，用于与数据库交互

     ```python
     Students.object.all()
     Students.object.get(pk=1)
     ```

  2. 定义模型类时未指定管理器，默认为object

  3. 自定义管理器：

     ```python
     class Students(models.MOdel):
         stu_obj = models.Manager()  # 自定义管理器
         sname = models.CharField(max_length=20)
         ...
     ```

  4. 自定义管理器Manager类：

     向管理器类中添加额外的方法，修改管理器返回的查询集。

     ```python
     class StudentManager(models.Manager):
         def get_queryset(self):
             return super(StudentManager, self).get_queryset().filter(isDelete=False)
         
         
     class Student(models.Model):
         stu_obj2 = models.Manager()
     ```

* 创建对象

  1. 在模型类中增加一个类方法

     ```python
     class Students(models.Model):
         # 定义类方法创建学生对象
         @classmethod
         def createStudent(cls, name, age, gender, ...):
             stu = cls(sname=name, sage=age, sgender=gender, ...)
             return stu
     ```

  2. 在定义管理器中添加方法

     ```python
     class StudentManager(models.Manager):
         def get_queryset(self):
             return super(StudentManager, self).get_queryset().filter(isDelete=False)
         
         def createStudent(self, name, age, gender, ...):
             stu = self.model()
             stu.sname = name
             stu.asge = age
             stu.sgender = gender
             ...
             return stu
     ```

#### 模型查询

* 概念

* 查询集

  1. 返回集合的过滤器：

     all()

     filter(key=value)

     exclude() —— 过滤掉符合条件的

     values() 

     order_by() —— 排序

  2. 返回单个数据：

     get() —— 返回满足条件的对象（若没找到或找到多个，都会报异常）

     count() —— 返回查询集中的个数

     first()

     last()

     exists() —— 判断是否存在存在数据

  3. 限制查询集：

     返回查询列表，使用下标进行限制，等同于sql中的limit语句

     ```python
     studentlist = Students.object.all()[0:5]
     # 注意：下标不能为负数
     ```

  4. 缓存查询集

* 字段查询：

  概念：类似实现sql中的where语句。

  1. 比较运算符：

     - exact —— 判断

     - contains —— 是否包含

       ```python
       studentlist = Students.object.filter(sname_contains='孙')
       ```

     - startwith、endwith —— 以value开头或结尾

       ```python
       studentlist = Students.object.filter(sname_startwith='孙')
       ```

     - 注意：以上四个大小写敏感，前面加 i 表示不区分大小写。

     - in —— 是否包含在范围内

       ```python
       studentlist = Students.object.filter(pk_in=[1, 2, 3])
       ```

     - gt ——大于

     - gte —— 大于等于

     - lt —— 小于

     - lte —— 小于等于

       ```python
       studentlist = Students.object.filter(sge_gt=30])
       ```

     - 日期

  2. 聚合函数

     - Avg
     - Count
     - Max
     - Min
     - Sum

  3. F、O对象

     ![](G:\Github\Django\images\015.png)

  









