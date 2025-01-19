---
sidebar_position: 1
---

**# GreenBTC 2.0**

**免费绿化查询**


```
  https://api.studio.thegraph.com/query/44303/greenbtc20sgraph/version/latest

  query MyQuery {
    greenBT20SUsers(
      first: 1000
      orderBy: timesLucky
      orderDirection: desc
      where: {timesNormal: 0}
      skip: 1000
    ) {
      id
      timesLucky
      timesNormal
    }
  }

  query MyQuery {
    greenBT20SUsers(
      first: 1000
      orderBy: timesLucky
      orderDirection: desc
      where: {timesNormal_gt: 0}
    ) {
      id
      timesNormal
      timesLucky
    }
  }

  query MyQuery {
    greenBT20SPassives(
      first: 1000
      orderBy: origin
      orderDirection: asc
      skip: 1000
    ) {
      id
      origin
      timesLuckyAttack
    }
  }

```


**+ Domain 配置信息**
  + https://github.com/arkreen/greenbtc-config
  + https://github.com/arkreen/greenbtc-config/blob/main/domains.json


```
{
    "domains": [
        {
            "domain_id": 1,
            "domain_key": "greenbtcv2",
            "domain_name": "GreenBTC v2",
            "domain_square": {
                "x": 0,
                "y": 320,
                "h": 64,
                "w": 64
            },
            "region": [163840, 163903, 196159, 196096],
            "box_price": 10,
            "box_top": 669611,
            "box_prize_total": 65536,
            "box_prize": [
                {
                    "token_key": "akre",
                    "token_amount": 3000,
                    "token_rate": 13,
                    "level":1
                },
                {
                    "token_key": "akre",
                    "token_amount": 1000,
                    "token_rate": 52,
                    "level":1
                },
                {
                    "token_key": "akre",
                    "token_amount": 400,
                    "token_rate": 328,
                    "level":1
                },
                {
                    "token_key": "akre",
                    "token_amount": 200,
                    "token_rate": 655,
                    "level":1
                },
                {
                    "token_key": "kwh",
                    "token_amount": 55,
                    "token_rate": 2621,
                    "level":2
                },
                {
                    "token_key": "kwh",
                    "token_amount": 3,
                    "token_rate": 9437,
                    "level":2
                },
                {
                    "token_key": "kwh",
                    "token_amount": 2,
                    "token_rate": 13107,
                    "level":3
                },
                {
                    "token_key": "gem",
                    "token_amount": 1,
                    "token_rate": 39323,
                    "level":3
                }
            ]
        },
        {
            "domain_id": 2,
            "domain_key": "pepe",
            "domain_name": "PEPE",
            "domain_square": {
                "x": 64,
                "y": 320,
                "h": 64,
                "w": 64
            },
            "region": [163904, 163967, 196223, 196160],
            "box_price": 10,
            "box_top": 671883,
            "box_prize_total": 65536,
            "box_prize": [
                {
                    "token_key": "gem",
                    "token_amount": 600,
                    "token_rate": 66,
                    "level":1
                },
                {
                    "token_key": "gem",
                    "token_amount": 300,
                    "token_rate": 131,
                    "level":1
                },
                {
                    "token_key": "gem",
                    "token_amount": 70,
                    "token_rate": 655,
                    "level":1
                },
                {
                    "token_key": "kwh",
                    "token_amount": 50,
                    "token_rate": 983,
                    "level":2
                },
                {
                    "token_key": "kwh",
                    "token_amount": 20,
                    "token_rate": 1966,
                    "level":2
                },
                {
                    "token_key": "gem",
                    "token_amount": 10,
                    "token_rate": 13107,
                    "level":3
                },
                {
                    "token_key": "gem",
                    "token_amount": 5,
                    "token_rate": 19661,
                    "level":3
                },
                {
                    "token_key": "kwh",
                    "token_amount": 1,
                    "token_rate": 28967,
                    "level":3
                }
            ]
        },
        {
            "domain_id": 3,
            "domain_key": "greenbtcv3-G",
            "domain_name": "GreenBTC v3 - G",
            "domain_square": {
                "x": 384,
                "y": 256,
                "h": 16,
                "w": 16
            },
            "region": [131456, 131471, 139151, 139136],
            "box_price": 10,
            "box_top": 172584,
            "box_prize_total": 65536,
            "box_prize": []
        }
    ]
}
```