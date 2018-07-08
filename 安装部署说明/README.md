# [CNJS安装部署说明文档](./安装部署说明.pdf)
## 一、硬件配置及软件环境
### 硬件
基于x86架构的64位CPU，内存4GB以上。
### 操作系统：
Ubuntu 18.04及以上版本
### 软件依赖：
```
NodeJS   10.4及以上版本
Mongodb  3.6 及以上版本
NPM      6.1 及以上版本
Redis    4.0 及以上版本
Nginx    1.14及以上版本（用于域名访问配置及前后端流量转发）
```
确保node和npm命令能正确运行，mongodb数据库已经启动，并默认监听27017端口，reids服务已启动并监听6379端口。

## 二、载入数据库配置
使用mongodb原生的 `mongorestore` 命令将 `database_restore.agz` 中的内容导入数据库。  
即使用命令:
```
mongorestore --gzip --archive= database_restore.agz
```
如果操作成功，那么会在mongodb中新建一个名为`node_club_dev`的数据库。
  
注：此默认数据库配置已生成两个账户便于测试。  
`admin`的登录token为`272a2a86-a3aa-420f-a789-0adae77537e8`  
`test1`的登录token为`ea826f5c-e252-40fd-a7e4-ec443d3a176e`

## 三、运行后端
### 1.拉取后端文件
`git clone https://github.com/cn-js/cnjs` 拉取后端代码并进入`cnjs`文件夹
### 2.安装依赖包
执行 `npm install` 命令，安装必须的依赖包
### 3.运行
执行 `node src/app.js` 启动后端服务。此时会监听`3000`端口，请保证`3000`端口未被占用以及能访问

## 四、运行前端
### 1.拉取前端文件
`git clone https://github.com/cn-js/react-cnjs` 拉取前端代码并进入`react-cnjs`文件夹
### 2.安装依赖包
执行 `npm install` 命令，安装必须的依赖包
### 3.运行
执行 `npm start` 启动前端服务。前端服务会监听`3999`端口，请保证`3999`端口未被占用并能访问
  
此时，访问 `http://YOUR_IP:3999` 便能打开CNJS社区APP了。   
## 为了更好的体验，请使用 **手机访问** 或者开启**电脑浏览器的开发者模式**，模拟手机客户端访问。

## 五、配置Nginx
使用nginx反向代理，分别向前后端服务转发各自的流量。  
本配置默认监听0.0.0.0  80端口  
  
将 `cnjs.conf` 配置文件放到 `/etc/nginx/conf.d` 目录下，并重启nginx服务。  
  
此时访问 `http://your_ip` 就能打开CNJS社区APP了
