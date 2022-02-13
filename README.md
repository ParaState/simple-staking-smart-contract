# Simple Staking Smart Contract

A smart contract which allows users to stake and un-stake a specified ERC20 token. 
Staked tokens are locked for a specific length of time (set by the contrat owner at the outset).
Once the time period has elapsed, the user can remove their tokens again.

![Untitled Diagram (1)](https://user-images.githubusercontent.com/9831342/151649198-5de7bfe2-095a-4d14-9fd4-dd53d78e94a3.jpg)

## How to deploy

- Compile the [SimpleStaking.sol](https://github.com/second-state/simple-staking-smart-contract/blob/main/SimpleStaking.sol) contract.

- Deploy the contract by passing in the official ERC20 token's contract address as the one-and-only constructor parameter.

- Call the `setTimestamp` function (as the contract owner) by passing in a value (in seconds) for which you want the timelock period to be. The value which you pass in, will be added to the block.timestamp as at the time you called the setTimestamp function. For example, if you passed in 3600, then the timelock period would be 1 hour from now.

## Test the contract (approval)

**This approval step is actually performed by the DApp's User Interface (UI).** The DApp will first check the `approval` relationship of the Simple Staking Smart Contract's deployment address and the user (`msg.sender`) and then present the user with an offer to approve a MetaMask transaction (in the event that the `approve` function needs to be actioned before the DApp can successfully proceed with the task of transferring the suggested amount of tokens from the ERC20 contract to the Staking contract). Once this back and forth has occured, the DApp will know that it is possible to proceed and will get on with the staking (as outlined in the step following this one)

Go to the ERC20 contract using wallet software of a user who holds ERC20 tokens.

Perform the `approve` function by passing in the Simple Staking Smart Contract's deployment address. Also add an amount of tokens which you would like to approve the Simple Staking Smart Contract to spend on the user's behalf.


<img width="285" alt="Screen Shot 2022-01-29 at 4 12 02 pm" src="https://user-images.githubusercontent.com/9831342/151650067-6c2d5144-3c38-40d9-8f46-ddf3c9273f0d.png">

Confirm the approval worked by calling the `allowance` function (passing in the user's address and the Simple Staking Smart Contract's deployment address)

<img width="279" alt="Screen Shot 2022-01-29 at 4 12 09 pm" src="https://user-images.githubusercontent.com/9831342/151650100-d10386c1-63d4-4359-af70-f36b966b36aa.png">

## Test the contract (staking)

Go to the Simple Staking Smart Contract and perform the `stakeTokens` function, by passing in the ERC20 contract's address and the amount of tokens you approved in the above step.

The tokens will be staked now.

You can check that the Simple Staking Smart Contract actually holds these tokens by checking the ERC20's `balanceOf` function (by passing in the Simple Staking Smart Contract's address)

<img width="293" alt="Screen Shot 2022-01-29 at 4 22 50 pm" src="https://user-images.githubusercontent.com/9831342/151650182-02b155c2-115a-46a1-8f78-62db241cbe80.png">

You can also check that your user's balance of ERC20 tokens has reduced by 250 (was 500 before)

<img width="358" alt="Screen Shot 2022-01-29 at 4 23 33 pm" src="https://user-images.githubusercontent.com/9831342/151650217-1cc42488-e7c9-4254-bd3e-f013349f0513.png">

## Test the contract (un-staking)

Go ahead and call the Simple Staking Smart Contract's `unstakeTokens` function by passing in the ERC20 contract's address and also the amount you wish to unstake. The `msg.sender` is the recipient by default, so we don't need to pass your user's address in. This is a feature which only allows the `msg.sender` to unlock their own tokens. Other users can not unstake other random user tokens.

You will now see that your user's ERC20 balance in their wallet has risen back from 250 to 500.

<img width="353" alt="Screen Shot 2022-01-29 at 4 27 40 pm" src="https://user-images.githubusercontent.com/9831342/151650326-d9812ee5-6b6f-4627-a107-c6d0e84fca3b.png">

You will also see that the ERC20 token contract no longer shows the Simple Staking Smart Contract's address as a holder of the ERC20 token.

<img width="287" alt="Screen Shot 2022-01-29 at 4 29 19 pm" src="https://user-images.githubusercontent.com/9831342/151650351-fa55287f-aad4-43f0-b7f7-ab8b185106cd.png">

Finally, you will also notice that the Simple Staking Smart Contract's `balance` for that specific user is back to `0`

<img width="283" alt="Screen Shot 2022-01-29 at 4 30 21 pm" src="https://user-images.githubusercontent.com/9831342/151650392-6b1d2fe9-18e4-4fea-a8fc-08865eac76ca.png">


