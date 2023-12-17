# OPQOnebot

继承自[kookonebot](https://github.com/super1207/KookOneBot)，为[OPQ](https://73s2swxb4k.apifox.cn/doc-2200981)实现[onebot11](https://github.com/botuniverse/onebot-11)协议！

[红色问答](https://github.com/super1207/redreply)、[MiraiCQ](https://github.com/super1207/MiraiCQ) 与此项目配合更佳，欢迎加入为它们创建的QQ群：920220179、556515826


## 配置文件

config.json 例子： 

```json
{
	"web_port": 8080,
	"web_host": "127.0.0.1",
	"opq_port": 8086,
	"bot_id": 1875159423,
	"access_token": "123456",
	"reverse_uri": [
				"http://127.0.0.1:55001/OlivOSMsgApi/pp/onebot/default",
                        	"ws://127.0.0.1:5555/some"
			],
	"secret":""
}
```

解释：

web_port：正向http和正向websocket需要这个端口号，若不使用正向http和正向websocket，填0即可。

web_host：正向http和正向websocket需要这个，若想要外网访问，填`"0.0.0.0"`，若不使用正向http和正向websocket，填`""`即可。

opq_port：opq的端口号，一般是8086

bot_id：你机器人的QQ号

access_token：正向http、正向websocket、反向websocket需要，若不需要访问密码，填`""`即可。

reverse_uri：反向http和反向websocket需要这个，若不需要反向http或反向ws，填`[]`即可。

secret：反向http需要的HMAC签名，用来验证上报的数据确实来自OneBot，若不需要，填`""`即可。

**注意：所有的字段都是必填的，不可省略！！！**

## 网络协议实现

正向ws

正向http，端口号和正向ws相同，自动识别！

反向ws

反向 http

## API

### 已实现

#### send_group_msg 发送群消息

目前支持文字、图片、at、语音(待测试)

#### send_private_msg 发送私聊消息

目前支持文字、图片、语音(待测试)

#### send__msg 发送消息

同上

#### get_stranger_info 获取陌生人信息

需要有相关事件

#### get_login_info 获取登录号信息

#### delete_msg 撤回消息


## 事件

### 已实现

#### 群消息 

目前接收文字、图片、at、语音(暂时有错)

#### 私聊消息

目前接收文字、图片、语音(暂时有错)

#### 新人入群

#### 生命周期

仅connect（反向http没有此事件）。

#### 心跳

目前固定为5秒一次

