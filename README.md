# EtherLotto
Ethereum blockchain based lottery.

## Playing

If you want to play to this lottery game invoked `play` method sending 10 weis to the following smart contract:

![Smart contract QR code](etherlotto-qr.jpg)

```
0x3d212eA8cB9b5795A374956cdB193EEE7802c37e
```

If you are the lucky winner then all the jackpot will be sent to your account.

## Smart contract ABI

```
[{
    constant: true,
    inputs: [],
    name: "pot",
    outputs: [{
        name: "",
        type: "uint256"
    }],
    payable: false,
    type: "function"
}, {
    constant: true,
    inputs: [],
    name: "bank",
    outputs: [{
        name: "",
        type: "address"
    }],
    payable: false,
    type: "function"
}, {
    constant: false,
    inputs: [],
    name: "play",
    outputs: [],
    payable: true,
    type: "function"
}, {
    inputs: [],
    payable: false,
    type: "constructor"
}]
```

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

## Testing

(assume you have created first etherbase account with some funding ether)

```
$ geth --syncmode "light"

$ geth account new
$ geth account new
$ geth account new

$ geth attach

> var myfunds = web3.eth.accounts[0]
> var a1 = web3.eth.accounts[1]
> var a2 = web3.eth.accounts[2]
> var a3 = web3.eth.accounts[3]

> personal.unlockAccount(myfunds)

> eth.sendTransaction({from: myfunds, to: a1, value: web3.toWei(.033, 'ether')})
> eth.sendTransaction({from: myfunds, to: a2, value: web3.toWei(.033, 'ether')})
> eth.sendTransaction({from: myfunds, to: a3, value: web3.toWei(.033, 'ether')})

> var etherlotto = eth.contract(
[{"constant":true,"inputs":[],"name":"pot","outputs":[{"name":"","type":"uint256"}],"payable":false,"type":"function"},{"constant":true,"inputs":[],"name":"bank","outputs":[{"name":"","type":"address"}],"payable":false,"type":"function"},{"constant":false,"inputs":[],"name":"play","outputs":[],"payable":true,"type":"function"},{"inputs":[],"payable":false,"type":"constructor"}]).at("0x3d212eA8cB9b5795A374956cdB193EEE7802c37e")

> web3.eth.sendTransaction({from: a1, to: etherlotto.address, value: 10, data: etherlotto.play.getData()})

```