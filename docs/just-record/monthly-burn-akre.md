---
sidebar_position: 1
---

# Monthly Burn AKRE

+ SubGraph Link

[https://api.studio.thegraph.com/query/44303/arec-graph/version/latest](https://api.studio.thegraph.com/query/44303/arec-graph/version/latest)

+ 2025年1月 

1月份发行收入:    10879899.420327 AKRE,   
  预计销毁:       8703919.536261600 AKRE
  Treasury收入:   2175979.884065400 AKRE
1月份消纳收入:      7506000.31 AKRE
  预计销毁:         6004800.248000000  AKRE
  Treasury收入:     1501200.062000000  AKRE
合计:
  预计销毁:       14708719.784261600  AKRE
  Treasury收入:     3677179.946065400  AKRE

```
query MyQuery {
  arecoverviews(block: {number: 67387132}) {
    numARECNFTCertified
    numARECNFTLiquidized
    numARECNFTMinted
    numARECNFTRedeemed
    numClimateAction
    numClimateBadge
    amountARECNFTCertified
    amountARECNFTLiquidized
    amountARECNFTMinted
    amountARECNFTRedeemed
    amountARECOffsetClaimed
  }
}

{
  "data": {
    "arecoverviews": [
      {
        "numARECNFTCertified": 46618,
        "numARECNFTLiquidized": 45990,
        "numARECNFTMinted": 46993,
        "numARECNFTRedeemed": 353,
        "numClimateAction": 33539,
        "numClimateBadge": 33383,
        "amountARECNFTCertified": "142914670584784",
        "amountARECNFTLiquidized": "142801899914055",
        "amountARECNFTMinted": "150729667995725",
        "amountARECNFTRedeemed": "41794069905",
        "amountARECOffsetClaimed": "129317942387001"
      }
    ]
  }
}

```

+ 2024年12月 

```
query MyQuery {
  arecoverviews(block: {number: 66158917}) {
    numARECNFTCertified
    numARECNFTLiquidized
    numARECNFTMinted
    numARECNFTRedeemed
    numClimateAction
    numClimateBadge
    amountARECNFTCertified
    amountARECNFTLiquidized
    amountARECNFTMinted
    amountARECNFTRedeemed
    amountARECOffsetClaimed
  }
}

{
  "data": {
    "arecoverviews": [
      {
        "numARECNFTCertified": 27035,
        "numARECNFTLiquidized": 26461,
        "numARECNFTMinted": 27406,
        "numARECNFTRedeemed": 353,
        "numClimateAction": 33531,
        "numClimateBadge": 33375,
        "amountARECNFTCertified": "132034771164457",
        "amountARECNFTLiquidized": "131917382125078",
        "amountARECNFTMinted": "132088710445398",
        "amountARECNFTRedeemed": "41794069905",
        "amountARECOffsetClaimed": "121811942077001"
      }
    ]
  }
}

```

+ 2024年11月 

```
query MyQuery {
  arecoverviews(block: {number: 64932348}) {
    numARECNFTCertified
    numARECNFTLiquidized
    numARECNFTMinted
    numARECNFTRedeemed
    numClimateAction
    numClimateBadge
    amountARECNFTCertified
    amountARECNFTLiquidized
    amountARECNFTMinted
    amountARECNFTRedeemed
    amountARECOffsetClaimed
  }
}

{
  "data": {
    "arecoverviews": [
      {
        "numARECNFTCertified": 19270,
        "numARECNFTLiquidized": 18737,
        "numARECNFTMinted": 19522,
        "numARECNFTRedeemed": 353,
        "numClimateAction": 33526,
        "numClimateBadge": 33370,
        "amountARECNFTCertified": "129400887458855",
        "amountARECNFTLiquidized": "129294696942634",
        "amountARECNFTMinted": "129453693749796",
        "amountARECNFTRedeemed": "41794069905",
        "amountARECOffsetClaimed": "118188742077001"
      }
    ]
  }
}

```

