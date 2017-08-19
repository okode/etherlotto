# EtherLotto
Ethereum blockchain based lottery.

## Playing

If you want to play to this lottery game send 10 weis in the following smart contract:

![Smart contract QR code](etherlotto-qr.jpg)

```
0x3d212eA8cB9b5795A374956cdB193EEE7802c37e
```

If you are the lucky winner then all the jackpot will be sent to your account.

## Rationale

This implementation uses a simplistic (almost)stochastic value from the following input data:

```
// Compute some *almost random* value for selecting winner from current transaction.
var random = uint(block.blockhash(block.number)) + block.timestamp + block.difficulty + block.number;
```

That computed value is far from beeing perfect but it's enough randomized for testing pourposes.

Blockchains are deterministic so it's difficult to provide a secure random source, but it's possible using some bridge between the Bitcoin blockchain & Ethereum smart contracts so instead using Ethereum block time, an automated lottery game can use higher block exchange rate from Bitcoin's blockchain increasing the entropy quality.

## Verifying contract

If you need you can verify this smart contract in the public Ethereum blockchain explorer:

https://etherscan.io/address/0x3d212ea8cb9b5795a374956cdb193eee7802c37e
