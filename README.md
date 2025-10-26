# FUND ME <!-- omit in toc -->

- [01 Add the contracts](#01-add-the-contracts)
- [02 Install Chainlink dependencies](#02-install-chainlink-dependencies)
- [03 Rename errors](#03-rename-errors)
- [04 Add Testing to test the FundMe contract](#04-add-testing-to-test-the-fundme-contract)
- [05 Add more tests and debug](#05-add-more-tests-and-debug)
- [06 Advanced deployment scripts](#06-advanced-deployment-scripts)
- [Appendix: Foundry](#appendix-foundry)
  - [Documentation](#documentation)
  - [Usage](#usage)
    - [Build](#build)
    - [Test](#test)
    - [Format](#format)
    - [Gas Snapshots](#gas-snapshots)
    - [Anvil](#anvil)
    - [Deploy](#deploy)
    - [Cast](#cast)
    - [Help](#help)

Create the project

```sh
forge init fund-me
```

## 01 Add the contracts

1. Remove all the *.sol files under `script/`, `src/` and `test/`.
2. Copy the following files to the `src/` folder:
   - [FundMe.sol](https://github.com/Cyfrin/remix-fund-me-cu/blob/main/FundMe.sol)
   - [PriceConverter.sol](https://github.com/Cyfrin/remix-fund-me-cu/blob/main/PriceConverter.sol)
3. Check that it does not compile:
   - `forge build` errors because there are libs not present in the project.

## 02 Install Chainlink dependencies

1. Import the necessary library directly from github:
   - `forge install smartcontractkit/chainlink-brownie-contracts`. No need for `--no-commit` flag, as it seems to be active by default, and now the flag that is available is the `--commit` for just the contrary.
2. Tell foundry that `@chainlink/` need to point to `lib/chainlink-brownie-contracts/`, ([chainlink-brownie-contracts](https://github.com/smartcontractkit/chainlink-brownie-contracts))

> NOTE: now `forge build` succeeds with 1 warning and 2 notes.

## 03 Rename errors

It is a best practice to name your errors with the name of the contract and two underscores.

Example:

- Contract name: `FundMe`
- Error name: `NotOwner`
- New error name: `FundMe__NotOwner`

## 04 Add Testing to test the FundMe contract

1. Create `test/FundMeTest.t.sol`. It is best practice to end test files with `.t.sol` suffix to indicate it is a test file.
2. The test is a contract that extends the `Test` abstract contract from `forge-std/Test.sol`.
3. Add a contract called `FundMeTest` that extends `Test`
   - Create a `FundMe fundMe` storage variable inside the testing contract.
   - Add a `setUp() external` function. This executes before every test. It deploys the `FundMe` contract in a test environment only for this test.
   Inside, deploy the `FundMe` contract.
   - Add a `testFundMeMinimumDollarIsFive() public view` function testing that the contract only receives funds with a minimum `USD` value of `5`.
4. Test the function executing `forge test`
5. You can add more verbosity to the test, for example to see logs with `console.log`, using `forge test -v` or `forge test -vv` up to `-vvvvv`.

## 05 Add more tests and debug

1. Add a new test to check that the owner is the sender.

    ```solidity
    function testOwnerIsMsgSender() public view {
        assertEq(fundMe.i_owner(), msg.sender);
    }
    ```

2. Executing the test it fails. We add more logs to see why.

    ```solidity
    function testOwnerIsMsgSender() public view {
        console.log(fundMe.i_owner());
        console.log(msg.sender);
        assertEq(fundMe.i_owner(), msg.sender);
    }
    ```

3. Executing the tests with `-vv` we see that indeed, the addresses are different.
Technically, the contract creating the `FundMe` contract is the `FundMeTest` contract, not us.

    ```solidity
    function testOwnerIsMsgSender() public view {
        assertEq(fundMe.i_owner(), address(this));
    }
    ```

## 06 Advanced deployment scripts

1. Create a deploy script called `DeployFundMe.s.sol`
2. Write the following code in it:

    ```solidity
    // SPDX-License-Identifier: MIT
    pragma solidity ^0.8.18;

    import {Script} from "forge-std/Script.sol";
    import {FundMe} from "../src/FundMe.sol";

    contract DeployFundMe is Script {
        function run() external {
            vm.startBroadcast();
            new FundMe();
            vm.stopBroadcast();
        }
    }
    ```

3. Test that you can deploy `FundMe` using `forge script script/DeployFundMe.s.sol`.

## Appendix: Foundry

**Foundry is a blazing fast, portable and modular toolkit for Ethereum application development written in Rust.**

Foundry consists of:

- **Forge**: Ethereum testing framework (like Truffle, Hardhat and DappTools).
- **Cast**: Swiss army knife for interacting with EVM smart contracts, sending transactions and getting chain data.
- **Anvil**: Local Ethereum node, akin to Ganache, Hardhat Network.
- **Chisel**: Fast, utilitarian, and verbose solidity REPL.

### Documentation

[https://book.getfoundry.sh/](https://book.getfoundry.sh/)

### Usage

#### Build

```shell
forge build
```

#### Test

```shell
forge test
```

#### Format

```shell
forge fmt
```

#### Gas Snapshots

```shell
forge snapshot
```

#### Anvil

```shell
anvil
```

#### Deploy

```shell
forge script script/Counter.s.sol:CounterScript --rpc-url <your_rpc_url> --private-key <your_private_key>
```

#### Cast

```shell
cast <subcommand>
```

#### Help

```shell
forge --help
anvil --help
cast --help
```
