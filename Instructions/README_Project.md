# Unit 20 - "Looks like we've made our First Contract!"

![contract](https://github.com/TaylorTucker/Solidity/blob/main/Instructions/Images/smartContract.PNG?raw=true)

## Background

Your new startup has created its own Ethereum-compatible blockchain to help connect financial institutions, and the team wants to build smart contracts to automate some company finances to make everyone's lives easier, increase transparency, and to make accounting and auditing practically automatic!

I created 1 `ProfitSplitter` contract. This contract will:

* Pay your Associate-level employees quickly and easily.


## Files

* [`AssociateProfitSplitter.sol`](AssociateProfitSplitter.sol) 



## Features

* `AssociateProfitSplitter` contract will accept Ether into the contract and divide the Ether evenly among the associate level employees. This will allow the Human Resources department to pay employees quickly and efficiently.


### Starting your project

Navigate to the [Remix IDE](https://remix.ethereum.org) and create a new contract called `AssociateProfitSplitter.sol` using the starter code for level one above.

The [Ganache](https://www.trufflesuite.com/ganache) development chain is connected to MetaMask to `localhost:8545`

###  The `AssociateProfitSplitter` Contract

Three `public` variables:

* `employee_one` -- The `address` of the first employee.

* `employee_two` -- Another `address payable` that represents the second employee.

* `employee_three` -- The third `address payable` that represents the third employee.

A constructor function accepts:

* `address payable _one`

* `address payable _two`

* `address payable _three`

Within the constructor, employee addresses are set to equal the parameter values. This avoids hardcoding the employee addresses.

#### Functions:

* `balance` -- set to `public view returns(uint)` returns the contract's current balance, should always return `0`.

* `deposit` -- set to `public payable` check, ensuring that only the owner can call the function.

  * In this function,

    * The `uint amount` is set to equal `msg.value / 3;` in order to calculate the split value of the Ether.

    * Transfers the `amount` to `employee_one`, `employee_two`,`employee_three`.

    * Since `uint` only contains positive whole numbers, and Solidity does not fully support float/decimals, I must deal with a potential remainder at the end of this function since `amount` will discard the remainder during division.

    * We may either have `1` or `2` wei leftover, so transfer the `msg.value - amount * 3` back to `msg.sender`. This will re-multiply the `amount` by 3, then subtract it from the `msg.value` to account for any leftover wei, and send it back to Human Resources.

* Fallback function -- `function() external payable`, calls the `deposit` function from within it. This ensures that the logic in `deposit` executes if Ether is sent directly to the contract. This is important to prevent Ether from being locked in the contract since we don't have a `withdraw` function in this use-case.

#### Testing the contract

In the `Deploy` tab in Remix, deploy the contract to your local Ganache chain by connecting to `Injected Web3` and ensuring MetaMask is pointed to `localhost:8545`.

You will need to fill in the constructor parameters with your designated `employee` addresses.

Test the `deposit` function by sending various values. Keep an eye on the `employee` balances as you send different amounts of Ether to the contract and ensure the logic is executing properly.

![Remix Testing](https://github.com/TaylorTucker/Solidity/blob/main/Instructions/Images/contract-execution.PNG?raw=true)





 - 
