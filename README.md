# OPQOnebot

### 注意，[OPQ](https://73s2swxb4k.apifox.cn/doc-2200981)为闭源非官方的QQ协议框架，部分用户数据会经过安全性和稳定性均未知的私人服务器，请不要使用关键账号登录，并且注意网络安全。

### opqonebot不会收集任何用户的隐私数据，也不对因此项目带来的任何损失负责，若您已经明白风险，请继续往下阅读，否则不要使用。

继承自[kookonebot](https://github.com/super1207/KookOneBot)，为[OPQ](https://73s2swxb4k.apifox.cn/doc-2200981)实现[onebot11](https://github.com/botuniverse/onebot-11)协议！

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

目前支持文字、图片、at、回复、语音（支持wav、mp3、部分flac、silk、ogg）、表情(有略微缺陷)、拍一拍、json(未测试)、xml(未测试)、文件(需要特殊设置，见下面的文件发送)、TTS([CQ:tts,text=你好])

#### send_private_msg 发送私聊消息

目前支持文字、图片、回复、语音（支持wav、mp3、部分flac、silk、ogg）、表情(有略微缺陷)、TTS([CQ:tts,text=你好])

#### send__msg 发送消息

同上

#### get_stranger_info 获取陌生人信息

需要有相关事件

#### get_login_info 获取登录号信息

#### delete_msg 撤回消息

#### get_group_member_list 获取群成员列表

#### get_group_member_info 获取群成员信息

#### set_group_ban 禁言

#### set_group_leave 退群 

#### set_group_kick 群组踢人

#### get_cookies 获取一些可能有用的数据

请自行观察这个api返回了什么东西(clientkey,pskey,gtk,cookies)

#### set_group_add_request 处理加群请求／邀请

#### set_friend_add_request 处理加好友请求

#### set_group_special_title 设置群组专属头衔（未测试）

#### set_group_card 设置群名片

#### get_group_list 获取群列表

#### get_group_info 获取群信息

#### send_like 点赞

需要有相关事件

#### get_friend_list 获取好友列表（未严格测试）

#### 发送群聊自定义合并转发（仅支持文字和图片）

[https://docs.go-cqhttp.org/api/#发送合并转发-群聊](https://docs.go-cqhttp.org/api/#%E5%8F%91%E9%80%81%E5%90%88%E5%B9%B6%E8%BD%AC%E5%8F%91-%E7%BE%A4%E8%81%8A)

不支持设置name和uin

注意不要一次性发送大量节点，会不安全。


## 事件

### 已实现

#### 群消息 

目前接收文字、图片、at、语音(暂时有错)、表情(有略微缺陷)

#### 私聊消息

目前接收文字、图片、语音(暂时有错)、表情(有略微缺陷)

#### 新人入群

#### 机器人被邀请入群

#### 有人申请入群

#### 加好友申请

#### 退群

类型均为leave，操作者就是退群者

#### 生命周期

仅connect（反向http没有此事件）。

#### 心跳

目前固定为5秒一次


## 群组文件发送

通过CQ码即可发文件，如：

[CQ:file,file=file:///D:\myfile\aaa.txt,name=aaa.txt]

[CQ:file,file=http://xxxxx/aaa.txt,name=aaa.txt]

[CQ:file,file=base64://xxxxx,name=aaa.txt]

如果`opq_onebot.exe`和`OPQBot.exe`在同一个目录下，则不需要任何设置即可发文件。

否则，需要在`opq_onebot.exe`的`config.json`中设置`opq_file_path`,如
```
{
	...
	...
	"opq_file_path": "D:\\OPQBot\\OPQBot.exe"
}
```
