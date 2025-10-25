# FUND ME

## 01 Create the project

```sh
forge init fund-me
```

## 02 Add the contracts

1. Remove all the *.sol files under `script/`, `src/` and `test/`.
2. Copy the following files to the `src/` folder:
   - [FundMe.sol](https://github.com/Cyfrin/remix-fund-me-cu/blob/main/FundMe.sol)
   - [PriceConverter.sol](https://github.com/Cyfrin/remix-fund-me-cu/blob/main/PriceConverter.sol)
3. Check that it does not compile:
   1. `forge build` errors because there are libs not present in the project.
