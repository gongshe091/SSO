# SSO 单点登陆

同域下的多个应用只需要（将cookie设置到顶级域名下+共享session如内存spring session或redis，或数据库）即可实现登陆哦

## 模块介绍
-	center 注册中心
	维护了支持统一登陆的app列表
-	app1/app2 后台不同的业务门户
-	base 公用代码库

## 业务流程

	https://yq.aliyun.com/articles/636281
	
	登陆流程：
	1.请求应用app1的资源，发现没有登陆，转到sso认证中心；
	2.认证中心发现没有登陆，返回到登陆页面；如果已登录则转到3.1
	3.认证中心确认登陆了以后，生成一个session，
		3.1 并返回到请求的应用的认证页面带上一个ticket。
	4.应用拿到ticket，请求sso认证中心，判断ticket是否有效，如果有效，则认为登陆成功，生成一个session并返回一个cookie
	

## 使用方法

	
## 版本

### 第一版（current）

	当前该做的，就是做一个简单的单点登陆，先跑通流程，再优化代码
	
### 后面考虑

-	0.1 集成spring session，做一个分布式session
-	0.2	再做一个分布式id生成器
-	0.3	再利用redis特性，做几个小例子，巩固知识点（工程量可能比较大）
-	0.4	集成shiro/oauth2
		oauth2暂时可不用集成，核心思想跟sso差不多，shiro可以考虑集成

到这里会封一个release出来

-	1.1	登陆了就应该有一些菜单权限，待完善
-	1.2	每个应用的超时时间可不同


-	2.1 做完0.3的情况下，会出现很多小应用，考虑集成dubbo服务治理


## 欢迎大家多提出修改意见哦

## 备注：
1. fork了本项目，如何更新至最新代码:https://blog.csdn.net/qq_39083004/article/details/81053953

```
1.	git remote add upstream https://github.com/jadeStoneStonger/SSO
2. 	用git remote -v可以看到一个origin是自己的，另外一个upstream原作者。
3. 	更新代码：
git fetch upstream //去拉去原作者的仓库更新
git checkout master //切换到自己的master
git merge upstream/master //merge或者rebase到你的master
结束！
```
