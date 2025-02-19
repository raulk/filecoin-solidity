---
title: "Multisig Actor"
sidebar_position: 5
---

# Multisig Actor

Multisig built-in actor is responsible for dealing with operations involving the Filecoin wallet.

To interact with specific multi-signature wallet address, you need to use this wallet address to invoke the methods in multisig built-in actor. You also need to specify method number of which method you want to invoke. Please refer the each method for its method number.

### Propose

```go
func Propose(params ProposeParams) ProposeReturn {...}
```

Propose a token transfer transaction for signers to approve, the proposer automatically approves this transaction. 

`uint` ProposeMethodNum = 1696838335.

**Params**:

+ `struct` ProposeParams
  + `bytes` ToAddress - the address to receive the token.
  + `int256` Value - the token amount to be transferred.
  + `uint64` Method: ?
  + `bytep[]` Params: ?

**Results**:

+ `struct` ProposeReturn
  + `int64` TxnID - the ID of the proposed transaction.
  + `bool` Applied - if the transaction was applied as proposed or not?
  + `uint31` Code - the exit code of the transaction, if Applied is false this field should be ignored.
  + `bytes` Ret - the return value of the transaction, if Applied is false this field should be ignored.


### Approve

```go
func Approve(params TxnIDParams) ApproveReturn {}
```

Other signers of the multi-signature address can use this method to approve the proposed messages. 

`uint` ApproveMethodNum = 1289044053.

**Params**:

+ `struct` TxnIDParams
  + `int64` ID - the signed message ID.
  + `bytes` ProposalHash - Hash of proposal to ensure an operation can only apply to a specific proposal.


**Results**:

+ `struct` ApproveReturn
  + `bool` Applied - if the transaction was applied as proposed or not?
  + `uint31` Code - the exit code of the transaction, if Applied is false this field should be ignored.
  + `bytes` Ret - the return value of the transaction, if Applied is false this field should be ignored.


### Cancel

```go
func Cancel(param TxnIDParams) EmptyValue {}
```

Multi-signature wallet signer to cancel a pending multi-signatures transaction.

`uint` CancelMethodNum = 3365893656.

**Params**:

+ `struct` TxnIDParams
  + `int64` ID - the signed message ID.
  + `bytes` ProposalHash - Hash of proposal to ensure an operation can only apply to a specific proposal.

**Results**:

+ `struct` EmptyValue.

### AddSigner

```go
func AddSigner(params AddSignerParams) EmptyValue {}
```

Add a signer to the multi-signature wallet.

`uint` AddSignerMethodNum = 3028530033.

**Params**:

+ `struct` AddSignerParams
  + `bytes` Signer - the new signer address.
  + `bool` Increase - increase threshold or not.


**Results**:

+ `struct` EmptyValue.

### RemoveSigner

```go
func RemoveSigner(params RemoveSignerParams) EmptyValue {}
```

Remove a signer from the multi-signature wallet.

`uint` RemoveSignerMethodNum = 21182899.

**Params**:

+ `struct` RemoveSignerParams
  + `bytes` Signer - the signer address to be removed.
  + `bool` Decrease - decrease threshold or not. Only able to decrease when threshold is larger than 2.

**Results**:

+ `struct` EmptyValue.

### SwapSigner

```go
func SwapSigner(params SwapSignerParams) EmptyValue {}
```

Swap signers for the multi-signature wallet.

`uint` SwapSignerMethodNum = 3968117037;

**Params**:

+ `struct` SwapSignerParams
  + `bytes` From - the signer address should will be removed from multi-signature wallet.
  + `bytes` To - the signer address should will be added to multi-signature wallet.


**Results**:

+ `struct` EmptyValue.

### ChangeNumApprovalsThreshold

```go
func ChangeNumApprovalsThreshold(params ChangeNumApprovalsThresholdParams) EmptyValue {}
```

Change the threshold number required for the approvals for the multi-signature wallet.

`uint` ChangeNumApprovalsThresholdMethodNum = 3375931653.

**Params**:

+ `struct` ChangeNumApprovalsThresholdParams
  + `unit64` NewThreshold - the new threshold number.


**Results**:

+ `struct` EmptyValue.

### LockBalance

```go
func LockBalance(params LockBalanceParams) EmptyValue {}
```

Lock the amount of token from multi-signature wallet from start epoch to unlock epoch.

`uint` LockBalanceMethodNum = 1999470977.

**Params**:

+ `struct` LockBalanceParams
  + `int64` StartEpoch - the epoch to start locking the balance.
  + `int64` UnlockDuration - the epoch to unlock the balance.
  + `int256` Amount - the amount of token to be locked.


**Results**:

+ `struct` EmptyValue.
