
# What is Just Mint

Just Mint means:
1. Just Mint protocol.
2. Just Mint application, which implements Just Mint protocol.
3. Just Mint Token, which is the first token minted according to Just Mint protocol.

## Just Mint protocol

### Minting curve

Just Mint protocol defines the token minting rules based on virtual liquidity curve [1].

We use token X as the base token, and token Y as the quote token. Anyone can use token X to mint token Y. Token X is the the token already alive, such as SOL, ETH, POL or UDSC, USDT. Token Y is the new token to mint. Creator of token Y defines the configuration token Y are minted. Noramlly it is defined by two points on the liquidity curve. 

The start point (x0,y0) and the end point (x1, y1) on the curve define the all the minting configution. The minting curve is:
  x * y = k

at any time with the payment x', the minting output is: 
  y' = y - (x0 * y0) / (x + x')

y1-y0 is the cap of the token available to mint. While the cap is reached, the minting process is ended.

x1-x0 is all the payment to mint the all the token.

x0/y0 is the initial minting price.

x1/y1 is the ending minting price.

### Liquidity Pool

Anyone can mint token Y with token X, and create the the liquidity pool with the received token Y. Just Mint Dapp allows only one liquidity pool is created.

The creator of the liquidity pool decides all the parameters of the liquidity pool, including intitial price, fee rate, and so on.

Once the amount of token X received as the income in the Dapp surpass the threshold (Xt), anyone can use these token X to buy token Y from the liquididty pool, and all the received token Y will be burned forever. The amount of Token X used to buy Token Y must be times of Xt.

While all the received Token X are used to buy and burn Token Y, the last supply Y will be the final supply of Token Y.

## **Just Mint** application

**Just Mint** application provide the UI to interact with **Just Mint** smart contract. Anyone can operate with **Just Mint** to:
 + Create a new token Y
 + Mint token Y with some amount of token X.
 + Create the liquidity pool of Token Y and Token X.
 + Buy and burn token Y with the received token X. 

Anyone can buy/sell Token Y with any 3rd-party DEX they are happy to use.

In the begining, creating a new token is totally free. A small amount of creating fee may be charged while **Just Mint** application is mature.  

## **Just Mint** token

**Just Mint** is the first token compliant with **"Just Mint"** minting rules with following configuration:

Token X: WSOL
Token Y: Name: "Just Mint Token", Symbol: 'JSMT', decimal: 6
x0: 10 SOL
y1: 110 Billion
x1: 110 SOL
y1: 10 Billion
Xt: 0.1 SOL




## References
[1] https://app.uniswap.org/whitepaper-v3.pdf


