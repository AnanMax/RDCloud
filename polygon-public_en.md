### Polygon-public Gateway Access Instructions


#### 1. Unzip the downloaded file

You can get the node access address and authorized node name

Gateway address: You can find the gateway address in nodeInfo.xlsx file: http://10.0.51.35:18601

Authorized node name: The node name that you can access. Example: bor-node1.default-no2024032600001.shanghai.bsnbase.com

#### 2. Get node authentication key

Example: 613168a8059c79434687ff7903fad416ae6a6d2a

![image-20240401175256422](wuhan.assets/image-20240401175256422.png)



#### 3. Request Bor node

* RPC Access Address

  Gateway_url/api/[Access Key]/rpc

  Example: 

  http://10.0.51.35:18601/api/613168a8059c79434687ff7903fad416ae6a6d2a/rpc

##### 3.1  eth_blockNumber

Returns the number of most recent block.

**Parameters**

None

**Returns**

`QUANTITY` - integer of the current block number the client is on.

**Example** 

```shell
// Request
curl -X POST -H "Content-Type:application/json" --data '{"jsonrpc":"2.0","method":"eth_blockNumber","params":[],"id":83}'
// Result
{
  "id":83,
  "jsonrpc": "2.0",
  "result": "0x3597572" 
}
```


* Response:

```shell
curl -X POST -H "Content-Type:application/json"  -H "Host:bor-node1.default-no2024032600001.shanghai.bsnbase.com"   --data '{"jsonrpc":"2.0","method":"eth_blockNumber","params":[],"id":1}'  http://10.0.51.35:18601/api/613168a8059c79434687ff7903fad416ae6a6d2a/rpc
```



##### 3.2  eth_getBlockByNumber

Returns information about a block by block number.

**Parameters**

