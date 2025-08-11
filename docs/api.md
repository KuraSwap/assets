# KuraSwap Routing API — Quote Endpoint

This document describes how to call the **quote** endpoint of the KuraSwap Routing API (a fork of Uniswap's routing-api), the meaning of each query parameter, and the structure of the response.

> **Base URL**: `GET /quote`
>
> Example (Sei, chainId `1329`):
>
> ```text
> https://routing.kuraswap.org/quote?tokenInAddress=0x4b416A45e1f26a53D2ee82a50a4C7D7bE9EdA9E4&tokenOutAddress=0xe15fc38f6d8c56af07bbcbe3baf5708a2bf42392&amount=1000000000000000000&type=exactIn&tokenInChainId=1329&tokenOutChainId=1329&protocols=v2%2Cv3%2Cmixed&enableUniversalRouter=true&slippageTolerance=0.5&deadline=1800
> ```

---

## Query Parameters

| Name                    | Type                   | Description                                                                                           |
| ----------------------- | ---------------------- | ----------------------------------------------------------------------------------------------------- |
| `tokenInAddress`        | `string`               | Address of the **input** token. Use `0xeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeee` for the native coin. |
| `tokenOutAddress`       | `string`               | Address of the **output** token. Use `0xeeee…eeee` for the native coin.                               |
| `amount`                | `string`               | Amount in smallest unit (wei-like). `exactIn` → amount in; `exactOut` → amount out.                   |
| `type`                  | `exactIn`              | Quote type.                                                                                           |
| `tokenInChainId`        | `number`               | Chain ID for input token. **Sei = 1329**.                                                             |
| `tokenOutChainId`       | `number`               | Chain ID for output token. **Sei = 1329**.                                                            |
| `protocols`             | `string`               | Comma-separated list: `v2`, `v3`, `mixed`.                                                            |
| `enableUniversalRouter` | `boolean`              | If `true`, includes `methodParameters` for direct Universal Router execution.                         |
| `slippageTolerance`     | `string`               | Slippage tolerance (e.g., `0.5` for 0.5%).                                                            |
| `deadline`              | `number`               | TTL in seconds (e.g., `1800` for 30 min).                                                             |

---

## Example Request

```text
GET /quote?tokenInAddress=0x4b416A45e1f26a53D2ee82a50a4C7D7bE9EdA9E4&tokenOutAddress=0xe15fc38f6d8c56af07bbcbe3baf5708a2bf42392&amount=1000000000000000000&type=exactIn&tokenInChainId=1329&tokenOutChainId=1329&protocols=v2,v3,mixed&enableUniversalRouter=true&slippageTolerance=0.5&deadline=1800
```

---

## Example Response

```json
{
  "methodParameters": {
    "calldata": "0x3593564c...",
    "value": "0x00",
    "to": "0x6004b32424c0e017688458E67F677658260ca25e"
  },
  "blockNumber": "162089148",
  "amount": "1000000000000000000",
  "amountDecimals": "1",
  "quote": "1337923",
  "quoteDecimals": "1.337923",
  "quoteGasAdjusted": "1337922",
  "quoteGasAdjustedDecimals": "1.337922",
  "gasUseEstimate": "273000",
  "gasPriceWei": "100",
  "route": [
    [
      { "type": "v3-pool", "address": "0x2110F13bC40e3d254C5f1C54D4D89cddB9a985aF", ... },
      { "type": "v3-pool", "address": "0x361cCee286Ba3cb7Ab7af3F193D2c2B47168F89f", ... },
      { "type": "v3-pool", "address": "0x5A8cbf6E7B8917F2b7663758cec671A0705e2511", ... }
    ]
  ],
  "routePercentages": [ { "protocol": "V3", "percent": "100.00", "tokenPath": [ ... ] } ],
  "routeString": "[V3] 100.00% = KURA -- 0.3% ... --> USDC",
  "priceImpact": "0.6264"
}
```

---

## Executing the Swap

When `enableUniversalRouter=true`, you can send `methodParameters.calldata` and `methodParameters.value` directly to the Universal Router.

```ts
const tx = await signer.sendTransaction({
  to: methodParameters.to,
  data: methodParameters.calldata,
  value: methodParameters.value
});
```

---

## Notes

* **Native coin**: Use `0xeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeee`.
* **Sei**: Chain ID = `1329`.
* **Universal Router**: Allows direct transaction execution using returned `methodParameters`.
