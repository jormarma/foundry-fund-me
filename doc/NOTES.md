# FUND ME

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
