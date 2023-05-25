# 编译执行
```
git clone https://github.com/yinghaoyu/chat_room.git
cd chat_room
git submodule update --init --recursive
make
make -j
sh move.sh

bin/chat_room -s
```

# 设计思路
## httpserver

支持文件访问，流量访问，index.html

实现一个文件的Servlet

1.handle 实现文件相关的操作。
2.ResourceSerlvet 实现文件访问

## Websocket Server
1. 普通的http实现，周期性轮训。
2. websocket 长连接， 服务器可以主动推送数据，效率高

## 协议设计
协议格式： {type:"协议类型", data: {}}
```
1. login协议。 
    Client: {type: "login_request", "name": "昵称"}
    Server: {type: "login_response", result: 200, msg: "ok"}
    
2. send协议。
    Client：{type: "send_request", "msg" : "消息"}
    Server: {type: "send_response", result: 200, msg: "ok"}
    
3. user_enter 通知
    {type: "user_enter", msg: "xxx 加入聊天室", time:xxx}
    
4. user_leave 通知
    {type: "user_leave", msg: "xxx 离开聊天室", time:xxx}
    
5. msg 通知
    {type: "msg", msg: "具体聊天信息", user: "xxx", time: xxxx}
```
