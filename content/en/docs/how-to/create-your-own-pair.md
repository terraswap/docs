---
title: Create Your Own Pair
weight: 30
---

{{< alert context="warning" >}}
**Important - Only for Terra 2.0**

PLEASE BE AWARE that native tokens must be registered in the factory first in order to create a pair including them. You can check registered native tokens through [this query]({{< ref "/docs/reference/factory#native-token-decimals" >}}). Contact us via [Terraswap Discord](https://discord.gg/XERFR8dCWv) if you need to add a new native token.
{{< /alert >}}

## Instantiation by Contract Address

You can use the Terraswap token factory contract.
- The address on Terra 2.0: `terra1466nf3zuxpya8q9emxukd7vftaf6h4psr0a07srl5zw74zh84yjqxl5qul`
- The address on Terra Classic: `terra1jkndu9w5attpz09ut02sgey5dd3e8sq5watzm0`

The JSON message format is as follows:

```json
{
  "create_pair": {
    "asset_infos": [
      {
        "token": {
          "contract_addr": "terra..."
        }
      },
      {
        "native_token": {
          "denom": "uluna"
        }
      }
    ]
  }
}
```

This is a JSON constructor of pair contract. Tokens of pair can be either CW20 tokens or Terra(Classic) native tokens(including IBC tokens). Use JSON keys with their corresponding values as described below.
- `asset_infos[x].token.contract_addr`: CW20 token **address**
- `asset_infos[x].native_token.denom`: Terra(Classic) native token(including IBC token) **denominator**

Then, you may execute the contract with the organized JSON above.

## Provide initial liquidity

Terraswap pair contract derives the swap rate from the amount of the remained assets on the pool. However, if you have just created your own pair and haven't provided its liquidity yet, the contract won't be able to calculate the rate, and all swap simulations and transactions will fail. So, for the pair to work successfully, you should provide the initial liquidity.

{{< alert context="warning" >}}
**Warning**

In order to prevent LP inflation attacks, when a user provides initial liquidity, the amount of minimum liquidity will belong to the pair contract itself and be permanently locked. Thus, the initial provider should be aware that some of their shares will be sacrificed by the amount of minimum liquidity (0.001 shares of LP tokens with 6 decimal places, equal to 1000uLp) for this protection, and they will receive the amount of LP tokens which the minimum liquidity is deducted from.
{{< /alert >}}
