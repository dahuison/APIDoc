# 基本信息 Base information

原生WSS接口 Base url: wss://wbs.mexc.com/raw/ws



## 公共接口 public:



### K线 kline



##### 获取全量的k线 the k-line full data

**Channel**:

request **get.kline**

response **rs.kline**

**Request Payload:**

```
{

  "req":"get.kline", // request key

  "symbol":"VDS_USDT",//	symbol 交易对

  "interval":"Min30",	// kline interval	K线间隔时间	目前只支持 support: Min1、Min5、Min15、Min30、Min60、Day1、Month1

  "start":1561107500000,// start timeK线起始时间

  "end":1561453160000	// end time	K线结束时间

}
```

**Response Payload:**

```
{

  "channel":"rs.kline"// response key

  "symbol":"VDS_USDT",// 交易对 symbol

  "data":{

    "q":[		// 这根K线期间成交额 dealTotal

      25710.17

    ],

    "s":"ok",	//状态 state

    "c":[		// 这根K线期间末一笔成交价 the closing price

      1561449600

    ],

    "v":[		// 这根K线期间成交量 volume 

      295324.832092

    ],

    "h":[		// 这根K线期间最高成交价 the highest price

      4.0439

    ],

    "l":[		// 这根K线期间最低成交价 the lowest price

      3.8564

    ],

    "o":[		// 这根K线期间第一笔成交价 the opening price

      3.8817

    ]

  }

}
```



##### 获取增量的k线 get kline keep updating.

**Channel**:

request **sub.kline**

push **push.kline**

**Request Payload:**

```
{

  "op":"sub.kline",    //sub key

  "symbol":"VDS_USDT",

  "interval":"Min30"

}
```

**Response Payload:**

```
{

  "channel":"push.kline", //push key

  "symbol":"VDS_USDT",  // 交易对 symbol

  "data":{

    "q":[		 // 这根K线期间成交额 dealTotal

      25710.17,

      33157.01

    ],

    "s":"ok", // state

    "c":[		  // 这根K线期间末一笔成交价 the closing price

      1561449600,

      1561451400

    ],

    "v":[			// 这根K线期间成交量 the volume

      295324.832092,

      1414326.509656

    ],

    "h":[			// 这根K线期间最高成交价 the highest price

      4.0439,

      4.39

    ],

    "l":[			// 这根K线期间最低成交价 the lowest price

      3.8564,

      3.8568

    ],

    "o":[			// 这根K线期间第一笔成交价 the opening price

      3.8817,

      4.0195

    ]

  }

}
```



### 订阅交易信息 subscribe symbol infomation

订阅交易信息 subscribe symbol infomation

**Channel**:

request **sub.symbol**

push **push.symbol**

**Request Payload:**

```
{

  "op":"sub.symbol", // sub key

  "symbol":"VDS_USDT"	//	交易对

}
```

**Response Payload**

```
{

  "channel":"push.symbol",  // push key

  "data":{					//数据 data

    "deals":				//成交信息 deal info

	    [

	      {

	        "t":1561465233455,//成交时间 deal time

	        "p":"4.2003",	//交易价格 deal price

	        "q":"86.68",	//成交数量 deal quantity

	        "T":1			//成交类型:1买、2卖  deal type: 1 buy , 2 sell

	      }

	    ],

    "bids": 			//买单 bids list

	    [

	      {

	        "p":"4.2000",	//买单价格 price

	        "q":"1488.43",	//买单数量 quantity

	        "a":"6251.40600"//买单总量 amount

	      }

	    ],

    "asks":					//卖单 asks list

	    [

	      {

	        "p":"4.2000",	//卖单价格 price

	        "q":"1488.43",	//卖单数量 quantity

	        "a":"6251.40600"//卖单总量 amount

	      }

	    ]

  },

  "symbol":"VDS_USDT"	  //交易对

}
```



### 订阅交易对有限档位深度 Subscribe to trading pairs with limited depth

**Channel**:

request **sub.limit.depth**

response **push.limit.depth**

- 有效档位为: 5, 10, 20 available
  limit : 5 , 10, 20 
- 推送评率: 每秒推送 rate: per second

**Request Payload:**

```
{

  "op”:”sub.limit.depth",

  "symbol":"EOS_USDT",   //交易对

  "depth": 5

}
```

**Response Payload**

```
{

 "channel": "push.limit.depth",

 "data": {

  "asks": [

   [

    "2.5784",      //价格

    "1994.917"     //数量

   ],
  ],

  "bids": [

   [

    "2.5767",
    "588"
   ],
  ]

 },

 "symbol": "EOS_USDT",

 "depth": 5

}
```



### 订阅overview

**Channel**:

request **sub.overview**

push **push.overview**

**Request Payload:**

```
{

  "op": "sub.overview"

}
```

**Response Payload**

