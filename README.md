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
