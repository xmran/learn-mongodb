# learn-mongodb
# mongodb 安装
  - 官网：https://www.mongodb.com/
  - 手册：https://docs.mongodb.org/manual/
  - **注意** 安装好后看一下装好的文件夹：例：C:\Program Files\MongoDB\Server\3.0\bin  将自己安装好的文件夹路径加入到系统的path环境变量中
## 使用mongodb
  - mongo   使用数据库
  - mongod  开机
  -mongoimport  导入数据
  ### 开机命令
   - 系统根目录打开cmd 执行 mongod --dbpath mongo文件路径  例：mongod --dbpath D:\work\mongo
      - --dbpath就是选择数据库文档所在的文件夹。
   - 再开一个cmd 输入 mongo 此时环境运行起来
  - **注意** 必须同时开这两个cmd，一定要保持，开机这个CMD不能动了，不能关，不能ctrl+c。 一旦这个cmd有问题了，数据库就自动关闭了。
  ### 运行cmd
   - show dbs  列出所有数据库
   - use 数据库名字   使用某个数据库 如果想新建数据库，也是use。use一个不存在的，就是新建。
   - db 查看当前所在数据库
   - cls 清屏
   - db.student.insert({“name”:”xiaoming”}) 插入数据 数据库中不能直接插入数据，只能往集合(collections)中插入数据。不需要创建集合，只需要写点语法
   - db.dropDatabase(); 删除数据库，删除当前所在的数据库
   #### 导入数据
    mongoimport --db test --collection restaurants --drop --file primer-dataset.json  
    -db test  想往哪个数据库里面导入    
    --collection restaurants  想往哪个集合中导入  
    --drop 把集合清空  
    --file primer-dataset.json  哪个文件  
    test：数据库名  restaurants：集合名称   将json文件拖入cmd中
    这样，我们就能用sublime创建一个json文件，然后用mongoimport命令导入，这样学习数据库非常方便。
  #### 查找数据
    - db.restaurants.find() find中没有参数，那么将列出这个集合的所有文档  
    - db.student.find({"score.shuxue":70}) 精确匹配  
    - db.student.find({"score.shuxue":70 , "age":12}) 多个条件  
    - db.student.find({"score.yuwen":{$gt:50}}) 大于条件  
    - db.student.find({$or:[{"age":9},{"age":11}]})  或者。寻找所有年龄是9岁，或者11岁的学生  
    - db.restaurants.find().sort( { "borough": 1, "address.zipcode": 1 } )   查找完毕之后，打点调用sort，表示升降排序
 ### 修改数据
    - db.student.update({"name":"小明"},{$set:{"age":16}});   查找名字叫做小明的，把年龄更改为16岁  
    - db.student.update({"score.shuxue":70},{$set:{"age":33}});   查找数学成绩是70，把年龄更改为33岁  
    - db.student.update({"sex":"男"},{$set:{"age":33}},{multi: true})   更改所有匹配项目  
    - db.student.update({"name":"小明"},{"name":"大明","age":16})  完整替换，不出现$set关键字了
 ### 删除数据
    - db.restaurants.remove( { "borough": "Manhattan" } )  
    - db.restaurants.remove( { "borough": "Queens" }, { justOne: true } )
 ### 数据分页
    - limit（）  读取的条数  
    - skip（）  略过的条数  
    - db.student.find({}).limit(10).skip(page*10)    limit()和skip()配合使用实现数据分页
 ### 获取数据总数
    db.student.stats().count;