```
{

   "channel": "push.overview",

  "data": {

    "NEW_ETH": {

      "p": 0.00001412,

      "r": 0.0389

    },

    "BTC_ETH": {

      "p": 53.97062162,

      "r": -0.0042

    }

  }



}
```



#### 订阅cny

**Channel**:

request **sub.cny**

push **push.cny**

**Request Payload:**

```
{

  "op": "sub.cny"

}
```

**Response Payload**

```
{

   "channel": "push.cny",

  "data": {

    "NEW": "0",

    "BCHC": "0",

    "BSV": "0",

    "BCH": "0",

    "EOS": "7.78800007",

    "HMM": "0",

    "USDT": "7.08",

    "MX": "0.026904",

    "HHM": "0",

    "Biu": "0",

    "BTC": "80588.1",

    "BUC": "0",

    "Asia": "0",

    "ETH": "19.824"

  }

}
```



#### 订阅增量深度信息 Subscribe to incremental depth

订阅指定交易对的增量深度信息 Subscribe to incremental depth

**Channel**:

订阅 subscribe **sub.depth**

推送 push **push.depth**

**Request Payload:**

```
{

  "op":"sub.depth",

  "symbol": "BTC_USDT"

}
```

数据 data

```
{

  "symbol":"BTC_USDT",

  "data":

  {

    "version":"70981115",

    "bids":

    [{

      "p":"46977.11",   // 价格 price

      "q":"1.000000",   // 数量 quantity

      "a":"46977.11"   // 金额 amount

    }]

  },

  "channel":"push.depth"

}
```



## 私有接口 private channel



### 获取账户订单状态推送 Get account order status push

**Channel**:

operation **sub.personal**

**Request Payload:**

```
{

  "op":"sub.personal",  // sub key

  "api_key": "api_key",	//API Key

  "sign": "b8d2ff6432798ef858782d7fd109ab41",//签名,签名规则 把api_key、req_time以及及op用MD5私钥做一个签名  Use MD5 private key to sign api_key, req_time, and op

  "req_time": "1561433613583"	//当前时间的时间戳 current timestamp 

}
```

响应 response

response **push.personal.order**

**Response Payload**

```
{

  "channel": "sub.personal",

  "msg": "OK"

}
```

获取订阅私有接口数据的错误信息 Get the error message of subscribing to private interface data

response **rs.error**

**Response Payload**

```
{

  "channel":"sub.personal",//push key

  "msg":"signature validation failed",	//error message

}
```

push **push.personal.order**

**Response Payload**

```
{

  "channel":"push.personal.order",    //push key

  "symbol":"ETH_USDT",          // 交易对

  "data":{

    "price":1,             // 价格 price

    "quantity":5,            // 量 quantity

    "amount":5.01,           // 交易额（以计价货币计算） deal amount

    "remainAmount":5.01,        // 剩余交易额 remain deal amount

    "remainQuantity":5,         // 剩余量 remain deal quantity

    "id":"069e29f4-8870-489f-aebf",   // 订单id order id

    "status":1,             // 订单状态,1:未成交 2:已成交 3:部分成交 4:已撤单 5:部分撤单 order state 1. NEW New order 2.FILLED	3.PARTIALLY_FILLED	4.CANCELED	Order canceled 5.PARTIALLY_CANCELED	Order filled partially, and then the rest of the order is canceled

    "tradeType":1,           // 订单类型（1：买单。2：卖单） orderType : 1. bug 2.sell

    "createTime":1561518653000     // 订单创建时间戳 createTime

  }

}
```



### 获取订单成交推送

获取本账户下订单成交的逐笔推送信息

**Channel**:

operation **sub.personal.deals**

**Request Payload:**

```
{

  "op":"sub.personal",  // sub key

  "api_key": "api_key",	//申请的API Key

  "sign": "b8d2ff6432798ef858782d7fd109ab41",//签名,签名规则 把api_key、req_time以及及op用私钥做一个签名，使用MD5 加密

  "req_time": "1561433613583"	//当前时间的时间戳

}
```

响应

response **push.personal.deals**

**Response Payload**

```
{

  "channel": "sub.personal.deals",

  "msg": "OK"

}
```

获取订阅私有接口数据的错误信息

response **rs.error**

**Response Payload**

```
{

  "channel":"sub.personal.deals",//push key

  "msg":"signature validation failed",	//错误信息 error message

}
```

push **push.personal.order**

**Response Payload**

```
{

  "channel":"push.personal.deals",    //push key

  "symbol":"ETH_USDT",          // 交易对

  "data": {

    "t":1561465233455,//成交时间 deal time

    "p":"4.2003",	//交易价格 deal price

    "q":"86.68",	//成交数量 deal quantity

    "T":1,			//成交类型:1买、2卖  dealType : 1. bug 2.sell

    "M":1,     //自成交标记:1是，0否 isBuySelf : 1. true 2. false

    "id":"8659ba6653ff462ebb9cf274dc616cc9" //成交订单id deal order id

  }

}
```

Last updated 2021-09-15 14:54:27 CST 