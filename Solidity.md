# Getting Started with Solidity

Before starting this tutorial, I want to give a bit of context to Solidity and why it might be important for one to understand. 

So first, what is Ethereum. Ethereum is "a global, open-source platform for decentralized applications" according to their [website](https://www.ethereum.org/). Actually this website would be the best place to start to understand what exactly is going on with Ethereum.

Let's get excited about Ethereum. It's time for a new era of the Internet - one in which money and payments are built-in and you own your data. No company or person should own the infrastructure - it should be a neutral, open-access infrastructure. Founded in 2015, Ethereum is the world's "leading programmable blockchain" and has a native cryptocurrency called Ether (ETH). 

The cool part about learning Ethereum is that you can build decentralized applications (called dapps) that utilize the very technology of cryptocurrency/blockchain. Games, decentralized markets, cryptocurrency wallets, and other financial applications are all possible.

"Ethereum is different than Bitcoin in that it allows for smart contracts which can be described as highly programmable digital money. Imagine automatically sending money from one person to another but only when a certain set of conditions are met." [Source.](https://blog.coinbase.com/a-beginners-guide-to-ethereum-46dd486ceecf)

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

So now, we may need more complex data types. Solidity provides something called *structs* which come in the following form: 

```javascript

struct Thing {
  uint variable1;
  string variable2;
}
```

Now, if we want a collection of something, we want to use data types called *arrays*, which are either dynamic or fixed. A dynamic array has no fixed size; a fixed array has a fixed size. You would do the following:

```javascript

uint[2] fixedArray; 
string[5] stringArray; 
uint[] dynamicArray; 
```

You can even create an array of structs if you wanted to by doing the following: ```Thing[] thing1;``` assuming we had a Thing struct. 

Arrays can be public, which allows Solidity to enable access to it if other people are using your code. You just need to add the word "public" in front of the array type like so: ```Thing[] public thingArray;```. Other contracts could read from but not write to this array. 

Therefore, if we wanted to create new Things and add them to the thing array, we would simply do the following: 

```javascript
// create a New Thing:
Thing thing22 = Thing(22, "Thing22");

// Add that person to the Array:
thingArray.push(thing22);
```

Cleaner code would probably do the following: 

```javascript
thingArray.push(Thing(22, "Thing22"));
// adds to end of the thingArray.
```

If you want to write a function in Solidity, you just use the word ```function``` and specify the parameters in the call. Many people often start function parameter names with an underscore to differentiate these from global variables. This would look like the following: 

```javascript
function createThing (string _nameOfThing, uint _numberOfThing) {
    // do stuff here. 
}
```

Combining this information with what was learnt above, we notice that we could push items to the public array using this function if we simply add the following line: 

```javascript
function createThing (string _nameOfThing, uint _numberOfThing) {
    thingArray.push(Thing(_nameofThing,_numberOfThing)); 
}
```

In Solidity, functions are public by default; however, this means that anyone can just call the contract's function and execute the code. Obviously, this may not be great for your application so thankfully we can make functions private (which we want to probably set by default unless we for sure want to give people the ability to publically access something). 

You'd just accomplish this by adding the word ```private``` after the function's parameters. For some reason, we call the function with an underscore to indicate that it's a private function. So using the example above, we'd have:

```javascript
function _createThing (string _nameOfThing, uint _numberOfThing) private {
    thingArray.push(Thing(_nameofThing,_numberOfThing)); 
}
```
## Getting Even Deeper into Solidity...

As you may know already, functions can return values by using the keyword ```return```. In Solidity, we also have to consider function modifiers that indicate the state of the function. For example, if I wanted to declare a function with the ability to view, I can simply just write ```view``` in the function like so:

```javascript
function someFunction() public view returns (string) {
    // only lets you view data not modify it!
}
```

You could also use ```pure``` functions, which means you are not even accessing data that's in the application. In other words, you can write a function that doesn't read from the state of the app (only function parameters). An example is provided below: 

```javascript
function _multiply(uint a, uint b) private pure returns (uint) {
  return a * b; // pure because uses only parameters.
}
```
Something unique about Solidity is that you are actually specifying the return type value! 

Now, as you may or may not be familiar with, hash functions are very commonly used for blockchain purposes. The hash function basically maps an input to a random value where a small change in the input corresponds to a large change in the hash (you can imagine this being useful for cryptographic purposes). 

Ethereum has the hash function called ```keccak256``` which is a version of SHA3. It expects a single parameter of type bytes, so one must "pack" any parameters before calling this hash function. This is accomplished in Solidity, for example, by doing the following: ```keccak256(abi.encodePacked("aaaab"));``` 

Something to note is that in Solidity, you should typecast by using parenthesis like so: ```uint8 c = a * uint8(b); ```

So obviously, with this knowledge, you can write private and public functions. This will be helpful when writing decentralized applications or smart contracts. 

Now, you can use something called an ```event``` which enables your contract to communicate anything on the blockchain to the front-end app, which listens for certain events and takes action when they happen. The ```event``` keyword,which contains the parameters and result, is written similar to a function. 

You could use the keyword ```emit``` to indicate an event being fired. This would usually be put inside the function and looks like the following:

```javascript
// declare the event
event IntegersAdded(uint x, uint y, uint result);

function add(uint _x, uint _y) public {
  uint result = _x + _y;
  // fire an event to let the app know the function was called:
  emit IntegersAdded(_x, _y, result);
  return result;
  // From the cryptozombies tutorial
}
```

So one thing that you can do once you've written your back-end application is connect it to a front-end application (for example, a Javascript front end). This can be accomplished by utilizing the ```Web3.js``` library that is in Ethereum for Javascript. 

## Mappings and Addresses: Ethereum Blockchain Details

So, the Ethereum blockchain is made up of ```accounts```, which are like bank accounts (in that they have a balance of Ether). Ether is the currency used on the Ethereum blockchain. You can send and receive Ether payments to other accounts just like a wire transfer to a bank account. Each account has an ```address``` which is a number similar to a bank account number. It's a unique identifier that points to the account. An address is owned by a specific user (or smart contract). 

So, in Solidity, ```Mappings``` are another way of storing organized data in Solidity. You can define a ```mapping``` by doing the following: 

```javascript
// For a financial app, storing a uint that holds the user's account balance:
mapping (address => uint) public accountBalance;
// Or could be used to store / lookup usernames based on userId
mapping (uint => string) userIdToName;
// Taken from cryptozombies tutorial. 
```
A mapping is just a key-value store for storing and looking up data; you would enter the key in order to access the value. The first example above would take an address as the key and return a uint or number as the value. 

The mappings can be used to keep track of information and to whom that information is owned by (like a user who owns something on the decentralized application). But you need to update your methods in order to actually use the mappings; you can use this by using the ```msg.sender```, which refers to the address of the person (or smart contract) who called the current function. A function execution starts with a external caller; a contract does nothing until someone calls one of its functions. 

So for example, if you had a mapping to a favorite number and a function that sets a number to the favorite number, it would look like the following (example for cryptozombies): 

```javascript
mapping (address => uint) favoriteNumber;

function setMyNumber(uint _myNumber) public {
  // Update our `favoriteNumber` mapping to store `_myNumber` under `msg.sender`
  favoriteNumber[msg.sender] = _myNumber;
  // ^ The syntax for storing data in a mapping is just like with arrays
}

function whatIsMyNumber() public view returns (uint) {
  // Retrieve the value stored in the sender's address
  // Will be `0` if the sender hasn't called `setMyNumber` yet
  return favoriteNumber[msg.sender];
}
```

In this case, anyone could call the setMyNumber function and store a uint in the contract, which would be tied to their address. Then, when calling whatIsMyNumber, they'd be returned the uint that was stored. 

Although this is a really simple example, the beauty of blockchain is shown. The ```msg.sender``` is secure because you would have to steal the private key associated with the Ethereum address in order to modify someone's data. 

Another feature of Solidity is ```require```, which makes it so that the function will throw an error and stop executing if some condition isn't true. You can think of this like a try-catch or while statement. This looks like the following:

```javascript
function compareName(string _name) public returns (string) {
  require(keccak256(abi.encodePacked(_name)) == keccak256(abi.encodePacked("Isaac")));
  // no built-in function for string comparison, so compare the hash values. 
  // If it's true, proceed with the function:
  return "Hi!";
}
```

In this case, if you were to use a different name other than Isaac, the function would not run (execute) and it would throw an error. Require is useful for verifying conditions before running a function! 

So you think you're hot shit because you can write one extremely long contract? Well, guess what, Solidity thinks that you should slow your roll bro. In other words, Solidity has a feature for contracts called ```inheritance``` that makes it possible to split code logic across multiple contracts. This is accomplished by using the ```is``` keyword; let's say that you had a contract called Cookie. You could create another contract called Chocolate Chip that would inherit from the Cookie contract like so: ```contract ChocolateChip is Cookie```. If you were to compile and deploy ChocolateChip, it would have access to the functions (public ones) that are defined in Cookie. 

Now, when you have files that reference each other, you're likely going to use the ```import``` ability, which would look like this in practice: ```import "./someothercontract.sol";```. This, of course, assumes that the other contract is available in the same directory as the file we are calling this import statement from. 

In Solidity, you can store variables in storage or in memory. Storage refers to variables stored permanently on the blockchain; memory variables are temporary and are erased between external function calls to the contract. It's similar to RAM whereas the storage is similar to information on a hard-disk (or heap vs. stack in C++). Solidity mostly handles these keywords by default; however, there are times where you do need to use the keywords (e.g. with structs and arrays within functions). 

The example given in the cryptozombies tutorial clarifies this:

```javascript
contract SandwichFactory {
  struct Sandwich {
    string name;
    string status;
  }

  Sandwich[] sandwiches;

  function eatSandwich(uint _index) public {
    // Sandwich mySandwich = sandwiches[_index];

    // ^ Seems pretty straightforward, but solidity will give you a warning
    // telling you that you should explicitly declare `storage` or `memory` here.

    // So instead, you should declare with the `storage` keyword, like:
    Sandwich storage mySandwich = sandwiches[_index];
    // ...in which case `mySandwich` is a pointer to `sandwiches[_index]`
    // in storage, and...
    mySandwich.status = "Eaten!";
    // ...this will permanently change `sandwiches[_index]` on the blockchain.

    // If you just want a copy, you can use `memory`:
    Sandwich memory anotherSandwich = sandwiches[_index + 1];
    // ...in which case `anotherSandwich` will simply be a copy of the 
    // data in memory, and...
    anotherSandwich.status = "Eaten!";
    // ...will just modify the temporary variable and have no effect 
    // on `sandwiches[_index + 1]`. But you can do this:
    sandwiches[_index + 1] = anotherSandwich;
    // ...if you want to copy the changes back into blockchain storage.
  }
}
```