# FUND ME <!-- omit in toc -->

- [01 Add the contracts](#01-add-the-contracts)
- [02 Install Chainlink dependencies](#02-install-chainlink-dependencies)
- [03 Rename errors](#03-rename-errors)
- [04 Add Testing to test the FundMe contract](#04-add-testing-to-test-the-fundme-contract)
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
