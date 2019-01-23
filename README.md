# bijibeifen001

1、manjaro系统下面的git可能会出现git下来的项目做了更改之后，不能git push到服务器，可能和git的设置有关，需要ssh方式。
	避免踩坑解决办法，在git项目的时候，不要直接拷贝http路经，而是需要像下面这样克隆项目，把用户名称和密码带上，这样就能绕坑了。
	
	git clone http://liujiaheng:123456@10.80.65.35:8080/gitblit/r/code/SAAS/ngcms.git
			 用户名称   用户密码
			 
同步系统时间
sudo ntpdate 0.cn.pool.ntp.org

2、docker
	启动docker服务:
	sudo systemctl start docker 
	查看docker服务的状态:
	sudo systemctl status docker
	设置docker开机启动服务:
	systemctl enable docker 
 	启动一个mysql应用实例
 	sudo docker run --name mysqldb -e MYSQL_ROOT_PASSWORD=123456 -p 6666:3306 -d mysql
 	sudo docker run --name mysqldb-useThe -e MYSQL_ROOT_PASSWORD=123456 -p 6630:3306 -d mysql
 	简单启动redis服务
 	sudo docker run --name redis4 -p 6379:6379 -d redis
	启动mongo
	sudo docker run --name mongo1 -p 27011:27017 -d mongo
		创建admin用户n搜权
		a.1  docker exec -it mongo bash
		a.2  mongo
		a.3  use admin
		a.4  db.createUser({ 
				user: 'mongo-admin', 
				pwd: 'mongo-password', 
				roles: [ { role: "root", db: "admin" } ] });
		a.5  db.auth("mongo-admin","mongo-password")

		role后面的参数参考,可根据时间情况选择：
			Read：允许用户读取指定数据库
			readWrite：允许用户读写指定数据库
			dbAdmin：允许用户在指定数据库中执行管理函数，如索引创建、删除，查看统计或访问system.profile
			userAdmin：允许用户向system.users集合写入，可以找指定数据库里创建、删除和管理用户
			clusterAdmin：只在admin数据库中可用，赋予用户所有分片和复制集相关函数的管理权限。
			readAnyDatabase：只在admin数据库中可用，赋予用户所有数据库的读权限
			readWriteAnyDatabase：只在admin数据库中可用，赋予用户所有数据库的读写权限
			userAdminAnyDatabase：只在admin数据库中可用，赋予用户所有数据库的userAdmin权限
			dbAdminAnyDatabase：只在admin数据库中可用，赋予用户所有数据库的dbAdmin权限。
			root：只在admin数据库中可用。超级账号，超级权限
		a.6 创建普通用户
			use somedb
			db.createUser({ user: 'someusername', pwd:'somepwd', roles: [ {role:"readWrite",db:"somedb"}]});
			db.auth("someusername","somepwd")

		步骤a.1到a.6会得到两个授权用户mongo-admin,someusername,密码分别为mongo-password,somepwd

		mongo登录命令：mongo 数据库名称 -u 用户名 -p 用户密码
			例如：
			mongo admin -u mongo-admin -p mongo-password
			mongo somedb -u someusername -p somepwd

	启动mongo-express 
	docker run -itd -p 8030:8081 --link mongo1:mongo mongo-express

