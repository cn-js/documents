# CNJS软件设计文档
## 架构设计
### 架构描述

整个APP的架构，分为前后端。前端的架构为MVVM架构，为模型层，视图层，视图模型层，为目前前端开发中最受欢迎的架构。<br>
后端采用RESTful设计风格，应用程序状态和功能可以分为各种资源。资源是一个有趣的概念实体，它向客户端公开。资源的例子有：应用程序对象、数据库记录、算法     等等。每个资源都使用 URI (Universal Resource Identifier) 得到一个唯一的地址。所有资源都共享统一的接口，以便在客户端和服务器之间传输状态。使用的      是标准的 HTTP 方法，比如 GET、PUT、POST 和 DELETE。Hypermedia 是应用程序状态的引擎，资源表示通过超链接互联。<br>
REST 约束条件作为一个整体应用时，将生成一个简单、可扩展、有效、安全、可靠的架构。由于它简便、轻量级以及通过 HTTP 直接传输数据的特性，用于 web 服务和动态 Web 应用程序的多层架构可以实现可重用性、简单性、可扩展性和组件可响应性的清晰分离。

#### 视图层
个人设置改成用户主页。
1. 首页
2. 发布页
3. 消息 
4. 用户主页

#### 视图模型层
这个是前端框架的一个实现。通过绑定试图模型层和视图层。当模型层的数据发生变化时，会让视图模型层也发生变化，同时视图层也会变化。

#### 视图模型层
这里是前端的数据存储的地方。来源是通过HTTP请求和后端交互，获取数据。

#### 数据层
后端主要是作为一个数据来源。通过接受到HTTP请求，然后根据不同的请求去操作数据库，并返回数据。

### 架构图
![图2-1](https://github.com/cn-js/documents/blob/scarlettee-patch-2/%E8%BD%AF%E4%BB%B6%E8%AE%BE%E8%AE%A1%E6%96%87%E6%A1%A3/images/%E5%9B%BE2-1%EF%BC%9A%E6%9E%B6%E6%9E%84%E5%9B%BE.png) 

### 关键抽象
#### 用户模块
User（抽象类）， RegisterUser（已注册用户），AnonymousUser（游客）<br>
![图2-2](https://github.com/cn-js/documents/blob/scarlettee-patch-2/%E8%BD%AF%E4%BB%B6%E8%AE%BE%E8%AE%A1%E6%96%87%E6%A1%A3/images/%E5%9B%BE2-2%EF%BC%9A%E7%94%A8%E6%88%B7%E6%A8%A1%E5%9D%97%E7%B1%BB%E5%9B%BE.jpg)

#### 主题模块
Topic(抽象类)，All(所有)，Best(精华)，Share(分享)，Ask(问答)，Job(招聘)<br>
![图2-3](https://github.com/cn-js/documents/blob/scarlettee-patch-2/%E8%BD%AF%E4%BB%B6%E8%AE%BE%E8%AE%A1%E6%96%87%E6%A1%A3/images/%E5%9B%BE2-3%EF%BC%9A%E4%B8%BB%E9%A2%98%E6%A8%A1%E5%9D%97%E7%B1%BB%E5%9B%BE.png)

#### 评论模块
Comments(抽象类），包含author_id<br>
![图2-4](https://github.com/cn-js/documents/blob/scarlettee-patch-2/%E8%BD%AF%E4%BB%B6%E8%AE%BE%E8%AE%A1%E6%96%87%E6%A1%A3/images/%E5%9B%BE2-4%EF%BC%9A%E8%AF%84%E8%AE%BA%E6%A8%A1%E5%9D%97%E7%B1%BB%E5%9B%BE.png)

#### 消息模块
Messages(抽象类），类型: reply（回复话题），reply2（话题中回复），follow（关注用户），at（ ＠某用户）<br>
![图2-5](https://github.com/cn-js/documents/blob/scarlettee-patch-2/%E8%BD%AF%E4%BB%B6%E8%AE%BE%E8%AE%A1%E6%96%87%E6%A1%A3/images/%E5%9B%BE2-5%EF%BC%9A%E6%B6%88%E6%81%AF%E6%A8%A1%E5%9D%97%E7%B1%BB%E5%9B%BE.png)

## 用例分析
### 补充用例归约
经检查，本项目组发现用例归约比较完善，暂时无需补充。

### 用例中类的析取
#### 游客注册用例类的析取
游客首次使用该app时，只拥有帖子的浏览权限；在注册时，输入access-token后，注册成功，系统分配一个用户ID标识用户，加入用户数据库，获得用户权限。<br>
边界类：signin。signin.html为游客注册填写access-token的页面。<br>
控制类：export。export控制类负责处理注册时的相关操作，包括输入access-token；加入用户数据库，记录用户相关信息；完成注册反馈。<br>
实体类：user. user实体类表示注册时的信息，包括注册码（access-token），注册后的用户ID。<br>
![图3-1-1](https://github.com/cn-js/documents/blob/scarlettee-patch-2/%E8%BD%AF%E4%BB%B6%E8%AE%BE%E8%AE%A1%E6%96%87%E6%A1%A3/images/%E5%9B%BE3-1-1%EF%BC%9A%E6%B8%B8%E5%AE%A2%E6%B3%A8%E5%86%8C%E7%94%A8%E4%BE%8B%E7%B1%BB%E7%9A%84%E6%9E%90%E5%8F%96%E5%9B%BE.png)<br>
![图3-1-2](https://github.com/cn-js/documents/blob/scarlettee-patch-2/%E8%BD%AF%E4%BB%B6%E8%AE%BE%E8%AE%A1%E6%96%87%E6%A1%A3/images/%E5%9B%BE3-1-2%EF%BC%9A%E6%B8%B8%E5%AE%A2%E6%B3%A8%E5%86%8C%E7%94%A8%E4%BE%8B%E7%B1%BB%E7%9A%84%E6%97%B6%E5%BA%8F%E5%9B%BE.png)<br>
用户在主页面点击我,系统调用边界类signin函数，再调用控制类中showup()显示登陆界面，signup()函数让用户登录，调用user实体类。成功后结果返回给控制类。<br>

下图是边界类signin的文件其中的登录，输入用户名部分。
![图3-1-3](https://github.com/cn-js/documents/blob/scarlettee-patch-2/%E8%BD%AF%E4%BB%B6%E8%AE%BE%E8%AE%A1%E6%96%87%E6%A1%A3/images/%E5%9B%BE3-1-3.png)<br>

下图是控制类export文件中的登录操作：
![图3-1-4](https://github.com/cn-js/documents/blob/scarlettee-patch-2/%E8%BD%AF%E4%BB%B6%E8%AE%BE%E8%AE%A1%E6%96%87%E6%A1%A3/images/%E5%9B%BE3-1-4.png)<br>

下图是实体类user实体类注册时的信息，包括注册码（access-token），注册后的用户ID。
![图3-1-5](https://github.com/cn-js/documents/blob/scarlettee-patch-2/%E8%BD%AF%E4%BB%B6%E8%AE%BE%E8%AE%A1%E6%96%87%E6%A1%A3/images/%E5%9B%BE3-1-5.png)<br>
















