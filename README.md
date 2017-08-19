# EtherLotto
Ethereum blockchain based lottery.

## Rationale

This implementation uses a simplistic (almost)stochastic value from the following input data:

```
// Compute some *almost random* value for selecting winner from current transaction.
var random = uint(block.blockhash(block.number)) + block.timestamp + block.difficulty + block.number;
```

That computed value is far from beeing perfect but it's enough randomized for testing pourposes.

Blockchains are deterministic so it's difficult to provide a secure random source, but it's possible using some bridge between the Bitcoin blockchain & Ethereum smart contracts so instead using Ethereum block time, an automated lottery game can use higher block exchange rate from Bitcoin's blockchain increasing the entropy quality.
