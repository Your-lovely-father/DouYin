# 低仿抖音短视频
[抖音](https://www.douyin.com/)
该项目基本使用JavaScript（ES6/7）开发，混入了Python写的爬虫来爬取[梨视频](https://www.pearvideo.com/)的短视频来丰满自己的数据库。

__注：本项目仅供学习交流使用，切勿用于商业用途，如有侵犯第三方版权问题及时联系我__

## 前端技术栈
 - Axios
 - Vue2
 - Vuex
 - Vue Router
 - Vue CLI 3
 - Vue-socket.io
 - Stylus
## 后端技术栈
 - koa2
 - sequelize
 - ioredis
 - socket.io

## 项目运行
__注意：由于涉及大量的 ES6/7 等新属性，node 需要 6.0 以上版本__

``` 

npm install

启动redis数据库和mysql数据库

redis数据库配置文件为./server/redis.js 这个没有启动感觉是这个问题
mysql数据库配置文件为./server/config.js

node ./server/init-db.js (初始化数据库生成表结构) -- 空表
或者将./server/utils/backup.sql还原到你自己的数据库下

node ./server/app.js （启动服务器）

npm run serve （前端项目）


```
前后端都在一个项目里（感觉不是很合理），所以必须先启动后端相关的服务器。

## 目标功能
 - [x] 登录、注册
 - [x] 密码找回
 - [x] 修改个人资料
 - [x] 个人信息浏览（已发布、点赞的视频）
 - [x] 上传头像
 - [x] 发送邮件验证
 - [x] 视频浏览
 - [x] 关注与粉丝
 - [x] 视频点赞、评论点赞
 - [x] 视频评论、回复评论
 - [x] 评论@用户
 - [x] 关注动态浏览
 - [x] 好友（互相关注）间私信
 - [x] 发布动态
 - [x] 搜索视频，用户（根据视频描述，根据昵称或id）
 - [x] 私信、被关注、被评论、被@、被点赞、关注人发布动态的消息提醒
 - [ ] 删除评论
 - [ ] 删除视频
 - [ ] 分享
 - [ ] [后台管理](https://github.com/Your-lovely-father/DouYin-Admin)
 
## 总结

会话管理是用的koa-session2插件，通过session和cookie结合来管理会话。用户登录成功之后可以用户信息存入session中。koa-session2会将sessionId写入cookie，再把session对象写入redis，键值为sessionId，这样只要cookie没有过期，客户端的每次请求就会携带这个sessionId，在服务端就可以从redis中获取登录信息，当然也可以用作会话拦截。注销的时候只需要将ctx.session置为空对象，这样cookie就会被清掉了。

## 目录结构
```
.
├── public
├── server                                             (服务器在这里)
│   ├── controllers                                    (各个类别的controller)
│   ├── models                                         (sequelize模型)
│   ├── static
│   │   ├── assets
│   │   │   ├── avatar                                 (静态资源头像)
│   │   │   ├── css
│   │   │   ├── fonts
│   │   │   ├── img
│   │   │   ├── js
│   │   │   ├── videoCover                             (静态资源视频封面)
│   │   │   └── videoPath                              (静态资源视频)
│   └── utils                                          (服务器util)
├── src                                                (前端项目在这里)
│   ├── base                                           (基础组件)
│   ├── common
│   │   ├── fonts                                      (iconfont)
│   │   ├── js                                         (util/config)
│   │   └── stylus
│   ├── components                                     (逻辑组件)
│   ├── store                                          (vuex)
│   └── views                                          (页面)

```

## License
[MIT](./LICENSE)
