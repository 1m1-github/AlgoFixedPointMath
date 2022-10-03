# AlgoFixedPointMath
high precision fixed point mathematical functions for Algorand smart contracts as an API

## alternative
a better alternative to this project is to implement fixed point math as opcodes in the AVM by interpreting byte[] as fixed point values ~ see the discussion here: https://discord.com/channels/491256308461207573/806903824265904149/1025438663426977853

## $log$, $exp$, $pow$ for fixed point values with upto $36^*$ decimal precision exposed via ABI

the functions would be approximated using their Taylor expansions

the implementation will follow the below linked Solidity implementations by balancer ~ it is open license, the code has been in use for sometime by a well sized community and it is v2

the code below results in 18 decimal precision and works with 256bit intermediary precision ~ we would start by copying that implementation and as a next step, we could update to use 512bit intermediary values resulting in 36bit result precision

arithmetic with 256bit `int` in `AVM` will be implemented using `b*` and `b/` (https://developer.algorand.org/docs/get-details/dapps/avm/teal/opcodes/#b_2)

this SC (smart contract) will expose $log$, $exp$, $pow$ and other mathematical functions via the currently suggested Algorand ABI (https://developer.algorand.org/docs/get-details/dapps/smart-contracts/ABI)

## existing Solidity code to be copied

- log, exp: https://github.com/balancer-labs/balancer-v2-monorepo/blob/592b0534f782b9bfb668990f7821e041a9b775d4/pkg/solidity-utils/contracts/math/LogExpMath.sol
- pow: https://github.com/balancer-labs/balancer-v2-monorepo/blob/592b0534f782b9bfb668990f7821e041a9b775d4/pkg/solidity-utils/contracts/math/FixedPoint.sol
- mult, div: https://github.com/balancer-labs/balancer-v2-monorepo/blob/592b0534f782b9bfb668990f7821e041a9b775d4/pkg/solidity-utils/contracts/math/Math.sol
- swap (_calcOutGivenIn): https://github.com/balancer-labs/balancer-v2-monorepo/blob/592b0534f782b9bfb668990f7821e041a9b775d4/pkg/pool-weighted/contracts/WeightedMath.sol

## use cases
DeFi often needs these functions ~ any other mathematical, scientific dApps might also need these basic functions

## notes

* the Solidity implementation speaks of 18 decimal precision using 256bit values ~ Algorand currently allows 512bit values ~ we are assuming, for now, that doubling the precision of the intermediary values will double the precision of the result ~ to be calculated ~ the 512bit max was given by an Algorand internal dev and remains to be confirmed; dev is highly capable
