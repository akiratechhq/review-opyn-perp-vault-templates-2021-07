<div id="splash">
    <div id="project">
          <span class="splash-title">
               Project
          </span>
          <br />
          <span id="project-value">
               Project name
          </span>
    </div>
     <div id="details">
          <div id="left">
               <span class="splash-title">
                    Client
               </span>
               <br />
               <span class="details-value">
                    Client name
               </span>
               <br />
               <span class="splash-title">
                    Date
               </span>
               <br />
               <span class="details-value">
                    July 2021
               </span>
          </div>
          <div id="right">
               <span class="splash-title">
                    Reviewers
               </span>
               <br />
               <span class="details-value">
                    Daniel Luca
               </span><br />
               <span class="contact">@cleanunicorn</span>
               <br />
               <span class="details-value">
                    Andrei Simion
               </span><br />
               <span class="contact">@andreiashu</span>
          </div>
    </div>
</div>


## Table of Contents
 - [Details](#details)
 - [Issues Summary](#issues-summary)
 - [Executive summary](#executive-summary)
     - [Week 1](#week-1)
     - [Week 2](#week-2)
 - [Scope](#scope)
 - [Recommendations](#recommendations)
 - [Issues](#issues)
 - [Artifacts](#artifacts)
     - [Surya](#surya)
     - [Coverage](#coverage)
     - [Tests](#tests)
 - [License](#license)


## Details

- **Client** Client name
- **Date** July 2021
- **Lead reviewer** Daniel Luca ([@cleanunicorn](https://twitter.com/cleanunicorn))
- **Reviewers** Daniel Luca ([@cleanunicorn](https://twitter.com/cleanunicorn)), Andrei Simion ([@andreiashu](https://twitter.com/andreiashu))
- **Repository**: [Project name](https://github.com/opynfinance/perp-vault-templates)
- **Commit hash** `1248e6606feb3279a94104df6c6dfcb8d46271f4`
- **Technologies**
  - Solidity
  - Node.JS

## Issues Summary

| SEVERITY       |    OPEN    |    CLOSED    |
|----------------|:----------:|:------------:|
|  Informational  |  0  |  0  |
|  Minor  |  0  |  0  |
|  Medium  |  0  |  0  |
|  Major  |  0  |  0  |

## Executive summary

This report represents the results of the engagement with **Client name** to review **Project name**.

The review was conducted over the course of **2 weeks** from **October 15 to November 15, 2020**. A total of **5 person-days** were spent reviewing the code.

### Week 1

During the first week, we ...

### Week 2

The second week was ...

## Scope

The initial review focused on the [Project name](https://github.com/opynfinance/perp-vault-templates) repository, identified by the commit hash `1248e6606feb3279a94104df6c6dfcb8d46271f4`. ...

<!-- We focused on manually reviewing the codebase, searching for security issues such as, but not limited to, re-entrancy problems, transaction ordering, block timestamp dependency, exception handling, call stack depth limitation, integer overflow/underflow, self-destructible contracts, unsecured balance, use of origin, costly gas patterns, architectural problems, code readability. -->

**Includes:**
- GoodContract.sol

**Excludes:**
- BadContract.sol

## Recommendations

We identified a few possible general improvements that are not security issues during the review, which will bring value to the developers and the community reviewing and using the product.

<!-- ### Increase the number of tests

A good rule of thumb is to have 100% test coverage. This does not guarantee the lack of security problems, but it means that the desired functionality behaves as intended. The negative tests also bring a lot of value because not allowing some actions to happen is also part of the desired behavior.

-->

<!-- ### Set up Continuous Integration

Use one of the platforms that offer Continuous Integration services and implement a list of actions that compile, test, run coverage and create alerts when the pipeline fails.

Because the repository is hosted on GitHub, the most painless way to set up the Continuous Integration is through [GitHub Actions](https://docs.github.com/en/free-pro-team@latest/actions).

Setting up the workflow can start based on this example template.


```yml
name: Continuous Integration

on:
  push:
    branches: [master]
  pull_request:
    branches: [master]

jobs:
  build:
    name: Build and test
    runs-on: ubuntu-latest
    strategy:
      matrix:
        node-version: [12.x]
    steps:
    - uses: actions/checkout@v2
    - name: Use Node.js ${{ matrix.node-version }}
      uses: actions/setup-node@v1
      with:
        node-version: ${{ matrix.node-version }}
    - run: npm ci
    - run: cp ./config.sample.js ./config.js
    - run: npm test

  coverage:
    name: Coverage
    needs: build
    runs-on: ubuntu-latest
    strategy:
      matrix:
        node-version: [12.x]
    steps:
    - uses: actions/checkout@v2
    - name: Use Node.js ${{ matrix.node-version }}
      uses: actions/setup-node@v1
      with:
        node-version: ${{ matrix.node-version }}
    - run: npm ci
    - run: cp ./config.sample.js ./config.js
    - run: npm run coverage
    - uses: actions/upload-artifact@v2
      with:
        name: Coverage ${{ matrix.node-version }}
        path: |
          coverage/
```

This CI template activates on pushes and pull requests on the **master** branch.

```yml
on:
  push:
    branches: [master]
  pull_request:
    branches: [master]
```

It uses an [Ubuntu Docker](https://hub.docker.com/_/ubuntu) image as a base for setting up the project.

```yml
    runs-on: ubuntu-latest
```

Multiple Node.js versions can be used to check integration. However, because this is not primarily a Node.js project, multiple versions don't provide added value.

```yml
    strategy:
      matrix:
        node-version: [12.x]
```

A script item should be added in the `scripts` section of [package.json](./code/package.json) that runs all tests.

```json
{
   "script": {
      "test": "buidler test"
   }
}
```

This can then be called by running `npm test` after setting up the dependencies with `npm ci`.

If any hidden variables need to be defined, you can set them up in a local version of `./config.sample.js` (locally named `./config.js`). If you decide to do that, you should also add `./config.js` in `.gitignore` to make sure no hidden variables are pushed to the public repository. The sample config file `./config.sample.js` should be sufficient to pass the test suite.

```yml
    steps:
    - uses: actions/checkout@v2
    - name: Use Node.js ${{ matrix.node-version }}
      uses: actions/setup-node@v1
      with:
        node-version: ${{ matrix.node-version }}
    - run: npm ci
    - run: cp ./config.sample.js ./config.js
    - run: npm test
```

You can also choose to run coverage and upload the generated artifacts.

```yml
    - run: npm run coverage
    - uses: actions/upload-artifact@v2
      with:
        name: Coverage ${{ matrix.node-version }}
        path: |
          coverage/
```

At the moment, checking the artifacts is not [that](https://github.community/t/browsing-artifacts/16954) [easy](https://github.community/t/need-clarification-on-github-actions/16027/2), because one needs to download the zip archive, unpack it and check it. However, the coverage can be checked in the **Actions** section once it's set up.

-->

<!-- ### Contract size

The contracts are dangerously close to the hard limit defined by [EIP-170](https://eips.ethereum.org/EIPS/eip-170), specifically **24676 bytes**.

Depending on the Solidity compiler version and the optimization runs, the contract size might increase over the hard limit. As stated in [the Solidity documentation](https://solidity.readthedocs.io/en/latest/using-the-compiler.html#using-the-commandline-compiler), increasing the number of optimizer runs increases the contract size.

> If you want the initial contract deployment to be cheaper and the later function executions to be more expensive, set it to `--optimize-runs=1`. If you expect many transactions and do not care for higher deployment cost and output size, set `--optimize-runs` to a high number.

Even if you remove the unused internal functions, it will not reduce the contract size because the Solidity compiler shakes that unused code out of the generated bytecode.

#### DELEGATECALL approach

Another way to improve contract size is by breaking them into multiple smaller contracts, grouped by functionality and using `DELEGATECALL` to execute that code. A standard that defines code splitting and selective code upgrade is the [EIP-2535 Diamond Standard](https://eips.ethereum.org/EIPS/eip-2535), which is an extension of [Transparent Contract Standard](https://github.com/ethereum/EIPs/blob/master/EIPS/eip-1538.md). A detailed explanation, documentation and implementations can be found in the [EIP-2535](https://eips.ethereum.org/EIPS/eip-2535). However, the current EIP is in **Draft** status, which means the interface, implementation, and overall architecture might change. Another thing to keep in mind is that using this pattern increases the gas cost. -->

## Issues


## Artifacts

### Surya

Sūrya is a utility tool for smart contract systems. It provides a number of visual outputs and information about the structure of smart contracts. It also supports querying the function call graph in multiple ways to aid in the manual inspection and control flow analysis of contracts.

**Contracts Description Table**

|  Contract  |         Type        |       Bases      |                  |                 |
|:----------:|:-------------------:|:----------------:|:----------------:|:---------------:|
|     └      |  **Function Name**  |  **Visibility**  |  **Mutability**  |  **Modifiers**  |
||||||
| **OpynPerpVault** | Implementation | ERC20Upgradeable, ReentrancyGuardUpgradeable, OwnableUpgradeable |||
| └ | init | Public ❗️ | 🛑  | initializer |
| └ | setCap | External ❗️ | 🛑  | onlyOwner |
| └ | totalAsset | External ❗️ |   |NO❗️ |
| └ | getSharesByDepositAmount | External ❗️ |   |NO❗️ |
| └ | getWithdrawAmountByShares | External ❗️ |   |NO❗️ |
| └ | deposit | External ❗️ | 🛑  | onlyUnlocked |
| └ | registerDeposit | External ❗️ | 🛑  | onlyLocked |
| └ | claimShares | External ❗️ | 🛑  |NO❗️ |
| └ | withdraw | External ❗️ | 🛑  | nonReentrant onlyUnlocked |
| └ | registerWithdraw | External ❗️ | 🛑  | onlyLocked |
| └ | withdrawFromQueue | External ❗️ | 🛑  | nonReentrant notEmergency |
| └ | closePositions | Public ❗️ | 🛑  | onlyLocked unlockState |
| └ | rollOver | External ❗️ | 🛑  | onlyOwner onlyUnlocked lockState |
| └ | emergencyPause | External ❗️ | 🛑  | onlyOwner |
| └ | resumeFromPause | External ❗️ | 🛑  | onlyOwner |
| └ | _netAssetsControlled | Internal 🔒 |   | |
| └ | _totalAssets | Internal 🔒 |   | |
| └ | _effectiveBalance | Internal 🔒 |   | |
| └ | _totalDebt | Internal 🔒 |   | |
| └ | _deposit | Internal 🔒 | 🛑  | |
| └ | _closeAndWithdraw | Internal 🔒 | 🛑  | |
| └ | _distribute | Internal 🔒 | 🛑  | nonReentrant |
| └ | _withdrawFromQueue | Internal 🔒 | 🛑  | |
| └ | _regularWithdraw | Internal 🔒 | 🛑  | |
| └ | _getSharesByDepositAmount | Internal 🔒 |   | |
| └ | _getWithdrawAmountByShares | Internal 🔒 |   | |
| └ | _payRoundFee | Internal 🔒 | 🛑  | |
| └ | _snapshotShareAndAsset | Internal 🔒 | 🛑  | |

**Legend**

|  Symbol  |  Meaning  |
|:--------:|-----------|
|    🛑    | Function can modify state |
|    💵    | Function is payable |

#### Graphs

<!-- ***Contract***

```text
surya graph Contract.sol | dot -Tpng > ./static/Contract_graph.png
```

![Contract Graph](./static/Contract_graph.png)

```text
surya inheritance Contract.sol | dot -Tpng > ./static/Contract_inheritance.png
```

![Contract Inheritance](./static/Contract_inheritance.png)

```text
Use Solidity Visual Auditor
```

![Contract UML](./static/Contract_uml.png) -->

#### Describe

```text
$ npx surya describe ./contracts/core/OpynPerpVault.sol
 +  OpynPerpVault (ERC20Upgradeable, ReentrancyGuardUpgradeable, OwnableUpgradeable)
    - [Pub] init #
       - modifiers: initializer
    - [Ext] setCap #
       - modifiers: onlyOwner
    - [Ext] totalAsset
    - [Ext] getSharesByDepositAmount
    - [Ext] getWithdrawAmountByShares
    - [Ext] deposit #
       - modifiers: onlyUnlocked
    - [Ext] registerDeposit #
       - modifiers: onlyLocked
    - [Ext] claimShares #
    - [Ext] withdraw #
       - modifiers: nonReentrant,onlyUnlocked
    - [Ext] registerWithdraw #
       - modifiers: onlyLocked
    - [Ext] withdrawFromQueue #
       - modifiers: nonReentrant,notEmergency
    - [Pub] closePositions #
       - modifiers: onlyLocked,unlockState
    - [Ext] rollOver #
       - modifiers: onlyOwner,onlyUnlocked,lockState
    - [Ext] emergencyPause #
       - modifiers: onlyOwner
    - [Ext] resumeFromPause #
       - modifiers: onlyOwner
    - [Int] _netAssetsControlled
    - [Int] _totalAssets
    - [Int] _effectiveBalance
    - [Int] _totalDebt
    - [Int] _deposit #
    - [Int] _closeAndWithdraw #
    - [Int] _distribute #
       - modifiers: nonReentrant
    - [Int] _withdrawFromQueue #
    - [Int] _regularWithdraw #
    - [Int] _getSharesByDepositAmount
    - [Int] _getWithdrawAmountByShares
    - [Int] _payRoundFee #
    - [Int] _snapshotShareAndAsset #


 ($) = payable function
 # = non-constant function

```

### Coverage

```text
$ npm run coverage

> @opynfinance/perp-vault-templates@1.0.0 coverage
> npx hardhat coverage --testfiles 'test/unit-tests/**/*.ts'


Version
=======
> solidity-coverage: v0.7.16

Instrumenting for coverage...
=============================

> core/OpynPerpVault.sol
> example-actions/ShortOToken.sol
> example-actions/ShortPutWithETH.sol
> libraries/SwapTypes.sol
> proxy/CTokenProxy.sol
> proxy/ETHProxy.sol
> utils/AirswapUtils.sol
> utils/AuctionUtils.sol
> utils/CompoundUtils.sol
> utils/GammaUtils.sol
> utils/RollOverBase.sol
> utils/ZeroXUtils.sol

Coverage skipped for:
=====================

> interfaces/IAction.sol
> interfaces/ICEth.sol
> interfaces/IChainlink.sol
> interfaces/IComptroller.sol
> interfaces/IController.sol
> interfaces/ICToken.sol
> interfaces/IEasyAuction.sol
> interfaces/IERC20Detailed.sol
> interfaces/IOracle.sol
> interfaces/IOToken.sol
> interfaces/IOtokenFactory.sol
> interfaces/IPool.sol
> interfaces/IPriceFeed.sol
> interfaces/ISwap.sol
> interfaces/ITreasury.sol
> interfaces/IVault.sol
> interfaces/IWETH.sol
> interfaces/IWhitelist.sol
> interfaces/IZeroXV4.sol
> mocks/MockAction.sol
> mocks/MockCompoundContracts.sol
> mocks/MockController.sol
> mocks/MockEasyAuction.sol
> mocks/MockERC20.sol
> mocks/MockOpynOracle.sol
> mocks/MockOracle.sol
> mocks/MockOToken.sol
> mocks/MockPool.sol
> mocks/MockPricer.sol
> mocks/MockSwap.sol
> mocks/MockWETH.sol
> mocks/MockWhitelist.sol
> mocks/MockZeroXV4.sol
> tests/CompoundUtilTester.sol

Compilation:
============

Compiling 63 files with 0.7.6
contracts/mocks/MockEasyAuction.sol:81:7: Warning: Unnamed return variable can remain unassigned. Add an explicit return with value to all non-reverting code paths or name the variable.
      uint64 /*userId*/
      ^----^

@openzeppelin/contracts-upgradeable/drafts/ERC20PermitUpgradeable.sol:41:43: Warning: Unused function parameter. Remove or comment out the variable name to silence this warning.
    function __ERC20Permit_init_unchained(string memory name) internal initializer {
                                          ^----------------^

contracts/utils/RollOverBase.sol:134:31: Warning: Unused function parameter. Remove or comment out the variable name to silence this warning.
  function _customOTokenCheck(address _nextOToken) internal view virtual {c_0xb65bf4 ...
                              ^-----------------^

contracts/mocks/MockController.sol:75:5: Warning: Unused function parameter. Remove or comment out the variable name to silence this warning.
    address _otoken
    ^-------------^

contracts/mocks/MockEasyAuction.sol:44:57: Warning: Unused function parameter. Remove or comment out the variable name to silence this warning.
  function registerUser(address user) external returns (uint64 userId) {
                                                        ^-----------^

contracts/mocks/MockAction.sol:33:3: Warning: Function state mutability can be restricted to view
  function closePosition() external override {
  ^ (Relevant source part starts here and spans across multiple lines).

contracts/mocks/MockController.sol:74:3: Warning: Function state mutability can be restricted to pure
  function isSettlementAllowed(
  ^ (Relevant source part starts here and spans across multiple lines).

contracts/core/OpynPerpVault.sol:14:1: Warning: Contract code size exceeds 24576 bytes (a limit introduced in Spurious Dragon). This contract may not be deployable on mainnet. Consider enabling the optimizer (with a low "runs" value!), turning off revert strings, or using libraries.
contract OpynPerpVault is ERC20Upgradeable, ReentrancyGuardUpgradeable, OwnableUpgradeable {
^ (Relevant source part starts here and spans across multiple lines).

contracts/example-actions/ShortOToken.sol:28:1: Warning: Contract code size exceeds 24576 bytes (a limit introduced in Spurious Dragon). This contract may not be deployable on mainnet. Consider enabling the optimizer (with a low "runs" value!), turning off revert strings, or using libraries.
contract ShortOToken is IAction, OwnableUpgradeable, AuctionUtils, AirswapUtils, RollOverBase, GammaUtils {
^ (Relevant source part starts here and spans across multiple lines).

Generating typings for: 66 artifacts in dir: typechain for target: ethers-v5
Successfully generated 113 typings!
Compilation finished successfully

Network Info
============
> HardhatEVM: v2.2.1
> network:    hardhat

No need to generate any newer typings.


  ShortAction
    deployment test
      ✓ deploy (466ms)
      ✓ should deploy with type 1 vault (340ms)
    idle phase
      ✓ should revert if calling mint + sell in idle phase
      ✓ should not be able to token with invalid strike price
      ✓ should be able to commit next token
      ✓ should revert if the vault is trying to rollover before min commit period is spent
    activating the action
      ✓ should revert if the vault is trying to rollover from non-vault address
      ✓ should be able to roll over the position
      ✓ should get currentValue as total amount in gamma as
      ✓ should not be able to commit next token
      ✓ should revert if the vault is trying to rollover
      short with AirSwap
        ✓ should not be able to mint and sell if less than min premium
        ✓ should be able to mint and sell in this phase (59ms)
        ✓ should revert when trying to fill wrong order (44ms)
      short by starting an EasyAuction
        ✓ should be able to mint and start an auction phase (57ms)
        ✓ should start another auction with otoken left in the contract
        ✓ can short by participate in a "buy otoken auction" (77ms)
    close position
      ✓ should revert if the vault is trying to close from non-vault address
      ✓ should be able to close the position (43ms)
      ✓ should revert if calling mint in idle phase

  Short Put with ETH Action
    deployment
      ✓ deploy short put action example  (105ms)
    idle phase
      ✓ should revert if calling mint + sell in idle phase
      ✓ should be able to commit next token
      ✓ should revert if the vault is trying to rollover before min commit period is spent
    activating the action
      ✓ should revert if the vault is trying to rollover from non-vault address
      ✓ should be able to roll over the position
      ✓ should execute the trade with borrowed eth (50ms)
      ✓ should not be able to commit next token
      ✓ should revert if the vault is trying to rollover
    close position
      ✓ should revert if the vault is trying to close from non-vault address
      ✓ should be able to close the position (63ms)

  OpynPerpVault Tests
    init
      ✓ should revert when trying to init with duplicated actions (52ms)
      ✓ should init the contract successfully (44ms)
    Round 0, vault unlocked
      ✓ unlocked state checks
      ✓ should be able to deposit ETH and WETH (134ms)
      ✓ should be able to withdraw eth (145ms)
      ✓ should revert when depositing more than the cap (52ms)
      ✓ should revert when trying to register a deposit
      ✓ should revert when trying to register a queue withdraw
      ✓ should revert when calling closePosition
      ✓ should revert if rollover is called with total percentage > 100 (41ms)
      ✓ should revert if rollover is called with total percentage < 100
      ✓ should revert if rollover is called with invalid percentage array
      ✓ should rollover to the next round (56ms)
    Round 0, vault Locked
      ✓ locked state checks
      ✓ should revert when trying to call rollover again
      ✓ should revert when trying to withdraw
      ✓ should revert when trying to deposit
      ✓ should be able to register a withdraw (133ms)
      ✓ should revert when scheduling a deposit more than the cap
      ✓ should be able to increase cap
      ✓ should be able to schedule a deposit with ETH (84ms)
      ✓ should be able to schedule a deposit with WETH (81ms)
      ✓ should revert if trying to get withdraw from queue now
      ✓ should revert if trying to get claim shares now
      ✓ should revert if calling resumeFrom pause when vault is normal
      ✓ should be able to set vault to emergency state (49ms)
      ✓ should be able to close position (105ms)
    Round 1: vault Unlocked
      ✓ unlocked state checks
      ✓ should revert if calling closePositions again
      ✓ should have correct reserved for withdraw
      ✓ should allow anyone can trigger claim shares (38ms)
      ✓ should allow queue withdraw weth (49ms)
      ✓ queue withdraw and normal withdraw should act the same now (54ms)
      ✓ should allow normal deposit (55ms)
      ✓ should be able to rollover again (53ms)
    Round 1: vault Locked
      ✓ should be able to call withdrawQueue
      ✓ should be able to close a non-profitable round (69ms)
      ✓ should be able to withdraw full amount if the round is not profitable

  CompoundUtils
    tester contract with WETH in it
      ✓ deploy tester and supply it with some WETH (46ms)
      ✓ can supply WETH
      ✓ can borrow USDC
      ✓ can repay USDC
      ✓ can redeem WETH
    tester contract with USDC in it
      ✓ deploy another tester and supply it with some USDC (45ms)
      ✓ can supply USDC
      ✓ can borrow WETH
      ✓ can repay WETH
      ✓ can redeem USDC


  79 passing (5s)

----------------------|----------|----------|----------|----------|----------------|
File                  |  % Stmts | % Branch |  % Funcs |  % Lines |Uncovered Lines |
----------------------|----------|----------|----------|----------|----------------|
 core/                |      100 |    90.63 |      100 |      100 |                |
  OpynPerpVault.sol   |      100 |    90.63 |      100 |      100 |                |
 example-actions/     |    92.31 |    68.42 |    95.24 |    92.47 |                |
  ShortOToken.sol     |    94.23 |    71.43 |      100 |    94.34 |    238,249,281 |
  ShortPutWithETH.sol |    89.74 |       60 |     87.5 |       90 |117,118,142,206 |
 libraries/           |      100 |      100 |      100 |      100 |                |
  SwapTypes.sol       |      100 |      100 |      100 |      100 |                |
 proxy/               |    41.67 |       50 |       50 |    43.24 |                |
  CTokenProxy.sol     |        0 |      100 |        0 |        0 |... 72,74,76,77 |
  ETHProxy.sol        |      100 |       50 |      100 |      100 |                |
 utils/               |    91.21 |       70 |    86.67 |     91.3 |                |
  AirswapUtils.sol    |      100 |      100 |      100 |      100 |                |
  AuctionUtils.sol    |      100 |       75 |      100 |      100 |                |
  CompoundUtils.sol   |      100 |       50 |      100 |      100 |                |
  GammaUtils.sol      |    82.35 |      100 |       80 |    82.35 |    102,104,114 |
  RollOverBase.sol    |      100 |       90 |      100 |      100 |                |
  ZeroXUtils.sol      |        0 |      100 |        0 |        0 | 17,25,26,34,35 |
----------------------|----------|----------|----------|----------|----------------|
All files             |    89.57 |       75 |    90.22 |    89.74 |                |
----------------------|----------|----------|----------|----------|----------------|

> Istanbul reports written to ./coverage/ and ./coverage.json
```

### Tests

```text
$ npm run test

> @opynfinance/perp-vault-templates@1.0.0 test
> FORK=false hardhat test --network hardhat ./test/unit-tests/**/*.ts

No need to generate any newer typings.


  ShortAction
    deployment test
      ✓ deploy (228ms)
      ✓ should deploy with type 1 vault (111ms)
    idle phase
      ✓ should revert if calling mint + sell in idle phase
      ✓ should not be able to token with invalid strike price
      ✓ should be able to commit next token
      ✓ should revert if the vault is trying to rollover before min commit period is spent
    activating the action
      ✓ should revert if the vault is trying to rollover from non-vault address
      ✓ should be able to roll over the position
      ✓ should get currentValue as total amount in gamma as
      ✓ should not be able to commit next token
      ✓ should revert if the vault is trying to rollover
      short with AirSwap
        ✓ should not be able to mint and sell if less than min premium
        ✓ should be able to mint and sell in this phase (43ms)
        ✓ should revert when trying to fill wrong order
      short by starting an EasyAuction
        ✓ should be able to mint and start an auction phase (56ms)
        ✓ should start another auction with otoken left in the contract
        ✓ can short by participate in a "buy otoken auction" (66ms)
    close position
      ✓ should revert if the vault is trying to close from non-vault address
      ✓ should be able to close the position
      ✓ should revert if calling mint in idle phase

  Short Put with ETH Action
    deployment
      ✓ deploy short put action example  (85ms)
    idle phase
      ✓ should revert if calling mint + sell in idle phase
      ✓ should be able to commit next token
      ✓ should revert if the vault is trying to rollover before min commit period is spent
    activating the action
      ✓ should revert if the vault is trying to rollover from non-vault address
      ✓ should be able to roll over the position
      ✓ should execute the trade with borrowed eth (40ms)
      ✓ should not be able to commit next token
      ✓ should revert if the vault is trying to rollover
    close position
      ✓ should revert if the vault is trying to close from non-vault address
      ✓ should be able to close the position (43ms)

  OpynPerpVault Tests
    init
      ✓ should revert when trying to init with duplicated actions
      ✓ should init the contract successfully
    Round 0, vault unlocked
      ✓ unlocked state checks
      ✓ should be able to deposit ETH and WETH (96ms)
      ✓ should be able to withdraw eth (104ms)
      ✓ should revert when depositing more than the cap (40ms)
      ✓ should revert when trying to register a deposit
      ✓ should revert when trying to register a queue withdraw
      ✓ should revert when calling closePosition
      ✓ should revert if rollover is called with total percentage > 100
      ✓ should revert if rollover is called with total percentage < 100
      ✓ should revert if rollover is called with invalid percentage array
      ✓ should rollover to the next round (52ms)
    Round 0, vault Locked
      ✓ locked state checks
      ✓ should revert when trying to call rollover again
      ✓ should revert when trying to withdraw
      ✓ should revert when trying to deposit
      ✓ should be able to register a withdraw (77ms)
      ✓ should revert when scheduling a deposit more than the cap
      ✓ should be able to increase cap
      ✓ should be able to schedule a deposit with ETH (60ms)
      ✓ should be able to schedule a deposit with WETH (66ms)
      ✓ should revert if trying to get withdraw from queue now
      ✓ should revert if trying to get claim shares now
      ✓ should revert if calling resumeFrom pause when vault is normal
      ✓ should be able to set vault to emergency state (41ms)
      ✓ should be able to close position (83ms)
    Round 1: vault Unlocked
      ✓ unlocked state checks
      ✓ should revert if calling closePositions again
      ✓ should have correct reserved for withdraw
      ✓ should allow anyone can trigger claim shares
      ✓ should allow queue withdraw weth
      ✓ queue withdraw and normal withdraw should act the same now (42ms)
      ✓ should allow normal deposit (40ms)
      ✓ should be able to rollover again (46ms)
    Round 1: vault Locked
      ✓ should be able to call withdrawQueue
      ✓ should be able to close a non-profitable round (60ms)
      ✓ should be able to withdraw full amount if the round is not profitable

  CompoundUtils
    tester contract with WETH in it
      ✓ deploy tester and supply it with some WETH (45ms)
      ✓ can supply WETH
      ✓ can borrow USDC
      ✓ can repay USDC
      ✓ can redeem WETH
    tester contract with USDC in it
      ✓ deploy another tester and supply it with some USDC (40ms)
      ✓ can supply USDC
      ✓ can borrow WETH
      ✓ can repay WETH
      ✓ can redeem USDC


  79 passing (5s)
```

## License

This report falls under the terms described in the included [LICENSE](./LICENSE).

<!-- Load highlight.js -->
<link rel="stylesheet"
href="//cdnjs.cloudflare.com/ajax/libs/highlight.js/10.4.1/styles/default.min.css">
<script src="//cdnjs.cloudflare.com/ajax/libs/highlight.js/10.4.1/highlight.min.js"></script>
<script>hljs.initHighlightingOnLoad();</script>
<script type="text/javascript" src="https://cdn.jsdelivr.net/npm/highlightjs-solidity@1.0.20/solidity.min.js"></script>
<script type="text/javascript">
    hljs.registerLanguage('solidity', window.hljsDefineSolidity);
    hljs.initHighlightingOnLoad();
</script>
<link rel="stylesheet" href="./style/print.css"/>
