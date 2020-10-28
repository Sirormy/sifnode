# ADR 001: CLP integration with Sifnode

## Changelog

- 2020/10/217 Initial version

## Status

*Proposed*

## Context
This ADR contains a summary of decisions taken during the implementation of the clp module and a summary of the final outcome
### Summary

For the Sifchain MVP ,CLP provides a module  

### Pros and Cons

1. Seperate Ledger Solution

Pros: Peggy and Sifnode can develop and extend seperately, totally decoupled. Peggy can be focused on recording cross chain assets transfers with its own validator set, tokenized incentives for maintaining consensus, and its own native token.  This validator set would be dedicated to supporting other Cosmos SDK chains besides Sifchain.

Cons: Peggy and Sifnode would need IBC support, which is not currently used in any production environment yet.  Sifchain users who want to swap or pool with an Ethereum token would need two transactions.  The first would be transferring an asset from Ethereum to Peggy's peg zone.  The second would be transferring the pegged asset from the peg zone to Sifchain via IBC.

2. Shared Ledger Solution

Pros: It is much easier to deploy and maintenence since all operations like cross-chain token transfer, adding liquidity, and swapping tokens would be processed by a single chain.  There would be no dependency on IBC.

Cons: For the long term, the system is hard to scale out. For example, all Sifnode operators would also need to deploy a Ethereum node process Ethereum's high gas fees.  This increases the labor costs of running a Sifnode validator in a way that is unsustainable as Sifchain bridges to more blockchains besides Ethereum.

## Decision
We choose the second solution to implement now. The major reason is the IBC still in development and not mature enough for production usage at this time. We will keep our eyes on the maturity of IBC and make a switch when we judge it is ready.

We will decouple the cross-chain transfer functions (native to Peggy) and liquidity and swap (native to Sifnode) at the module level. This will make it easier for us to update to IBC when needed

## Consequences

### Positive

- We can quickly deliver our MVP

### Negative

- Nothing major

### Neutral

- Nothing major

## References

https://blog.cosmos.network/the-internet-of-blockchains-how-cosmos-does-interoperability-starting-with-the-ethereum-peg-zone-8744d4d2bc3f
