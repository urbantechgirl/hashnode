## Cryptocurrency Tutorial Using METAMASK And REMIX IDE

In this step-by-step tutorial, you will learn how to create and deploy an ERC-20 token on Ethereum.

We will use [Metamask](https://metamask.io/) and [Remix IDE](https://remix.ethereum.org) for this tutorial.


## What is ERC-20?

**ERC** stands for **Ethereum Request for Comment**

An ERC20 token is a standard used for creating and issuing smart contracts on the Ethereum blockchain. It was proposed in November 2015 by Ethereum developer Fabian Vogelsteller.
ERC-20 defines a common list of rules for Ethereum tokens to follow within the larger Ethereum ecosystem, allowing developers to program how new tokens will function in this ecosystem. This also allows developers to accurately predict interaction between tokens. These rules include how the tokens are transferred between addresses and how data within each token is accessed. Most tokens on Ethereum comply with the ERC-20 specification. Following a standard like ERC-20 allows application developers which use ERC-20 tokens to easily support all ERC-20 tokens without having to write specialized code for them individually.

 ### **Prerequisites**
1. Make sure you have downloaded and installed Metamask.
2. Select the Rinkeby Testnet network to work with
3. Request some testnet ether on Rinkeby through any one of the following faucets:

[  Metamask Faucet](https://faucet.metamask.io/)

[Chainlink Faucet](https://faucets.chain.link/rinkeby)

[Paradigm Faucet](https://faucet.paradigm.xyz/)

*Once you have set all of these up, let's get started!*

## Writing the code
We are using Remix IDE for writing the smart contract.

In Remix, create a new contract file, I named mine [ZQToken.sol](https://github.com/urbantechgirl/learnweb3.io/tree/main/ZQToken) - you can name it whatever you want!

In the contract, write the following code:

```
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

import "https://github.com/OpenZeppelin/openzeppelin-contracts/blob/master/contracts/token/ERC20/ERC20.sol";

contract ZQToken is ERC20 {
    constructor(string memory _name, string memory _symbol) ERC20(_name, _symbol) {
        _mint(msg.sender, 10 * 10 ** 18);
    }
```
**it will look like this**
![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1653052158259/LapRPSCc3.png align="left")
Let's break it down line-by-line and understand what is going on:
```
pragma solidity ^0.8.0;
```
This line specifies the compiler version of Solidity to be used. 
```
import "https://github.com/OpenZeppelin/openzeppelin-contracts/blob/master/contracts/token/ERC20/ERC20.sol";
```
This line imports the ERC-20 token standard from OpenZeppelin (OZ). OZ is an Ethereum security company.  Whenever implementing a smart contract which needs to comply with a standard, try to find an OZ reference implementation rather than rewriting the entire standard from scratch.
You can look at the implementation of ERC-20 standard contract if you want by following the link - https://github.com/OpenZeppelin/openzeppelin-contracts/blob/master/contracts/token/ERC20/ERC20.sol
```
contract ZQToken is ERC20
```
This specifies a new contract, named LW3Token, in our Solidity file. Also, it says that this contract is an instance of ERC20. ERC20 in this case refers to the standard contract we imported from OpenZeppelin.
```
{
    constructor(string memory _name, string memory _symbol) ERC20(_name, _symbol) {
        _mint(msg.sender, 10 * 10 ** 18);
    }
```
We created a constructor function that is called when the smart contract is first deployed. Within the constructor, there are two arguments from the user which specify the name and symbol of our cryptocurrency. E.g. name = Ethereum, symbol = ETH.

Immediately after specifying the constructor function, we call ERC20(_name, _symbol).

The ERC20 contract we imported from OpenZeppelin has its own constructor, which requires the name and symbol parameters. Since we are extending the ERC20 contract, we need to initialize the ERC20 contract when we deploy ours. So, as part of our constructor, we also need to call the constructor on the ERC20 contract.

Therefore, we are providing _name and _symbol variables to our contract, which we immediately pass on to the ERC20 constructor, thereby initializing the ERC20 smart contract.

**mint** is an internal function within the ERC20 standard contract, which means that it can only be called by the contract itself. Since you as the developer want to receive some tokens when you deploy this contract, we call the _mint function to mint some tokens to msg.sender.

_mint takes two arguments - an address to mint to, and the amount of tokens to mint.
 10 * 10 ** 18 specifies that you want 10 full tokens to be minted to your address.

*Note: You might be wondering why we did not just write '10' in the amount, instead of 10 ** 18 (which is actually 10 ^ 18).*
ERC20 tokens by default work with 18 decimal places. So 1 full LW3Token in this case, is actually represented as 10 ^ 18. Therefore, to get 10 full LW3Tokens, we use 10 * 10 ** 18.

## Compiling

1. Open REMIX IDE
![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1653051895507/oO5PuqZSl.png align="left")

1. Go to the Solidity compiler tab select ZQToken.sol and click on compile

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1653052227079/K4zQ020t_.png align="left")

## Deploying
1. Go to the Deployer tab in Remix.

2. Select the Injected Web3 environment (ensure you are on the Rinkeby Test Network), and connect your Metamask wallet.
![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1653053126765/8TV9I0AVs.png align="left")


3. Select the ZQToken.sol contract, and enter values for the constructor arguments _name and _symbol under the option 'deploy' Click Transact and approve the transaction from Metamask to deploy your contract!

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1653053406033/rIgtL2NLv.png align="left")
A metamask notification like this will pop up.
When deployed, the contract should show up under the Deployed Contracts section. Click the Copy Address button to copy the contract address.

**CONGRATS YOU'VE CREATED YOUR VERY OWN TOKEN!**

## HOW TO VIEW Tokens in Metamask
You may notice that even though you minted tokens to your address, they don't show up in Metamask.


- Copy your contract address
- Open Metamask and click Import Tokens in the Assets tab
![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1653053733857/J_fUkUKAK.png align="left")
- Enter your Token Contract Address, and it should detect the name and number of decimals automatically
- Click Add, and you will see your balance in Metamask!
![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1653054484141/xdq9ka2Ki.png align="left")
