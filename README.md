# clone-lin-rocket-reth

Experimental i64-scale LIN clone of [rocket-pool/rocketpool](https://github.com/rocket-pool/rocketpool) tag `v1.4` rETH exchange (`contracts/contract/token/RocketTokenRETH.sol`).

- **LIN clone:** [`src/lin_rocket_reth.lin`](src/lin_rocket_reth.lin)
- **Proofs (results only) live in lin-open:** https://github.com/kbelludoo/lin-open
- **Event receipt:** `docs/events/EVENT_ROCKET_RETH_CLONE_LIN.rulel` in lin-open

This repository is the standalone LIN copy. It is **not** Rocket Pool, **not** a staking router, and does **not** claim Solidity uint256 / mainnet rETH / deposit-pool parity.

Upstream RocketTokenRETH.sol is GPL-3.0-only. This LIN kernel is an original uint64-scale implementation of the published exchange-rate, not a verbatim Solidity dump.

Canonical goldens (uint64-scale, 128-bit product):

- `getRethValue(1000, 0, 0)` = **1000** (empty rethSupply is 1:1)
- named contrast Lido empty-div0: **0** shares for 1000 ETH empty
- named contrast OZ ERC-4626 +1/+1: **1000**
- named contrast Morpho VIRTUAL_SHARES=1e6: **1000000000**
- after 1-wei bootstrap + 1e6-ETH donation, victim of 1e6 ETH: Rocket/Lido **0** vs OZ **1** vs Morpho **1999996**
- `getRethValue(1000, 5000, 2000)` = **400**; `getEthValue(400, 5000, 2000)` = **1000**
- `getRethValue(1000, 0, 2000)` = **0** (Solidity reverts; LIN fail-closes)
- empty `getExchangeRate` = **1e18**; `1e18*20/1` fail-closes to **0**
- `1e18 * 1e18 / 1` fail-closes to **0**
