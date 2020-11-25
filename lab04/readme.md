# CAT调用链监控集成

## 一、CAT3.0本地部署

参考点评官方[CAT服务器部署指南](https://github.com/dianping/cat/wiki/readme_server)，使用源码构建部署包，并部署到本地Tomcat。

配置文件示例：

{CAT安装盘}/data/appdatas/cat/client.xml

```xml
<?xml version="1.0" encoding="utf-8"?>
<config mode="client">
	    	<servers>
	                <server ip="192.168.90.80" port="2280" http-port="8081"/>
	                <!--server ip="10.1.1.2" port="2280" http-port="8080"/>
	                <server ip="10.1.1.3" port="2280" http-port="8080"/-->
	    	</servers>
</config>

```

{CAT安装盘}/data/appdatas/cat/datasources.xml

```xml

<?xml version="1.0" encoding="utf-8"?>

<data-sources>
	<data-source id="cat">
		<maximum-pool-size>3</maximum-pool-size>
		<connection-timeout>1s</connection-timeout>
		<idle-timeout>10m</idle-timeout>
		<statement-cache-size>1000</statement-cache-size>
		<properties>
			<driver>com.mysql.jdbc.Driver</driver>
			<url><![CDATA[jdbc:mysql://127.0.0.1:3306/cat]]></url>  <!-- 请替换为真实数据库URL及Port  -->
			<user>root</user>  <!-- 请替换为真实数据库用户名  -->
			<password>root</password>  <!-- 请替换为真实数据库密码  -->
			<connectionProperties><![CDATA[useUnicode=true&characterEncoding=UTF-8&autoReconnect=true&socketTimeout=120000]]></connectionProperties>
		</properties>
	</data-source>
</data-sources>

```

**注意**

1. 修改Tomcat端口为8081(8080已经被Apollo使用)
2. mysql不要使用5.7以上版本，否则可能有兼容性问题

部署完毕启动Tomcat，通过浏览器访问校验CAT正常启动

```
http://localhost:8081/cat
```

如果CAT启动有问题可以通过如下日志定位问题：

1. CAT启动日志，在CAT安装盘`\data\applogs\cat`目录中
2. Tomcat日志，在{Tomcat部署目录}`\logs`

## 二、项目配置

在如下五个项目中配置相应的CAT项目名

* account-service
* notification-service
* statistics-service
* gateway
* registry

```
src/main/resources/META-INF/app.properties
```



