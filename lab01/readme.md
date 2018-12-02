# 开发环境搭建

## 一、安装MongoDB和Robomongo

从MongoDB官网下载[MongoDB Community Serfver 4.0.4](https://www.mongodb.com/download-center/community)，本地安装为Windows服务。

下载MongoDB开源管理工具[Robomongo(GUI for MongoDB)](https://download.robomongo.org/1.2.1/windows/robo3t-1.2.1-windows-x86_64-3e50a65.exe)，本地安装即可。

## 二、创建数据库和用户

安装完成后MongoDB默认只能本机访问，并且不需要密码，下面我们创建数据库并添加用户，

通过Robo 3T创建连接(不需要认证)并连接到MongoDB，在数据库连接图标上鼠标右击选`Open Shell`，打开操作窗口，

在操作窗口中创建管理员账户`admin:admin`

```
use admin

show dbs
```

```
db.createUser({user: "admin", pwd: "admin", 
  roles:[{role: "userAdminAnyDatabase", db: "admin"}], 
  mechanisms:[  
  "SCRAM-SHA-1"
 ]})

show users
```

在操作窗口中创建数据库`piggymetrics_account_db`和普通账户`user2:test`

```
use piggymetrics_account_db

db.user2.insert({"test":"12345678"})

show dbs
```

```
db.createUser({user: "user2", pwd: "test", 
  roles:[{role: "readWrite", db: "piggymetrics_account_db"}], 
  mechanisms:[  
  "SCRAM-SHA-1"
 ]})

show users
```

使用上述方法依次创建如下数据库和普通账户：

* 数据库`piggymetrics_notification_db`和账户`user3:test`
* 数据库`piggymetrics_statistics_db`和账户`user4:test`

在Windows服务中停止MongoDB Server,

在MongoDB Server安装目录`/MongoDB/Server/4.0/bin`找到`mongo.cfg`，添加启用安全配置：

```yml

security:
  authorization: enabled

```

在Windows服务中重新启动MongoDB Server,

校验，

通过Robo 3T创建一个连接，连接到admin管理员数据库，设置相应的用户名密码认证，校验连接正常，且管理员可以看到其它所有数据库。

通过Robo 3T创建三个连接，分别连接到piggymetrics_account_db，piggymetrics_notification_db和piggymetrics_statistics_db三个数据库，设置相应的用户名密码认证，校验连接正常。


## 三、导入种子账户数据

通过Robo 3T连接到数据库piggymetrics_account_db，在数据库连接图标上鼠标右击选`Open Shell`，打开操作窗口，导入[seed](https://github.com/spring2go/piggymetrics/tree/master/mongodb)中的种子账户数据:

```
use piggymetrics_account_db;
```

```javascript

print('dump start');

db.accounts.update(
    { "_id": "demo" },
    {
    "_id": "demo",
    "lastSeen": new Date(),
    "note": "demo note",
    "expenses": [
        {
            "amount": 1300,
            "currency": "USD",
            "icon": "home",
            "period": "MONTH",
            "title": "Rent"
        },
        {
            "amount": 120,
            "currency": "USD",
            "icon": "utilities",
            "period": "MONTH",
            "title": "Utilities"
        },
        {
            "amount": 20,
            "currency": "USD",
            "icon": "meal",
            "period": "DAY",
            "title": "Meal"
        },
        {
            "amount": 240,
            "currency": "USD",
            "icon": "gas",
            "period": "MONTH",
            "title": "Gas"
        },
        {
            "amount": 3500,
            "currency": "EUR",
            "icon": "island",
            "period": "YEAR",
            "title": "Vacation"
        },
        {
            "amount": 30,
            "currency": "EUR",
            "icon": "phone",
            "period": "MONTH",
            "title": "Phone"
        },
        {
            "amount": 700,
            "currency": "USD",
            "icon": "sport",
            "period": "YEAR",
            "title": "Gym"
        }
    ],
    "incomes": [
        {
            "amount": 42000,
            "currency": "USD",
            "icon": "wallet",
            "period": "YEAR",
            "title": "Salary"
        },
        {
            "amount": 500,
            "currency": "USD",
            "icon": "edu",
            "period": "MONTH",
            "title": "Scholarship"
        }
    ],
    "saving": {
            "amount": 5900,
            "capitalization": false,
            "currency": "USD",
            "deposit": true,
            "interest": 3.32
        }
    },
    { upsert: true }
);

print('dump complete');


```

## 四、导入项目源码

在Eclipse IDE里头导入[piggymetrics改造版源码](https://github.com/spring2go/piggymetrics)

