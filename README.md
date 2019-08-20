# jcc_rpc_yi
[jcc_rpc](https://github.com/JCCDex/jcc_rpc) 的易语言实现

文档请参见 testDoc目录下的 JCC测试返回.xls 文件介绍

本项目由井通基金会资助

项目讨论的QQ群：568285439 （SWTC&MOAC开发者社区）

Telegram: https://t.me/moacblockchain

提案发起（Submit proposal）： https://github.com/JCCDex/ProjectFundingProposal/issues

本项目关联提案 ： [
PFP08 JCC_RPC_易语言开发实现](https://github.com/JCCDex/ProjectFundingProposal/issues/9)


#查询当前委托

参数|类型|备注
---|:--:|---:
exHost|文本型|exHost
address|文本型|钱包地址
page|文本型|页码，该字段暂时无效,可以随便传，但是必须要有

返回信息
```
' {"code":"0","data":[{"type":"buy","pair":"SWT/CNY+jGa9J9TkqtBcUoHe2zqhVFFbgUVED6o9or","price":"0.001000","amount":"1.000000","sequence":4464,"passive":false},{"type":"buy","pair":"SWT/CNY+jGa9J9TkqtBcUoHe2zqhVFFbgUVED6o9or","price":"0.004000","amount":"300000.000000","sequence":4557,"passive":false}],"msg":"获得挂单列表成功","isActive":true}
```

#查询历史交易记录

参数|类型|是否为空|备注
---|:--:|:--:|---:
exHost|文本型| | exHost
address|文本型| | 钱包地址
ledger|文本型|可空| 区块账本编号，从第二页开始需要，该值由上一页查询返回
seq|文本型| 可空| 交易序列号，从第二页开始需要，该值由上一页查询返回
返回信息
```
' {"code":"0","data":{"marker":{"ledger":11588678,"seq":4},"transactions":[{"hash":"89DF2578BFCC39BE7815DE9FEE0737834947C9A99410D401098AD8526EF58878/8AE6E7D1C916AA9BB4983ABCC2CE98CE9FD57E8E7E66FDCD1C0FEFF19B8A3A81/undefined","time":1545899990,"type":"sell","pairs":"MOAC/CNT","amount":"26.7","sum":"81.7019999999999","price":"3.05999999999999625468","status":"offer_bought","counterparty":{"account":"jnpCL7vYAnAhjdQR7iVS4yeJ6t2tbw3KNp","seq":72,"hash":"8AE6E7D1C916AA9BB4983ABCC2CE98CE9FD57E8E7E66FDCD1C0FEFF19B8A3A81"}},{"hash":"1DA1BAD815E0D029EA665B271C6E3B884CD0E91F1658CA8E542342D30FDDC337","time":1545734060,"type":"buy","pairs":"MOAC/CNT","amount":"818","sum":"2454","price":"3","status":"offer_created"}]},"msg":"获取历史交易成功","isActive":true}
```

###查询历史转账记录

参数|类型|是否为空|备注
---|:--:|:--:|---:
exHost|文本型| | exHost
address| 文本型| | 钱包地址
ledger|文本型|可空| 区块账本编号，从第二页开始需要，该值由上一页查询返回
seq|文本型|可空| 交易序列号，从第二页开始需要，该值由上一页查询返回
```
 {"code":"0","data":{"marker":{"ledger":11490452,"seq":6},"transactions":[{"hash":"957F315F85E0C4EA7029B1A8B6EAF1568480867DFFACD3E362641D5E37B1C0E5","time":1544788830,"sender":"jG9ntUTuBKqDURPUqbGYZRuRDVzPY6bpxL","receiver":"jHXA8QvnogEw3exos7V2t3UXZmDWhDgHQT","currency":"MOAC","amount":"1","result":false}]},"msg":"获取历史交易成功","isActive":true}
```

参数|备注
---|---:
ledger|下次请求的账本编号
seq |下次请求的交易序列号
hash |交易hash
time |交易时间(秒)
sender |发送方
receiver|接收方
amount|交易数量
result|该字段无效,不用处理

###撤单

参数|类型|是否为空|备注
---|:--:|:--:|---:
exHost|文本型||'服务器地址
sign|文本型||'签名后的数据
返回文本| 文本型||
url|文本型||
json|类_json||
```
' {"code":"0","data":{"hash":"E601D772D15F2AFC563E8CE2324F0BB684590EA1FB409011111EDDD9EFA36C20"},"msg":"取消挂单提交成功","isActive":true}
```





###获取服务器列表

参数|类型|是否为空|备注
---|:--:|:--:|---:
URL|文本型|| 服务器列表，便于以后服务器地址更改，不写死
exHosts：交易服务器列表，默认端口为80
infoHosts：信息服务器列表，默认端口为80
接口路由中以/exchange开头的请调用exHosts列表中服务器
接口路由中以/info开头的请调用infoHosts列表中服务器
为了减轻单个服务器负载，请用轮询机制分别访问列表中每台服务器



###获取钱包余额

参数|类型|是否为空|备注
---|:--:|:--:|---:
exHost|文本型| | 服务器地址
address| 文本型| | 钱包地址
|url|文本型| ||

```
{"code":"0","data":[{"value":"105140.995617","currency":"SWT","issuer":"","freezed":"105080","reserve":"20","title":"SWT"},],"msg":"获得余额成功"}
```

参数|备注
---|---:
code|"0"表示成功返回
value|钱包总余额，包含冻结余额
currency|币种Token
freezed|冻结金额
title|币种名称
```
url ＝ exHost ＋ “/exchange/balances/” ＋ address
```



###查询历史交易记录

参数|类型|是否为空|备注
---|:--:|:--:|---:
exHost|文本型| | exHost
address|文本型| |钱包地址
ledger|文本型|可空| 区块账本编号，从第二页开始需要，该值由上一页查询返回
seq|文本型|可空|交易序列号，从第二页开始需要，该值由上一页查询返回
url| 文本型| | 'exHost地址


```
{"code":"0","data":{"marker":{"ledger":11588678,"seq":4},"transactions":
[{"hash":"D166357BF8E0FBAB5B450379A0DB19BA55A773075E0F52B06B7CD6A8406E8219","time":1546070620,"type":"sell","pairs":"MOAC/CNT","amount"
:"818","sum":"3272","price":"4","status":"offer_cancelled"},
{"hash":"89DF2578BFCC39BE7815DE9FEE0737834947C9A99410D401098AD8526EF58878/8AE6E7D1C916AA9BB4983ABCC2CE98CE9FD57E8E7E66FDCD1C0FEFF19B8A3
A81/undefined","time":1545899990,"type":"sell","pairs":"MOAC/CNT","amount":"26.7","sum":"81.7019999999999","price":"3.05999999999999625468","status":"offer_bought","counterparty":
{"account":"jMbmoPA3QcWKoDQrhGdiykVkqJPe4cqYnY","seq":200,"hash":"40406805D40503AB867313511DE2D0D4125B4B3A2D582F0E72750C835597A122"}}]}
,"msg":"获取历史交易成功","isActive":true}
```

参数|备注
---|---:
ledger   |                  下次请求的账本编号
seq       |                 下次请求的交易序列号
hash       |                交易hash,   如果是用"/"分割，那么左边表示主动成交方，右边表示被动成交方
time       |                交易时间(秒)
type      |                 买、卖类型 sell-卖 buy-买
pairs     |                 交易对
amount     |                交易数量
sum       |                 交易总价格
price     |                 单价
status    |                 交易状态 offer_bought-主动成交 offer_funded-被动成交offer_partially_funded-部分成交 offer_cancelled-取消挂单 offer_created-创建挂单





###查询历史转账记录

参数|类型|是否为空|备注
---|:--:|:--:|---:
exHost|文本型| | exHost
address| 文本型| | 钱包地址
ledger|文本型| 可空| 区块账本编号，从第二页开始需要，该值由上一页查询返回
seq|文本型|可空| 交易序列号，从第二页开始需要，该值由上一页查询返回


```
{"code":"0","data":{"marker":{"ledger":11490452,"seq":6},"transactions":
[{"hash":"E0B3FA8A0438F15C8C8D068B383D19E3F5E1F633BAF756F4509435DF8178A35F","time":1546842750,"sender":"jHXA8QvnogEw3exos7V2t3UXZmDWhDgHQT","receiver":"jLUkoiBvewNDvrJMR7q96s67WgoGjmttPr","currency":"MOAC","amount":"194","result":false}]},"msg":"获取历史交易成功","isActive":true}
```

参数|备注
---|---:
ledger  |                   下次请求的账本编号
seq     |                   下次请求的交易序列号
hash     |                  交易hash
time     |                  交易时间(秒)
sender   |                  发送方
receiver |                  接收方
amount   |                  交易数量
result   |                  该字段无效,不用处理




###查询当前委托

参数|类型|是否为空|备注
---|:--:|:--:|---:
exHost|文本型| | exHost
address|文本型| | 钱包地址
page|文本型| | 页码，该字段暂时无效,可以随便传，但是必须要有
```
{"code":"0","data":[{"type":"buy","pair":"SWT/CNY+jGa9J9TkqtBcUoHe2zqhVFFbgUVED6o9or","price":"0.004000","amount":"300000.000000","sequence":4557,"passive":false}],"msg":"获得挂单列表
成功","isActive":true}
```

参数|备注
---|---:
type            |              类型 buy-买 sell-卖
pair            |              交易对
price           |              价格
amount          |              交易数量
sequence        |              交易序列号，用于取消挂单使用
passive         |              该字段无效，不用处理
```
url ＝ exHost ＋ “/exchange/orders/” ＋ address ＋ “/” ＋ page
```


###获取交易序列号

参数|类型|备注
---|:--:|---:
exHost|文本型|exHost
address|文本型| 钱包地址
sequence|文本型 |交易序列号
url|文本型||
返回文本|文本型||
json|类_json||

```
{"code":"0","data":{"sequence":4568},"msg":"获得序列号成功","isActive":true}
```



###子程序 挂单(前端签名---返回hash)

参数|类型|备注
---|:--:|---:
exHost| 文本型|exHost
sign| 文本型| 签名后的加密内容--挂单
url|文本型||
json| 类_json||

```
{"code":"0","data":{"hash":"39EC76DAAC1A2BC0662240145C3086110A7AB8864B2B1F4CF3C38616D78DFEA4"},"msg":"挂单提交成功","isActive":true}
```
```
url ＝ exHost ＋ “/exchange/sign_order”
```


###撤单

参数|类型|备注
---|:--:|---:
exHost|文本型|服务器地址
sign|文本型|签名后的数据
url|文本型||
json|类_json||

```
{"code":"0","data":{"hash":"E601D772D15F2AFC563E8CE2324F0BB684590EA1FB409011111EDDD9EFA36C20"},"msg":"取消挂单提交成功","isActive":true}
```
```
url ＝ exHost ＋ “/exchange/sign_cancel_order”
```


###撤单_非签名

参数|类型|备注
---|:--:|---:
参_SQ|文本型| 交易序号
参_ADDRESS|文本型| API
参_SECRET|文本型|私钥
winhttp|WinHttpR||
url|文本型||
data|文本型||
返回文本|文本型||
js|JScript||





###转账

参数|类型|是否为空|备注
---|:--:|:--:|---:
exHost|文本型||服务器列表
sign|文本型||签名
url|文本型|||
json|类_json|||

```
{"code":"0","data":{"hash":"22240FEC865A2325401BCFAEE80387033F3190B7EF506D11981D96F4F38F13E2"},"msg":"提交支付成功","isActive":true}
url ＝ exHost ＋ “/exchange/sign_payment”
```


###挂单_非签名

参数|类型|备注
---|:--:|---:
参__类型|整数型| 1买入,2卖出
参_数量| 文本型|  数量
参_价格| 文本型| 价格
参_secret_key| 文本型| 下单私钥
参_address| 文本型|  下单地址
url| 文本型||
data| 文本型||
GL_SQ| 文本型||
```
url ＝ “https://api.jingtum.com/v2/accounts/” ＋ 参_address ＋ “/orders”
```






###转账_非签名

参数|类型|是否为空|备注
---|:--:|:--:|---:
exHost|文本型||服务器地址
secret|文本型||转出钱包的私钥
to|文本型||接收方钱包的地址
amount|文本型||数量
currency|文本型||token名称
issuer|文本型||发行方
memo|文本型| 可空| 转账备注信息，最长512字节
data|文本型|||
url|文本型|||
json|类_json|||
```
{"code":"0","data":{"hash":"22240FEC865A2325401BCFAEE80387033F3190B7EF506D11981D96F4F38F13E2"},"msg":"提交支付成功","isActive":true}
```
```
url ＝ exHost ＋ “/exchange/payment”
```

###获取市场深度

参数|类型|是否为空|备注
---|:--:|:--:|---:
infoHost|文本型||服务器地址
currency|文本型||币种交易对 如:SWT-CNY
type|文本型||类型 normal-只获取最新10条记录 more-获取最新50条记录
url|文本型|||
返回文本|文本型|||


```
 {"code":"0","data":{"base":"SWT","counter":"CNY.jGa9J9TkqtBcUoHe2zqhVFFbgUVED6o9or","asks":
[{"price":0.00445,"amount":74328,"total":74328,"type":"sell"},{"price":0.00446,"amount":769281,"total":843609,"type":"sell"},
{"price":0.00447,"amount":1899950,"total":2743559,"type":"sell"},{"price":0.00448,"amount":1298921,"total":4042480,"type":"sell"},
{"price":0.00449,"amount":1912880,"total":5955360,"type":"sell"}],"bids":
[{"price":0.00442,"amount":261609,"total":261609,"type":"buy"},
{"price":0.00441,"amount":3089357.765534,"total":3350966.765534,"type":"buy"},
{"price":0.0044,"amount":1024005,"total":4374971.7655340005,"type":"buy"},
{"price":0.00439,"amount":1877847,"total":6252818.7655340005,"type":"buy"},
{"price":0.00438,"amount":1742312,"total":7995130.7655340005,"type":"buy"}]},"msg":"获取市场信息成功","success":true}
```

参数|备注
---|---:
price       |      价格
amount      |      数量
total       |      该字段暂时无效 可以忽略
type        |      类型 sell-卖 buy-买
```
url ＝ infoHost ＋ “/info/depth/” ＋ currency ＋ “/” ＋ type
```



###获取K线数据

参数|类型|备注
---|:--:|---:
infoHost|文本型||
currency| 文本型| 币种交易对 如:SWT-CNY
type|文本型| hour-小时 day-日 week-周 month-月
url|文本型||


```
{"code":"0","data":
[[1526313600000,0.03569,0.04150600000000021,0.03511625798095238,0.044564446944444454,14944051.348589845,371894445.0376669,2897],
[1526400000000,0.041600000000000005,0.0409,0.04029380231944445,0.04399294244,10679759.133056931,256273850.651661,37749]],"msg":"获取市场信息成功","success":true}
```


参数|备注
---|---:
json.data[1]           |         成交时间(毫秒)
json.data[2]           |         开盘价格
json.data[3]           |         收盘价格
json.data[4]           |         最低价格
json.data[5]           |         最高价格
json.data[6]           |         交易金额
json.data[7]           |         交易量
json.data[8]           |         成交笔数
```
url ＝ infoHost ＋ “/info/kline/” ＋ currency ＋ “/” ＋ type
```


###获取最新成交

参数|类型|是否为空|备注
---|:--:|:--:|---:
infoHost|文本型|| 服务器地址
currency|文本型|| 币种交易对 如:SWT-CNY
type|文本型||类型 normal-只获取最新10条记录 more-获取最新50条记录
url|文本型|||

返回参数: 服务器返回最近的240条数据
```
' {"code":"0","data":[[62.60056,14036,0.00446,1547025420000,0,1],[49.9966,11210,0.00446,1547025350000,0,1],
[99.99766,22421,0.0044599999999999996,1547025320000,0,1],[30.192000000000917,6800,0.004440000000000135,1547025300000,1,1],
[15.442979999999807,3486,0.004429999999999944,1547024770000,1,1],[99.99766000000002,22421,0.004460000000000001,1547024040000,0,1],
[786.768,177600,0.00443,1547023510000,1,3],[118.01970000000024,26640,0.004430168918918928,1547023330000,1,3],
[0.04460000000000264,10,0.004460000000000264,1547023320000,0,1],[99.99766,22421,0.0044599999999999996,1547023300000,0,1]],"msg":"获取市场信息成功","success":true}
```

参数|备注
---|---:
array[0]         |        交易金额
array[1]         |        交易量
array[2]         |       价格
array[3]         |        成交时间(毫秒)
array[4]         |        成交类型 0-买 1-卖
array[5]         |        撮合标记 1-非撮合 3-3方撮合 4-4方撮合 5-5方撮合 6-6方撮合
```
url ＝ infoHost ＋ “/info/history/” ＋ currency ＋ “/” ＋ type
```

###获取24小时行情数据

参数|类型|备注
---|:--:|---:
infoHost|文本型| 服务器地址
url|文本型||

```
url ＝ infoHost ＋ “/info/alltickers”
```

###获取交易详情

参数|类型|是否为空|备注
---|:--:|:--:|---:
exHost|文本型||服务器
hash|文本型|| hash值
url|文本型|||
```
url ＝ exHost ＋ “/exchange/detail/” ＋ hash
```

###网页访问_DELETE

参数|类型|备注
---|:--:|---:

网址|文本型|完整的网页地址,必须包含http://或者https://
访问方式|整数型|0=GET 1=POST 2=HEAD
提交信息|文本型|"POST"专用
提交Cookies|文本型|本参数传递变量时会自动回传返回的Cookie
返回Cookies|文本型|返回的Cookie
附加协议头|文本型|一行一个请用换行符隔开
返回协议头|文本型|返回的协议头
返回状态代码|整数型|网页返回的状态代码，例如：200；302；404等
禁止重定向|逻辑型|默认不禁止网页重定向
字节集提交|字节集|提交字节集数据
代理地址|文本型|代理地址，格式为 8.8.8.8:88
超时|整数型|秒，默认为15秒,-1为无限等待
代理用户名|文本型|用户名
代理密码|文本型|密码
代理标识|整数型|代理标识，默认为1，0为路由器
对象继承|对象|此处可自行提供对象，不再主动创建
是否自动合并更新Cookie|逻辑型|默认为真，自动合并更新
局_访问方式|文本型||
局_WinHttp|对象||
局_发送协议头|文本型|"0"|
局_返回协议头|文本型|"0"|
局_计次|整数型||
局_网页数据|字节集||
局_变体提交|变体型||

###线程_初始化COM库 ()
```
局_访问方式 ＝ “DELETE”
局_WinHttp.方法 (“Open”, 局_访问方式, 网址, 假)
局_WinHttp.写属性 (“Option”, 4, 13056)
附加协议头 ＝ “Accept: */*”
```
###局_WinHttp.方法 (“Send”, 提交信息)

```
局_网页数据 ＝ 局_WinHttp.读属性 (“ResponseBody”, ).取字节集 ()
返回协议头 ＝ 局_WinHttp.读文本属性 (“GetallResponseHeaders”, )
返回协议头 ＝ 子文本替换 (返回协议头, “Set-Cookie”, “Set-Cookie”, , , 假)
返回状态代码 ＝ 局_WinHttp.读数值属性 (“Status”, )
局_返回协议头 ＝ 分割文本 (返回协议头, #换行符, )
返回Cookies ＝ “”
```
```
返回状态代码 ＝ 局_WinHttp.读数值属性 (“Status”|)
局_返回协议头 ＝ 分割文本 (返回协议头|#换行符|)
返回Cookies ＝ “”
```

