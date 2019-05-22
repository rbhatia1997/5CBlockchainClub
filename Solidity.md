# Getting Started with Solidity

Before starting this tutorial, I want to give a bit of context to Solidity and why it might be important for one to understand. 

So first, what is Ethereum. Ethereum is "a global, open-source platform for decentralized applications" according to their [website](https://www.ethereum.org/). Actually this website would be the best place to start to understand what exactly is going on with Ethereum.

Let's get excited about Ethereum. It's time for a new era of the Internet - one in which money and payments are built-in and you own your data. No company or person should own the infrastructure - it should be a neutral, open-access infrastructure. Founded in 2015, Ethereum is the world's "leading programmable blockchain" and has a native cryptocurrency called Ether (ETH). 

The cool part about learning Ethereum is that you can build decentralized applications (called dapps) that utilize the very technology of cryptocurrency/blockchain. Games, decentralized markets, cryptocurrency wallets, and other financial applications are all possible.

"Ethereum is different than Bitcoin in that it allows for smart contracts which can be described as highly programmable digital money. Imagine automatically sending money from one person to another but only when a certain set of conditions are met." [Source](https://blog.coinbase.com/a-beginners-guide-to-ethereum-46dd486ceecf)

Some applications which exist include Cent (social network where you earn money by posting), Veil (placing bets on real world events), and CryptoKitties (collecting and breeding digital cats). Before I continue, I should plug the resources available on Ethereum's website, which will likely be more helpful than my rambling. 

The first source is on [using Ethereum](https://www.ethereum.org/use/)

The second source is on [learning Ethereum](https://www.ethereum.org/learn/)

The third source is on [developing with Ethereum](https://www.ethereum.org/developers/)

The final source is what I will base this tutorial off of, availble [here](https://cryptozombies.io/en/lesson/1/chapter/1)

## Introduction to Solidity 

Now that there is some context into Ethereum, it is important to introduce Solidity. Ethereum uses something called smart contracts (programs on the Ethereum blockchain) that send or receive Ether (amongst many other things). 

So this is cool and all, but Ethereum contracts are actually written in a programming language. One very common language is Solidity (which is the language of choice).

Solidity's code uses something called *contracts* which are the fundamental building block of ethereum applications. All the variables and functions belong to this *contract* and it is the starting point of a project. 

So when starting a ```.sol``` project file in Solidity, you're going to want to first enter the Solidity version that you're working with (which can be done by typing in the following:

```javascript
pragma solidity ^0.4.25; // Indicates version

contract HelloWorld {
    // Put your work here. 
}
```

State variables are stored in contract storage (written to the blockchain) - so it's similar to writing them to a database. I've noticed that writing in Solidity is similar to C++ where you have to add a semicolon at the end of every line of code. Obviously, as with any programming language, the basic math operations are built in. 

## Getting Deeper into Solidity...

