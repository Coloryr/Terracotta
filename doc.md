# Http接口文档

## 获取版本信息
```
GET /meta
```
返回
```json
{
    "compile_timestamp": "1762147569492",
    "easytier_version": "v2.4.5",
    "target_arch": "x86_64",
    "target_env": "msvc",
    "target_os": "windows",
    "target_tuple": "x86_64-pc-windows-msvc",
    "target_vendor": "pc",
    "version": "snapshot",
    "yggdrasil_port": 13448
}
```

## 关闭陶瓦联机
```
GET /panic?<peaceful>
```

- peaceful: bool 是否强制退出

无返回内容

## 获取日志
```
GET /log?<fetch>
```

- fetch: bool 是否为抓取

不知道这个返回啥

## 转到扫描模式
当你点击当**房主**时  
```
GET /state/scanning?<player>
```

- player: string 玩家名

无返回内容

## 取消状态
点击**返回时**  
```
GET /state/ide
```

无返回内容

## 进入房间
```
GET /state/guesting?<room>&<player>
```

- room: string 邀请码
- player: string 玩家名字

无返回内容，用状态码返回是否进入房间  
- 200: 成功进入
- 400: 无法进入

## 获取当前状态
```
GET /state
```

返回多种状态，其中`index`为请求返回次数，会自增  
空闲状态
```json
{
    "index": 0,
    "state": "waiting"
}
```
扫描状态
```json
{
    "index": 0,
    "state": "host-scanning"
}
```
开始创建房间时
```json
{
    "index": 0,
    "state": "host-starting",
    "room": "room"
}
```
创建完成
```json
{
    "index": 0,
    "state": "host-ok",
    "room": "room",
    "profile_index": 0,
    "profiles": []
}
```
链接房间
```json
{
    "index": 0,
    "state": "guest-connecting",
    "room": "room"
}
```
开始链接房间
```json
{
    "index": 0,
    "state": "guest-starting",
    "room": "room"
}
```
链接房间成功
```json
{
    "index": 0,
    "state": "guest-ok",
    "url": "url",
    "profile_index": 0,
    "profiles": []
}
```

profiles的数据结构为
- machine_id: string 机器码
- name: string 名字
- vendor: string 版本
- kind: ProfileKind 账户类型

ProfileKind有`HOST`, `LOCAL`, `GUEST`