# FUND ME <!-- omit in toc -->

- [Create the project](#create-the-project)
- [Add the contracts](#add-the-contracts)
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

## Create the project

```sh
forge init fund-me
```

## Add the contracts

1. Remove all the *.sol files under `script/`, `src/` and `test/`.
2. Copy the following files to the `src/` folder:
   - [FundMe.sol](https://github.com/Cyfrin/remix-fund-me-cu/blob/main/FundMe.sol)
   - [PriceConverter.sol](https://github.com/Cyfrin/remix-fund-me-cu/blob/main/PriceConverter.sol)
3. Check that it does not compile:
   1. `forge build` errors because there are libs not present in the project.

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
