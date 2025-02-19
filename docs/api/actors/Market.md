---
title: "Storage Market Actor"
sidebar_position: 3
---

# Storage Market Actor

Storage market actor is responsible for managing storage and retrieval deals. 

The ActorCode for storage market actor is `hex"0005"` which will be used to call this actor. You also need to specify method number of which method you want to invoke. Please refer the each method for its method number.

### AddBalance

```go
func AddBalance(address Address, uint256 value) EmptyValue {}
```

Deposit the received FIL token, which is received along with this message,  into the balance held in escrow address of the provider or client address.

`uint`  AddBalanceMethodNum = 822473126.

**Params**:

+ `bytes` Address - the address of provider or client.
+ `uint256` value - the amount of FIL token you want to deposit into the balance 

**Results**:

+ `struct` EmptyValue.

### GetBalance

```go
func GetBalance(address Address) GetBalanceReturn {}
```

Return the escrow balance and locked amount for an address.

`uint` GetBalanceMethodNum = 726108461.

**Params**:

+ `bytes` address - the wallet address to request balance.

**Results**:

+ `struct` GetBalanceReturn
  + `int256` Balance - the escrow balance for this address.
  + `int256` Locked - the escrow locked amount for this address.

### WithdrawBalance

```go
func WithdrawBalance(params WithdrawBalanceParams) WithdrawBalanceReturn {}
```

Withdraw the specified amount from the balance held in escrow.

`uint`  WithdrawBalanceMethodNum = 2280458852.

**Params**:

+ `struct` WithdrawBalanceParams
  + `bytes` ProviderOrClientAddress - the address of provider or client.
  + `int256` TokenAmount - the token amount to withdraw.


**Results**:

+ `struct` WithdrawBalanceReturn
  + `int256` AmountWithdraw - the token amount withdrawn.


### PublishStorageDeals

```go
func PublishStorageDeals(params PublishStorageDealsParams) PublishStorageDealsReturn {}
```

Publish a new set of storage deals which are not yet included in a sector.

`uint` PublishStorageDealsMethodNum = 2236929350.

**Params**:

+ `struct` PublishStorageDealsParams
  + `struct ClientDealProposal[]` Deals - list of deal proposals signed by a client
    + `struct DealProposal` Proposal 
      + `bytes` PieceCID.
      + `uint64` PieceSize - the size of the piece.
      + `bool` VerifiedDeal - if the deal is verified or not.
      + `bytes` Client - the address of the storage client.
      + `bytes` Provider - the address of the storage provider.
      + `string` Label - any label that client choose for the deal.
      + `int64` StartEpoch - the chain epoch to start the deal.
      + `int64` EndEpoch - the chain epoch to end the deal.
      +  `int256` StoragePricePerEpoch -  the token amount to pay to provider per epoch.
      + `int256` ProviderCollateral - the token amount as collateral paid by the provider.
      + `int256` ClientCollateral - the token amount as collateral paid by the client.

    + `bytes` ClientSignature - the signature signed by the client.


**Results**:

+ `struct` PublishStorageDealsReturn
  + `uint64[]` IDs - returned storage deal IDs.
  + `bytes` ValidDeals - represent all the valid deals.

### GetDealDataCommitment

```go
func GetDealDataCommitment(params GetDealDataCommitmentParams) GetDealDataCommitmentReturn {}
```

Return the data commitment and size of a deal proposal.

`uint` GetDealDataCommitmentMethodNum = 1157985802.

**Params**:

+ `uint64` GetDealDataCommitmentParams - Deal ID.

**Results**:

+ `struct` GetDealDataCommitmentReturn
  + `bytes` Data - the data commitment of this deal.
  + `uint64` Size  - the size of this deal.


### GetDealClient

```go
func GetDealClient(params GetDealClientParams) GetDealClientReturn {}
```

Return the client of the deal proposal.

`uint` GetDealClientMethodNum = 128053329.

**Params**:

+ `uint64` GetDealClientParams - CID of the deal proposal.

**Results**:

+ `bytes` GetDealClientReturn - the wallet address of the client.

### GetDealProvider

```go
func GetDealProvider(params GetDealProviderParams) GetDealProviderReturn {}
```

Return the provider of a deal proposal.

`uint` GetDealProviderMethodNum = 935081690.

**Params**:

+ `uint64` GetDealProviderParams - CID of the deal proposal.

**Results**:

+ `bytes` GetDealProviderReturn - the wallet address of the provider.

### GetDealLabel

```go
func GetDealLabel(params GetDealLabelParams) GetDealLabelReturn {}
```

Return the label of a deal proposal.

`uint` GetDealLabelMethodNum = 46363526.

**Params**:

+ `uint64` GetDealLabelParams - CID of the deal proposal.

**Results**:

+ `string` GetDealLabelReturn - the label of this deal.

### GetDealTerm

```go
func GetDealTerm(params GetDealTermParams) GetDealTermReturn {}
```

Return the start epoch and duration(in epochs) of a deal proposal. 

`uint` GetDealTermMethodNum = 163777312.

**Params**:

+ `uint64` GetDealTermParams - CID of the deal proposal.

**Results**:

+ `struct`GetDealTermReturn
  + `int64` Start - the chain epoch to start the deal.
  + `int64` End - the chain epoch to end the deal.


### GetDealTotalPrice

```
func GetDealTotalPrice(params GetDealTotalPriceParams) GetDealTotalPriceReturn {}
```

Return the total price that will be paid from the client to the provider for this deal.

`uint` GetDealEpochPriceMethodNum = 4287162428.

**Params**:

+ `uint64` GetDealTotalPriceParams - CID of the deal proposal.

**Results**:

+ `int256 ` GetDealTotalPriceReturn - the token amount that will be paid by client to provider.

### GetDealClientCollateral

```
func GetDealClientCollateral(params GetDealClientCollateralParams) GetDealClientCollateralReturn {}
```

Return the client collateral requirement for a deal proposal.

`uint` GetDealClientCollateralMethodNum = 200567895.

**Params**:

+ `uint64` GetDealClientCollateralParams - CID of the deal proposal.

**Results**:

+ `int256` GetDealClientCollateralReturn - the token amount as collateral paid by the client.

### GetDealProviderCollateral

```
func GetDealProviderCollateral(params GetDealProviderCollateralParams) GetDealProviderCollateralReturn {}
```

Return the provide collateral requirement for a deal proposal.

`uint`  GetDealProviderCollateralMethodNum = 2986712137.

**Params**:

+ `uint64` GetDealProviderCollateralParams - CID of the deal proposal.

**Results**:

+ `int256` GetDealProviderCollateralReturn - the token amount as collateral paid by the provider.

### GetDealVerified

```
func GetDealVerified(params GetDealVerifiedParams) GetDealVerifiedReturn {}
```

Return the verified flag for a deal proposal.

`uint` GetDealVerifiedMethodNum = 2627389465.

**Params**:

+ `uint64` GetDealVerifiedParams - CID of the deal proposal.

**Results**:

+ `bool` GetDealVerifiedReturn -  if the deal is verified or not.

### GetDealActivation

```
func GetDealActivation(params GetDealActivationParams) GetDealActivationReturn {}
```

Return the activation state for a deal.

`uint` GetDealActivationParams = 2567238399.

**Params**:

+ `uint64` GetDealVerifiedParams - CID of the deal proposal.

**Results**:

+ `struct` GetDealActivationReturn
  + `int64` Activated - Epoch at which the deal was activated, or -1.
  + `int64` Terminated -Epoch at which the deal was terminated abnormally, or -1.
