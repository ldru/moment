---
sidebar_position: 1
---

# Monthly Burn AKRE

+ SubGraph Link

[https://api.studio.thegraph.com/query/44303/arec-graph/version/latest](https://api.studio.thegraph.com/query/44303/arec-graph/version/latest)

+ 2024年12月 

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

