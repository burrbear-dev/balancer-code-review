# Rate Provider: `DolomiteRateProvider`

## Details
- Reviewed by: @schystz
- Checked by: 
- Deployed at:
    - WBERA [berachain:0xB48ea374a649F9Ab8d2Da4534b5EAE4c48773C98](https://berascan.com/address/0xB48ea374a649F9Ab8d2Da4534b5EAE4c48773C98)
- Audit report(s):
    - None

## Context
The ERC4626 RateProvider fetches the rate of ERC4626 vault tokens in terms of the underlying asset.

## Review Checklist: Bare Minimum Compatibility
Each of the items below represents an absolute requirement for the Rate Provider. If any of these is unchecked, the Rate Provider is unfit to use.

- [x] Implements the [`IRateProvider`](https://github.com/balancer/balancer-v2-monorepo/blob/bc3b3fee6e13e01d2efe610ed8118fdb74dfc1f2/pkg/interfaces/contracts/pool-utils/IRateProvider.sol) interface.
- [x] `getRate` returns an 18-decimal fixed point number (i.e., 1 == 1e18) regardless of underlying token decimals.

## Review Checklist: Common Findings
Each of the items below represents a common red flag found in Rate Provider contracts.

If none of these is checked, then this might be a pretty great Rate Provider! If any of these is checked, we must thoroughly elaborate on the conditions that lead to the potential issue. Decision points are not binary; a Rate Provider can be safe despite these boxes being checked. A check simply indicates that thorough vetting is required in a specific area, and this vetting should be used to inform a holistic analysis of the Rate Provider.

### Administrative Privileges
- [ ] The Rate Provider is upgradeable (e.g., via a proxy architecture or an `onlyOwner` function that updates the price source address).

- [x] Some other portion of the price pipeline is upgradeable (e.g., the token itself, an oracle, or some piece of a larger system that tracks the price).
    - WBERA [berachain:0xB48ea374a649F9Ab8d2Da4534b5EAE4c48773C98](https://berascan.com/address/0xB48ea374a649F9Ab8d2Da4534b5EAE4c48773C98)
        - upgradeable component: `DolomiteERC4626WithPayable` ([berachain:0xAa97D791Afc02AF30cf0B046172bb05b3c306517](https://berascan.com/address/0xAa97D791Afc02AF30cf0B046172bb05b3c306517#readProxyContract))
        - **@TODO: check other possible upgradeable components (use `statATokenv2RateProvider.md` as reference)**

### Oracles
- [ ] Price data is provided by an off-chain source (e.g., a Chainlink oracle, a multisig, or a network of nodes).

- [ ] Price data is expected to be volatile (e.g., because it represents an open market price instead of a (mostly) monotonically increasing price).


### Common Manipulation Vectors
- [ ] The Rate Provider is susceptible to donation attacks.

## Conclusion
**Summary judgment: @TODO**

[Draft] The Rate Providers should work well with Balancer pools. The underlying contracts have been audited and been in production for an extended period of time. The upgradeability of the underlying Dolomite protocol is guarded behind decentralized governance and has a minimum execution delay of 24 hours. 
