# ethers-multicall

[![npm package][npm-img]][npm-url]
[![Build Status][build-img]][build-url]
[![Downloads][downloads-img]][downloads-url]
[![Issues][issues-img]][issues-url]
[![Commitizen Friendly][commitizen-img]][commitizen-url]
[![Semantic Release][semantic-release-img]][semantic-release-url]

> ⚡🚀 Call multiple view functions, from multiple Smart Contracts, in a single RPC query!

Querying an RPC endpoint can be very costly (**100+ queries**) when loading data from multiple smart contracts.
With multicall, batch these queries into a single, on-chain query, without additional over-head!

This is the standalone package of the library formerly created & used by [Zapper](https://github.com/Zapper-fi/studio/tree/main/src/multicall).

## Install

```bash
npm install @morpho-labs/ethers-multicall
```

```bash
yarn add @morpho-labs/ethers-multicall
```

## Usage

```typescript
import { ethers } from "ethers";

import { EthersMulticall } from "@morpho-labs/ethers-multicall";

const provider = new ethers.providers.JsonRpcBatchProvider("...");
const multicall = new EthersMulticall(provider);

const uni = multicall.wrap(
  new ethers.Contract("0x1f9840a85d5aF5bf1D1762F925BDADdC4201F984", UniswapAbi)
); // make sure to always wrap contracts to benefit from multicalls

Promise.all([
  uni.name(),
  uni.symbol(),
  uni.decimals(),
  uni.inexistantFunction().catch(() => "default value"),
]).then(console.log);
```

[build-img]: https://github.com/morpho-labs/ethers-multicall/actions/workflows/release.yml/badge.svg
[build-url]: https://github.com/morpho-labs/ethers-multicall/actions/workflows/release.yml
[downloads-img]: https://img.shields.io/npm/dt/@morpho-labs/ethers-multicall
[downloads-url]: https://www.npmtrends.com/@morpho-labs/ethers-multicall
[npm-img]: https://img.shields.io/npm/v/@morpho-labs/ethers-multicall
[npm-url]: https://www.npmjs.com/package/@morpho-labs/ethers-multicall
[issues-img]: https://img.shields.io/github/issues/morpho-labs/ethers-multicall
[issues-url]: https://github.com/morpho-labs/ethers-multicall/issues
[codecov-img]: https://codecov.io/gh/morpho-labs/ethers-multicall/branch/main/graph/badge.svg
[codecov-url]: https://codecov.io/gh/morpho-labs/ethers-multicall
[semantic-release-img]: https://img.shields.io/badge/%20%20%F0%9F%93%A6%F0%9F%9A%80-semantic--release-e10079.svg
[semantic-release-url]: https://github.com/semantic-release/semantic-release
[commitizen-img]: https://img.shields.io/badge/commitizen-friendly-brightgreen.svg
[commitizen-url]: http://commitizen.github.io/cz-cli/
