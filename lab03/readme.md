# Gravitee OAuth2集成

## 一、先决条件

完成[gravitee_lab](https://github.com/spring2go/gravitee_lab)的**lab01**和**lab02**，确保mysql数据库中有如下表格和种子数据：

* oauth_clients
* oauth_roles
* oauth_scopes
* oauth_users
* oauth_access_tokens
* oauth_authorization_codes
* oauth_refresh_tokens

## 二、启动Gravitee服务器

在Gravitee源码目录中，修改配置文件，将服务器端口改为5000(8080已经被Apollo使用)

```yml
serverport: 5000

```

在Git Bash命令窗口中启动本地gravitee服务器:

```
./gravitee-server runserver

```

## 三、项目配置review

在Apollo配置界面上，依次review下列项目的配置，确保oauth2服务器相关配置正确。

* account-service
* gateway

## 参考

[本课程gravitee oauth2服务器实验](https://github.com/spring2go/gravitee_lab)




