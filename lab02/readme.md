# Apollo配置中心集成

## 一、Apollo本地版本

根据Apollo官方[Quick Start](https://github.com/ctripcorp/apollo/wiki/Quick-Start)安装本地版本。

在Git Bash命令窗口中启动本地Apollo:

```
./demo.sh start

```

## 二、创建项目和导入配置

在浏览器中登录Apollo管理界面

```
地址：localhost:8070

缺省账户：apollo/admin

```

依次创建如下项目，并导入[config](https://github.com/spring2go/piggymetrics/tree/master/config)中对应的配置文件

* registry
* account-service
* statistics-service
* notification-service
* gateway

## 三、项目配置review

依次review上面五个项目中的`application.propreties`文件，确保apollo配置正确。


## 参考

1. [本课程apollo实验](https://github.com/spring2go/apollo_lab)
2. [Apollo官方Java客户端使用指南](https://github.com/ctripcorp/apollo/wiki/Java%E5%AE%A2%E6%88%B7%E7%AB%AF%E4%BD%BF%E7%94%A8%E6%8C%87%E5%8D%97)
3. [Apollo官方使用案例use case](https://github.com/ctripcorp/apollo-use-cases)


