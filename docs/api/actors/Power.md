---
title: "Storage Power Actor"
sidebar_position: 6
---

# Storage Power Actor

Strorage power actor is responsible for keeping track of the storage power allocated at each storage miner.

The ActorCode for storage power built-in actor is `hex"0004"` which will be used to call methods in storage power actor. You also need to specify method number of which method you want to invoke. Please refer the each method for its method number.

### CreateMiner

```go
func CreateMiner(params CreateMinerParams, uint256 value) CreateMinerReturn {}
```

Create a new miner for the owner address and worker address.

`uint` CreateMinerMethodNum = 1173380165.

**Params**:

+ `struct` CreateMinerParams
  + `bytes` Owner - the address of the owner.
  + `bytes` Worker - the address of the worker.
  + `RegisteredPoStProof` WindowPoStProofType - the type of RegisteredPoStProof.
  + `bytes` Peer - peerID.
  + `bytes[]` Multiaddrs - the multi-address which is used to control new created miner.
+ `uint256` value - the amount of token the new miner will receive

**Results**:

+ CreateMinerReturn

  + `bytes` IDAddress - The canonical ID-based address for the actor.

  + `byte`: RobustAddress -A more expensive but re-org-safe address for the newly created actor.


### NetworkRawPower

```go
func NetworkRawPower() NetworkRawPowerReturn {}
```

Return the total raw power of the network.

`uint`  NetworkRawPowerMethodNum = 931722534.

**Params**:

+ null

**Results**:

+ `int256`  NetworkRawPowerReturn - the raw storage power of the whole network.


### MinerRawPower

```go
func MinerRawPower(params MinerRawPowerParams) MinerRawPowerParams {}
```

Return the raw power claimed by the specified miner, and whether the miner has more than the consensus minimum amount of storage active.

`uint` MinerRawPowerMethodNum = 3753401894.

**Params**:

+ MinerRawPowerParams
  + `uint64` Miner - Miner ID

**Results**:

+ `struct` MinerRawPowerParams
+ `int256` RawBytePower - the row power of the miner.
  
+ `bool` MeetsConsensusMinimum - if the miner power meets the minimum for consensus.


### MinerCount

```go
func MinerCount() MinerCountReturn {}
```

Returns the total number of miners created, regardless of whether or not they have any pledged storage.

`uint` MinerRawPowerMethodNum = 3753401894.

**Params**:

+ null

**Results**:

+ `uint64` MinerCountReturn - the count of the miners that the caller address has.


### MinerConsensusCount

```go
func MinerConsensusCount() MinerConsensusCountReturn {}
```

Returns the total number of miners that have more than the consensus minimum amount of storage active.

`uint`  MinerConsensusCountMethodNum = 196739875.

**Params**:

+ null

**Results**:

+ `uint64`MinerConsensusCountReturn - the count of the miners meet the consensus minimum that the caller address has.