1. `QUANTITY|TAG` - integer of a block number, or the string `"earliest"`, `"latest"`, `"pending"`, `"safe"` or `"finalized"`, as in the [default block parameter](https://ethereum.org/en/developers/docs/apis/json-rpc/#default-block).
2. `Boolean` - If `true` it returns the full transaction objects, if `false` only the hashes of the transactions.

```js
params: [
  "0x1b4", // 436
  true,
]
```

**Returns**

`Object` - A block object, or `null` when no block was found:

- `number`: `QUANTITY` - the block number. `null` when its pending block.
- `hash`: `DATA`, 32 Bytes - hash of the block. `null` when its pending block.
- `parentHash`: `DATA`, 32 Bytes - hash of the parent block.
- `nonce`: `DATA`, 8 Bytes - hash of the generated proof-of-work. `null` when its pending block.
- `sha3Uncles`: `DATA`, 32 Bytes - SHA3 of the uncles data in the block.
- `logsBloom`: `DATA`, 256 Bytes - the bloom filter for the logs of the block. `null` when its pending block.
- `transactionsRoot`: `DATA`, 32 Bytes - the root of the transaction trie of the block.
- `stateRoot`: `DATA`, 32 Bytes - the root of the final state trie of the block.
- `receiptsRoot`: `DATA`, 32 Bytes - the root of the receipts trie of the block.
- `miner`: `DATA`, 20 Bytes - the address of the beneficiary to whom the mining rewards were given.
- `difficulty`: `QUANTITY` - integer of the difficulty for this block.
- `totalDifficulty`: `QUANTITY` - integer of the total difficulty of the chain until this block.
- `extraData`: `DATA` - the "extra data" field of this block.
- `size`: `QUANTITY` - integer the size of this block in bytes.
- `gasLimit`: `QUANTITY` - the maximum gas allowed in this block.
- `gasUsed`: `QUANTITY` - the total used gas by all transactions in this block.
- `timestamp`: `QUANTITY` - the unix timestamp for when the block was collated.
- `transactions`: `Array` - Array of transaction objects, or 32 Bytes transaction hashes depending on the last given parameter.
- `uncles`: `Array` - Array of uncle hashes.

* Example request:

  ```shell
  // Request
  curl -X POST -H "Content-Type:application/json" --data '{"jsonrpc":"2.0","method":"eth_getBlockByNumber","params":["0x1b4", true],"id":1}'
  // Result
  {
    "jsonrpc": "2.0",
    "id": 1,
    "result": {
        "number": "0x1b4",
        "hash": "0xa284f649d7d9a3c0dea48e3bf3d295767a4893902e61d27e1590d4cece691b6f",
        "transactions": [

        ],
        "totalDifficulty": "0xbed",
        "logsBloom": "0x00000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000",
        "receiptsRoot": "0x56e81f171bcc55a6ff8345e692c0f86e5b48e01b996cadc001622fb5e363b421",
        "extraData": "0xd58301090083626f7286676f312e3133856c696e757800000000000000000000e14198dde4da0ea1015e9d38ad288f5ba62cf8d1b9a98ccd02fb6f75553ee51c70caa1c376cf4a937c644cae060effe8bf25409cef9ecd25013a608b3a51cbef00",
        "nonce": "0x0000000000000000",
        "miner": "0x0000000000000000000000000000000000000000",
        "difficulty": "0x7",
        "gasLimit": "0xe984c2",
        "gasUsed": "0x0",
        "uncles": [

        ],
        "sha3Uncles": "0x1dcc4de8dec75d7aab85b567b6ccd41ad312451b948a7413f0a142fd40d49347",
        "size": "0x260",
        "transactionsRoot": "0x56e81f171bcc55a6ff8345e692c0f86e5b48e01b996cadc001622fb5e363b421",
        "stateRoot": "0x01b797385461764bd56336dd5e810f3d57529d47bcbf3260c7d9c770bf6c5af4",
        "mixHash": "0x0000000000000000000000000000000000000000000000000000000000000000",
        "parentHash": "0x9481d3bb2bbe842f0e4703cb5be094d95650fe8345b4da5642ed27bec3acd0d5",
        "timestamp": "0x5ed28d86"
    }
  }
  ```

* Response:

  ```shell
  curl -X POST  -H "Content-Type:application/json" -H "Host:bor-node1.default-no2024032600001.shanghai.bsnbase.com"   --data '{"jsonrpc":"2.0","method":"eth_getBlockByNumber","params":["0x1b4", true],"id":1}'  http://10.0.51.35:18601/api/613168a8059c79434687ff7903fad416ae6a6d2a/rpc
  ```




##### 3.3  net_version

Returns the current network id.

**Parameters**

None

**Returns**

- **String** - The current network id.

* Example request:

  ```shell
  curl https://localhost:8545 -X POST -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"net_version","params":[],"id":1}'
  ```

* Response:

  ```shell
  curl -X POST  -H "Content-Type:application/json" -H "Host:bor-node1.default-no2024032600001.shanghai.bsnbase.com"   --data '{"jsonrpc":"2.0","method":"net_version","params":[],"id":1}'  http://10.0.51.35:18601/api/613168a8059c79434687ff7903fad416ae6a6d2a/rpc
  ```



##### 3.4 txpool_status

Returns the number of transactions currently pending for inclusion in the next block(s), as well as the ones that are being scheduled for future execution only.

**Parameters**

None

* Example request:

  ```shell
  curl  https://rpc-endpoint.io:8545 -X POST -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"txpool_status","params":[],"id":1}'
  ```

* Response:

  ```shell
  curl -X POST  -H "Content-Type:application/json" -H "Host:bor-node1.default-no2024032600001.shanghai.bsnbase.com"   --data '{"jsonrpc":"2.0","method":"txpool_status","params":[],"id":1}'  http://10.0.51.35:18601/api/613168a8059c79434687ff7903fad416ae6a6d2a/rpc
  ```



**Please refer to the** [Bor node API document](https://github.com/0xPolygon/polygon-edge/tree/develop/docs/docs/api) **for more commands.**



#### 4. Requst heimdall node

* RPC Access Address

  Gateway_url/api/[Access Key]/rpc

  Example: 

  http://10.0.51.35:18601/api/613168a8059c79434687ff7903fad416ae6a6d2a/rpc

##### 4.1 net_info

Get network info.

**Parameters**

None

* Example request:

  ```shell
  // Request
  curl -X POST -H "Content-Type:application/json" http://localhost:26657/net_info

  // Result
  {
    "id": 0,
    "jsonrpc": "2.0",
    "result": {
      "listening": true,
      "listeners": [
        "Listener(@)"
      ],
      "n_peers": "1",
      "peers": [
        {
          "node_info": {
            "protocol_version": {
              "p2p": "7",
              "block": "10",
              "app": "0"
            },
            "id": "5576458aef205977e18fd50b274e9b5d9014525a",
            "listen_addr": "tcp:0.0.0.0:26656",
            "network": "cosmoshub-2",
            "version": "0.32.1",
            "channels": "4020212223303800",
            "moniker": "moniker-node",
            "other": {
              "tx_index": "on",
              "rpc_address": "tcp:0.0.0.0:26657"
            }
          },
          "is_outbound": true,
          "connection_status": {
            "Duration": "168901057956119",
            "SendMonitor": {
              "Active": true,
              "Start": "2019-07-31T14:31:28.66Z",
              "Duration": "168901060000000",
              "Idle": "168901040000000",
              "Bytes": "5",
              "Samples": "1",
              "InstRate": "0",
              "CurRate": "0",
              "AvgRate": "0",
              "PeakRate": "0",
              "BytesRem": "0",
              "TimeRem": "0",
              "Progress": 0
            },
            "RecvMonitor": {
              "Active": true,
              "Start": "2019-07-31T14:31:28.66Z",
              "Duration": "168901060000000",
              "Idle": "168901040000000",
              "Bytes": "5",
              "Samples": "1",
              "InstRate": "0",
              "CurRate": "0",
              "AvgRate": "0",
              "PeakRate": "0",
              "BytesRem": "0",
              "TimeRem": "0",
              "Progress": 0
            },
            "Channels": [
              {
                "ID": 48,
                "SendQueueCapacity": "1",
                "SendQueueSize": "0",
                "Priority": "5",
                "RecentlySent": "0"
              }
            ]
          },
          "remote_ip": "95.179.155.35"
        }
      ]
    }
  }
  ```


* Response:

  ```shell
  curl -X POST -H "Content-Type:application/json"  -H "Host:heimdalld-node1.default-5ce0a8f9dc0872b.shenzhen.bsnbase.com" http://10.0.51.35:18601/api/613168a8059c79434687ff7903fad416ae6a6d2a/rpc/net_info
  ```



##### 4.2 status

Get Tendermint status including node info, pubkey, latest block hash, app hash, block height and time.

**Parameters**

None

* Example request: 

  ```shell
  // Request
  curl -X POST -H "Content-Type:application/json" http://localhost:26657/status

  // Result
  {
    "id": 0,
    "jsonrpc": "2.0",
    "result": {
      "node_info": {
        "protocol_version": {
          "p2p": "7",
          "block": "10",
          "app": "0"
        },
        "id": "5576458aef205977e18fd50b274e9b5d9014525a",
        "listen_addr": "tcp:0.0.0.0:26656",
        "network": "cosmoshub-2",
        "version": "0.32.1",
        "channels": "4020212223303800",
        "moniker": "moniker-node",
        "other": {
          "tx_index": "on",
          "rpc_address": "tcp:0.0.0.0:26657"
        }
      },
      "sync_info": {
        "latest_block_hash": "790BA84C3545FCCC49A5C629CEE6EA58A6E875C3862175BDC11EE7AF54703501",
        "latest_app_hash": "C9AEBB441B787D9F1D846DE51F3826F4FD386108B59B08239653ABF59455C3F8",
        "latest_block_height": "1262196",
        "latest_block_time": "2019-08-01T11:52:22.818762194Z",
        "earliest_block_hash": "790BA84C3545FCCC49A5C629CEE6EA58A6E875C3862175BDC11EE7AF54703501",
        "earliest_app_hash": "C9AEBB441B787D9F1D846DE51F3826F4FD386108B59B08239653ABF59455C3F8",
        "earliest_block_height": "1262196",
        "earliest_block_time": "2019-08-01T11:52:22.818762194Z",
        "catching_up": false
      },
      "validator_info": {
        "address": "5D6A51A8E9899C44079C6AF90618BA0369070E6E",
        "pub_key": {
          "type": "tendermint/PubKeyEd25519",
          "value": "A6DoBUypNtUAyEHWtQ9bFjfNg8Bo9CrnkUGl6k6OHN4="
        },
        "voting_power": "0"
      }
    }
  }
  ```


* Response:

  ```shell
  curl -X POST -H "Content-Type:application/json"  -H "Host:heimdalld-node1.default-5ce0a8f9dc0872b.shenzhen.bsnbase.com" http://10.0.51.35:18601/api/613168a8059c79434687ff7903fad416ae6a6d2a/rpc/status
  ```



##### 4.3 block

Get block height.

If the `height` field is set to a non-default value, upon success, the `Cache-Control` header will be set with the default maximum age.

**Parameters**

`height`- height to return. If no height is provided, it will fetch the latest block.

* Example request: 

  ```shell
  // Request
  curl -X POST -H "Content-Type:application/json" http://localhost:26657/block?height=1

  // Result
  {
    "id": 0,
    "jsonrpc": "2.0",
    "result": {
      "node_info": {
        "protocol_version": {
          "p2p": "7",
          "block": "10",
          "app": "0"
        },
        "id": "5576458aef205977e18fd50b274e9b5d9014525a",
        "listen_addr": "tcp:0.0.0.0:26656",
        "network": "cosmoshub-2",
        "version": "0.32.1",
        "channels": "4020212223303800",
        "moniker": "moniker-node",
        "other": {
          "tx_index": "on",
          "rpc_address": "tcp:0.0.0.0:26657"
        }
      },
      "sync_info": {
        "latest_block_hash": "790BA84C3545FCCC49A5C629CEE6EA58A6E875C3862175BDC11EE7AF54703501",
        "latest_app_hash": "C9AEBB441B787D9F1D846DE51F3826F4FD386108B59B08239653ABF59455C3F8",
        "latest_block_height": "1262196",
        "latest_block_time": "2019-08-01T11:52:22.818762194Z",
        "earliest_block_hash": "790BA84C3545FCCC49A5C629CEE6EA58A6E875C3862175BDC11EE7AF54703501",
        "earliest_app_hash": "C9AEBB441B787D9F1D846DE51F3826F4FD386108B59B08239653ABF59455C3F8",
        "earliest_block_height": "1262196",
        "earliest_block_time": "2019-08-01T11:52:22.818762194Z",
        "catching_up": false
      },
      "validator_info": {
        "address": "5D6A51A8E9899C44079C6AF90618BA0369070E6E",
        "pub_key": {
          "type": "tendermint/PubKeyEd25519",
          "value": "A6DoBUypNtUAyEHWtQ9bFjfNg8Bo9CrnkUGl6k6OHN4="
        },
        "voting_power": "0"
      }
    }
  }
  ```


* Response:

  ```shell
  curl -X POST -H "Content-Type:application/json"  -H "Host:heimdalld-node1.default-5ce0a8f9dc0872b.shenzhen.bsnbase.com" http://10.0.51.35:18601/api/613168a8059c79434687ff7903fad416ae6a6d2a/rpc/block?height=1
  ```