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






