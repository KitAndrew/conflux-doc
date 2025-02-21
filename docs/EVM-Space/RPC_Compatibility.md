---
id: evm_space_rpc_compatibility
title: Compatibility with the Web3 JSON-RPC Protocol
custom_edit_url: https://github.com/Conflux-Chain/conflux-doc/edit/master/docs/EVM-Space/RPC_Compatibility.md
keywords:
  - RPC
---

The Conflux EVM space implements the Web3 JSON-RPC protocol.

## Methods

| Method                 | Status      | Note    |
| ---------------------- | ----------- |-------- |
| web3_clientVersion     | ✅       |  |
| net_version | ✅       |  |
| eth_protocolVersion | ✅       |  |
| eth_chainId | ✅ | |
| eth_gasPrice | ✅ | |
| eth_blockNumber | ✅ | |
| eth_getBalance | ✅ | |
| eth_getStorageAt | ✅ | |
| eth_getCode | ✅ | |
| eth_getTransactionCount | ✅ | |
| eth_sendRawTransaction | ✅ | |
| eth_submitTransaction | ✅ | |
| eth_call | ✅ | |
| eth_estimateGas | ✅ | |
| eth_getTransactionByHash | ✅ |  |
| eth_getTransactionReceipt | ✅ |  |
| eth_getLogs | ✅ | The max gap between fromBlock and toBlock is limited to 1000|
| eth_getBlockByHash | ✅ |  |
| eth_getBlockByNumber | ✅ | |
| eth_getBlockTransactionCountByHash | ✅ | |
| eth_getBlockTransactionCountByNumber | ✅ | |
| eth_getTransactionByBlockHashAndIndex | ✅ | |
| eth_getTransactionByBlockNumberAndIndex | ✅ | |
| eth_syncing | ✅ |  |
| eth_hashrate | ✅ |  |
| eht_coinbase | ✅ |  |
| eth_mining | ✅ |  |
| eth_maxPriorityFeePerGas | ✅ |  |
| eth_accounts | ✅ |  |
| eth_submitHashrate | ✅ |  |
| eth_getUncleByBlockHashAndIndex | ✅ |  |
| eth_getUncleByBlockNumberAndIndex | ✅ |  |
| eth_getUncleCountByBlockHash | ✅ |  |
| eth_getUncleCountByBlockNumber | ✅ |  |
| parity_getBlockReceipts | ✅ |  |
| eth_pendingTransactions | 🚧 | |
| web3_sha3 | 🚧 | |
| trace_block | ✅ | Parity RPC |
| trace_filter | ✅ | Parity RPC  |
| trace_transaction | ✅ | Parity RPC  |
| eth_feeHistory | ❌ | |
| eth_getFilterChanges | ❌ | |
| eth_getFilterLogs | ❌ | |
| eth_newBlockFilter | ❌ | |
| eth_newFilter | ❌ | |
| eth_newPendingTransactionFilter | ❌ | |
| eth_uninstallFilter | ❌ | |
| net_listening | ❌ | |
| net_peerCount | ❌ | |
| eth_compileLLL | ❌ | |
| eth_compileSerpent | ❌ | |
| eth_compileSolidity | ❌ | |
| eth_getCompilers | ❌ | |
| eth_getProof | ❌ | EIP-1186 |
| eth_getWork | ❌ | |
| db_* | ❌ | |
| shh_* | ❌ | |
|  |  | |

Legend: ❌ = not supported. 🚧 = work in progress. ✅ = supported.

## Notes

* `eth_sendRawTransaction` only accept 155 transaction, `1559`, `2930` is not supported
* Methods not listed here are also not supported.
* There is no concept of uncle (aka ommer) blocks. The `eth_getUncleByBlockHashAndIndex` and `eth_getUncleByBlockNumberAndIndex` methods always return `null`. The `eth_getUncleCountByBlockHash` and `eth_getUncleCountByBlockNumber` methods return zero for valid block IDs and `null` for invalid block IDs. Additionally, uncle-related block metadata such as `sha3Uncles` is sha3 of empty hash array.
* The nonstandard Geth tracing APIs are not supported at present
* The nonstandard Parity tracing APIs are in progress

### `pending` tag

Only `eth_getTransactionCount` method has supported `pending` tag. Other method will treat `pending` tag as `latest`

* eth_getTransactionCount ✅
* eth_getBalance
* eth_getCode
* eth_getStorageAt
* eth_call

## Data verifiability

Below fields can not guarantee the verifiability

### Block

* hash
* stateRoot
* receiptsRoot
* transactionsRoot
* totalDifficulty

### Receipt

* logsBloom

## pub/sub

Ethereum event pub/sub is not supported now.

## ETH RPC docs

* [Ethereum JSON-RPC Specification](https://playground.open-rpc.org/?schemaUrl=https://raw.githubusercontent.com/ethereum/eth1.0-apis/assembled-spec/openrpc.json&uiSchema%5BappBar%5D%5Bui:splitView%5D=false&uiSchema%5BappBar%5D%5Bui:input%5D=false&uiSchema%5BappBar%5D%5Bui:examplesDropdown%5D=false)
* [ethereum/execution-apis](https://github.com/ethereum/execution-apis)
* [Infura JSON-RPC doc](https://infura.io/docs/ethereum#tag/JSON-RPC-Methods)
* [eth RPC wiki](https://eth.wiki/json-rpc/API)
* [geth RPC doc](https://geth.ethereum.org/docs/rpc/server)
* [Parity RPC doc](https://openethereum.github.io/JSONRPC)