3、JAVA	启动jar包
	java -jar -Dserver.port=3333 target/*.jar 指定到端口启动服务
	
4、Jetbeans license 
K03CHKJCFT-eyJsaWNlbnNlSWQiOiJLMDNDSEtKQ0ZUIiwibGljZW5zZWVOYW1lIjoibnNzIDEwMDEiLCJhc3NpZ25lZU5hbWUiOiIiLCJhc3NpZ25lZUVtYWlsIjoiIiwibGljZW5zZVJlc3RyaWN0aW9uIjoiRm9yIGVkdWNhdGlvbmFsIHVzZSBvbmx5IiwiY2hlY2tDb25jdXJyZW50VXNlIjpmYWxzZSwicHJvZHVjdHMiOlt7ImNvZGUiOiJJSSIsInBhaWRVcFRvIjoiMjAxOS0wNC0yNSJ9LHsiY29kZSI6IlJTMCIsInBhaWRVcFRvIjoiMjAxOS0wNC0yNSJ9LHsiY29kZSI6IldTIiwicGFpZFVwVG8iOiIyMDE5LTA0LTI1In0seyJjb2RlIjoiUkQiLCJwYWlkVXBUbyI6IjIwMTktMDQtMjUifSx7ImNvZGUiOiJSQyIsInBhaWRVcFRvIjoiMjAxOS0wNC0yNSJ9LHsiY29kZSI6IkRDIiwicGFpZFVwVG8iOiIyMDE5LTA0LTI1In0seyJjb2RlIjoiREIiLCJwYWlkVXBUbyI6IjIwMTktMDQtMjUifSx7ImNvZGUiOiJSTSIsInBhaWRVcFRvIjoiMjAxOS0wNC0yNSJ9LHsiY29kZSI6IkRNIiwicGFpZFVwVG8iOiIyMDE5LTA0LTI1In0seyJjb2RlIjoiQUMiLCJwYWlkVXBUbyI6IjIwMTktMDQtMjUifSx7ImNvZGUiOiJEUE4iLCJwYWlkVXBUbyI6IjIwMTktMDQtMjUifSx7ImNvZGUiOiJHTyIsInBhaWRVcFRvIjoiMjAxOS0wNC0yNSJ9LHsiY29kZSI6IlBTIiwicGFpZFVwVG8iOiIyMDE5LTA0LTI1In0seyJjb2RlIjoiQ0wiLCJwYWlkVXBUbyI6IjIwMTktMDQtMjUifSx7ImNvZGUiOiJQQyIsInBhaWRVcFRvIjoiMjAxOS0wNC0yNSJ9LHsiY29kZSI6IlJTVSIsInBhaWRVcFRvIjoiMjAxOS0wNC0yNSJ9XSwiaGFzaCI6Ijg4MjUwMTQvMCIsImdyYWNlUGVyaW9kRGF5cyI6MCwiYXV0b1Byb2xvbmdhdGVkIjpmYWxzZSwiaXNBdXRvUHJvbG9uZ2F0ZWQiOmZhbHNlfQ==-IJBDUuZMqhMJZfuM8Pgz1WXDRP3k9sKMJXuGdnbwoYDN4Y2G5Xmpw05GZUeESnh2/wzVxTHF4+PQ5ewk+J66F15b50VHSNxFI9XKWatoDfBc9EA1CddWqAU5CaipdMkSHoUDbT69PPGU4Vsfo1HTFv50tQ7RFVYMDbmVhw6mUbTFMvGiu5CZTuEVkmJ+1KpfuyQZvXjS1hXhfbK/xmpMG2/xRmK9lxW9PafZU1dWxqjYU8QBlUYgjdDsDS2apSTE+xFF6y3ZKK/YThpC7IYt5HR5Cc3VGjdb/H7jEAkH2/Uz0PrixPc3Bk5tU01rhxI4Z5VbmmWzGAhWWBtQEqU17A==-MIIEPjCCAiagAwIBAgIBBTANBgkqhkiG9w0BAQsFADAYMRYwFAYDVQQDDA1KZXRQcm9maWxlIENBMB4XDTE1MTEwMjA4MjE0OFoXDTE4MTEwMTA4MjE0OFowETEPMA0GA1UEAwwGcHJvZDN5MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAxcQkq+zdxlR2mmRYBPzGbUNdMN6OaXiXzxIWtMEkrJMO/5oUfQJbLLuMSMK0QHFmaI37WShyxZcfRCidwXjot4zmNBKnlyHodDij/78TmVqFl8nOeD5+07B8VEaIu7c3E1N+e1doC6wht4I4+IEmtsPAdoaj5WCQVQbrI8KeT8M9VcBIWX7fD0fhexfg3ZRt0xqwMcXGNp3DdJHiO0rCdU+Itv7EmtnSVq9jBG1usMSFvMowR25mju2JcPFp1+I4ZI+FqgR8gyG8oiNDyNEoAbsR3lOpI7grUYSvkB/xVy/VoklPCK2h0f0GJxFjnye8NT1PAywoyl7RmiAVRE/EKwIDAQABo4GZMIGWMAkGA1UdEwQCMAAwHQYDVR0OBBYEFGEpG9oZGcfLMGNBkY7SgHiMGgTcMEgGA1UdIwRBMD+AFKOetkhnQhI2Qb1t4Lm0oFKLl/GzoRykGjAYMRYwFAYDVQQDDA1KZXRQcm9maWxlIENBggkA0myxg7KDeeEwEwYDVR0lBAwwCgYIKwYBBQUHAwEwCwYDVR0PBAQDAgWgMA0GCSqGSIb3DQEBCwUAA4ICAQC9WZuYgQedSuOc5TOUSrRigMw4/+wuC5EtZBfvdl4HT/8vzMW/oUlIP4YCvA0XKyBaCJ2iX+ZCDKoPfiYXiaSiH+HxAPV6J79vvouxKrWg2XV6ShFtPLP+0gPdGq3x9R3+kJbmAm8w+FOdlWqAfJrLvpzMGNeDU14YGXiZ9bVzmIQbwrBA+c/F4tlK/DV07dsNExihqFoibnqDiVNTGombaU2dDup2gwKdL81ua8EIcGNExHe82kjF4zwfadHk3bQVvbfdAwxcDy4xBjs3L4raPLU3yenSzr/OEur1+jfOxnQSmEcMXKXgrAQ9U55gwjcOFKrgOxEdek/Sk1VfOjvS+nuM4eyEruFMfaZHzoQiuw4IqgGc45ohFH0UUyjYcuFxxDSU9lMCv8qdHKm+wnPRb0l9l5vXsCBDuhAGYD6ss+Ga+aDY6f/qXZuUCEUOH3QUNbbCUlviSz6+GiRnt1kA9N2Qachl+2yBfaqUqr8h7Z2gsx5LcIf5kYNsqJ0GavXTVyWh7PYiKX4bs354ZQLUwwa/cG++2+wNWP+HtBhVxMRNTdVhSm38AknZlD+PTAsWGu9GyLmhti2EnVwGybSD2Dxmhxk3IPCkhKAK+pl0eWYGZWG3tJ9mZ7SowcXLWDFAk0lRJnKGFMTggrWjV8GYpw5bq23VmIqqDLgkNzuoog==

5、jenkins不要使用官方镜像，使用jenkins/jenkins:latest镜像
	docker run --name myjenkins -p 9090:8080 -p 50000:50000 -v ~/jenkins_home:/var/jenkins_home jenkins/jenkins:latest
	docker run -d --name myjenkins-demo --net staticnet --ip 172.18.0.3 -p 9090:8080 -p 50000:50000 -v ~/jenkins_home/:/var/jenkins_home jenkins-img

6、oracle账户名：2429803999@qq.com 密码：Liu@19920520

7、启动ubuntu实例
   
   //docker run -it --name ubuntu-ssh-demo --net staticnet --ip 172.18.0.2 -p 53:53 -p 8080:8080 -p 80:80 -p 9090:9090 -p 8000:8000 ubuntu-ssh
   docker run -it --name ubuntu-ssh-demo --net staticnet --ip 172.18.0.2 -p 53:53 -p 8082:8080 -p 82:80 -p 9092:9091 -p 8002:8000 ubuntu-shh
	













