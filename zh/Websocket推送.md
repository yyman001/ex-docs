# Websocket推送
### 概述

WebSocket是HTML5一种新的协议（Protocol）。它实现了客户端与服务器全双工通信， 使得数据可以快速地双向传播。通过一次简单的握手就可以建立客户端和服务器连接， 服务器根据业务规则可以主动推送信息给客户端。其优点如下：

* 客户端和服务器进行数据传输时，请求头信息比较小，大概2个字节。
    
* 客户端和服务器皆可以主动地发送数据给对方。
    
* 不需要多次创建TCP请求和销毁，节约宽带和服务器的资源。

**强烈建议开发者使用WebSocket API获取市场行情和买卖深度等信息。**

*基本信息*
*   币币行情基础站点: [wss://wspool.hiotc.pro/kline-api/ws](wss://wspool.hiotc.pro/kline-api/ws)​
*   合约行情基础站点: [wss://futuresws.xxx.xxx/kline-api/ws](wss://futuresws.goko.vip/kline-api/ws) 其中xxx.xxx替换成交易所的主域
*   返回数据除了心跳数据都会二进制压缩(用户需要通过Gzip算法进行解压)

### Demo
https://github.com/exchange2021/openapidemo/blob/master/src/main/java/com/ws/WsTest.java​

### 参数示例

| event | channel                      | description               |
| ----- | ---------------------------- | ------------------------- |
| req   | market\_$symbol_kline_1month | 请求 1month 历史 k 线记录 |
| sub   | market\_$symbol_depth_step0  | 订阅深度                  |
| sub   | market\_$symbol_kline_1min   | 订阅 1min 实时 k 线信息   |
| sub   | market\_$symbol_ticker       | 订阅 24h 行情数据         |
| sub   | market\_$symbol_trade_ticker | 订阅实时成交              |
| unsub | market\_$symbol_depth_step0  | 取消订阅深度              |
| unsub | market\_$symbol_ticker       | 取消订阅 24h 行情数据     |
| unsub | market\_$symbol_trade_ticker | 取消订阅实时成交          |

```json
{
    "pong": 15359750
}
```

### 订阅全量深度
* 订阅数据样例
```json
{
    "event":"sub",
    "params":{
        "channel":"market_$symbol_depth_step0", // $symbol E.g. 币币:btcusdt 合约:e_btcusdt
        "cb_id":"1" // 业务id 非必填
    }
}
```
* 返回买卖盘最多30条数据
```json
{
    "channel":"market_btcusdt_depth_step0",
    "ts":1506584998239,
    "tick":{
        "asks":[ //卖盘
            [10000.19,0.93],
            [10001.21,0.2],
            [10002.22,0.34]
        ],
        "buys":[ //买盘
            [9999.53,0.93],
            [9998.2,0.2],
            [9997.19,0.21]
        ]
    }
}
```

### 订阅实时成交
* 订阅数据样例
```json
{
    "event":"sub",
    "params":{
        "channel":"market_$symbol_trade_ticker", // $symbol E.g. 币币:btcusdt 合约:e_btcusdt
        "cb_id":"1" // 业务id 非必填
    }
}
```
* 返回
```json
{
    "channel":"market_$symbol_trade_ticker",
    "ts":1506584998239,//请求时间
    "tick":{
        "id":12121,//data中最大交易ID
        "ts":1506584998239,//data中最大时间
        "data":[
            {
                "side":"buy",//买卖方向buy,sell
                "price":32.233,//单价
                "vol":232,//数量
                "amount":323,//总额
                "ds":'2017-09-10 23:12:21'
            }
        ]
    }
}
```

### 订阅k线行情
* 订阅数据样例
```json
{
    "event":"sub",
    "params":{
        "channel":"market_$symbol_kline_[1min/5min/15min/30min/60min/1day/1week/1month]", // $symbol E.g. btcusdt 
        "cb_id":"1" // 业务id 非必填
    }
}
```
* 返回
```json
{
    "channel":"market_$symbol_kline_1min", //1min代表1分钟k线
    "ts":1506584998239,//请求时间
    "tick":{
        "id":1506602880,//时间刻度起始值
        "vol":1212.12211,//交易量
        "open":2233.22,//开盘价
        "close":1221.11,//收盘价
        "high":22322.22,//最高价
        "low":2321.22//最低价
    }
}
```

### 订阅24h行情ticker
* 订阅数据样例
```json
{
    "event":"sub",
    "params":{
        "channel":"market_$symbol_ticker", // $symbol E.g. 币币:btcusdt 合约:e_btcusdt
        "cb_id":"1" // 业务id 非必填
    }
}
```
* 返回
```json
{
    "channel":"market_$symbol_ticker",
    "ts":1506584998239,//请求时间
    "tick":{
        "amount":123.1221,//交易额
        "vol":1212.12211,//交易量
        "open":2233.22,//开盘价
        "close":1221.11,//收盘价
        "high":22322.22,//最高价
        "low":2321.22,//最低价
        "rose":-0.2922,//涨幅
    }
}
```

### 请求k线历史数据
* 请求数据样例
```json
{
    "event":"req",
    "params":{
        "channel":"market_$symbol_kline_[1min/5min/15min/30min/60min/1day/1week/1month]",
        "cb_id":"1",
        "endIdx":"1506602880", //返回endIdx前pageSize条数据  非必填
        "pageSize":100 // 非必填
    }
}
```
* 返回
```json
{
    "event_rep":"rep","channel":"market_$symbol_kline_5min","cb_id":"原路返回",
    "ts":1506584998239,//请求时间
    "data":[ //最多300条
        {
            "id":1506602880,//时间刻度起始值
            "amount":123.1221,//交易额
            "vol":1212.12211,//交易量
            "open":2233.22,//开盘价
            "close":1221.11,//收盘价
            "high":22322.22,//最高价
            "low":2321.22//最低价
        },
        {
            "id":1506602880,//时间刻度起始值
            "amount":123.1221,//交易额
            "vol":1212.12211,//交易量
            "open":2233.22,//开盘价
            "close":1221.11,//收盘价
            "high":22322.22,//最高价
            "low":2321.22//最低价
        }
    ]
}
```
### 请求成交记录
* 请求数据样例
```json
{
    "event":"req",
    "params":{
        "channel":"market_$symbol_trade_ticker", // $symbol E.g. 币币:btcusdt 合约:e_btcusdt
        "cb_id":"1" // 业务id 非必填
    }
}
```
* 返回
```json
{
    "event_rep":"rep","channel":"market_$symbol_trade_ticker",
    "cb_id":"原路返回",
    "ts":1506584998239,"status":"ok",
    "data":[
        {
            "side":"buy",//买卖方向buy,sell
            "price":32.233,//单价
            "vol":232,//数量
            "amount":323//总额
        },
        {
            "side":"buy",//买卖方向buy,sell
            "price":32.233,//单价
            "vol":232,//数量
            "amount":323//总额
        }
    ]
}
```