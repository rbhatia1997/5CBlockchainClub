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

Now, in addition to private and public,Solidity has two more types of visibility for functions (confusing, I know). Specificially, these are ```internal``` and ```external``` respectively. Internal is the same as private, except it's accessible to contracts that inherit from this contract. Amazing, specific, and probably useful if you still want your function to be private but use it in modular code. External is similar to public, except these functions can only be called outside of the contract (they can't be called by functions inside that contract). The syntax here is the same as public and private - so you just add the keyword after the function. 

Now, you may want to interact with other people's contract. This can be done by defining an ```interface```. An interface is similar to defining a contract, except you are only declaring the functions that you want to interact with and the function bodies aren't defined (they are ended with a semicolon). So let's say you created an interface to use a function in a contract someone else wrote (this is all taken from the cryptozombies tutorial):

```javascript
//(Contract someone else wrote):
contract LuckyNumber {
  mapping(address => uint) numbers;

  function setNum(uint _num) public {
    numbers[msg.sender] = _num;
  }

  function getNum(address _myAddress) public view returns (uint) {
    return numbers[_myAddress];
  }
}
```

```javascript
// Thus, the interface looks like...
contract NumberInterface {
    // Yes, you still use the contract keyword.
  function getNum(address _myAddress) public view returns (uint);
}
```
Now, using the interface in a contract (again, taken from the cryptozombies site)... 

```javascript
contract MyContract {
  address NumberInterfaceAddress = 0xab38... 
  // ^ The address of the FavoriteNumber contract on Ethereum
  NumberInterface numberContract = NumberInterface(NumberInterfaceAddress);
  // Now `numberContract` is pointing to the other contract

  function someFunction() public {
    // Now we can call `getNum` from that contract:
    uint num = numberContract.getNum(msg.sender);
    // ...and do something with `num` here
  }
}
```
This, again, assumes that the contract can interact with any other contract given that the function are public or external. 

Now, one thing to note that is interesting about Solidity is that functions can return multiple values. You can either return values or just one specific value by using colons as such: ```(,,valueToReturn)```. Commonly, this is used when you want a specific value from another smart contract (e.g. the cryptokitties smart contract):

```javascript
    (,,,,,,,,,kittyDna) = kittyContract.getKitty(_kittyId);
// assuming we have a uint variable called kittyDna and a address pointing to the cryptokitty smart contract. 
```

So remember how earlier I said that require was similar to an if-else conditional? Well, Solidity actually has ```if``` as a keyword, which operates as one would expect in a programming context. 

## Advanced Solidity Concepts

Solidity is unique in that after you deploy a contract to Ethereum, it's immutable (it can never be modified or updated again). You need to ensure that the smart contract you upload is without flaws because you literally cannot change it once you start. 

Because of this, it would make sense to have functions that would enable a user to change certain "permanent" parts of an dapp (e.g. having a function that can set the address of a contract in case it changes in the future). 

So, obviously, if we set this function as external, it would be a massive security flaw (allowing all users the ability to change the function). Therefore, to handle these specific cases where you want to give a specific person special privledges (e.g. yourself), you can use ```Ownable```. 

The Ownable contract, taken from the OpenZeppelin Solidity library, is a library of secure and community-vetted smart contracts. If you were to look up this contact, you'd find some special stuff. First, a ```constructor``` (an optional special function) has the same name as the contract. It only gets run once (when the contract is first created). Next, a function ```modifier```, which are half-functions to modify other functions. This Ownable contract contains a function called ```onlyOwner```, which is so popular that most Solidity DApps start with a copy/paste of the Ownable contract. 

A function modifier, as mentioned previously, looks like a function but uses the keyword modifier instead of the keyword function. It can't be called directly (instead, the modifier's name is attached to the end of a function definition to change its behavior). So, if you have a modifier, it will execute code its code first then when it hits ```_:``` (placed at the end of the modifier's code), it executes the original function's code. The most common use for modifiers is to add require checks before a function executes. If you add the ```onlyOwner``` modifier to a function, it makes it such that only the owner of the contract can call that function. You would simply add this keyword after the function (e.g. after ```public``` keyword). 

Now, in Solidity, users have to pay every time they execute a function on the DApp using a currency called ```gas```. Gas is purchased with Ether (Ether has to be spent to execute functions on the dApp). How much gas depends on how complex that function's logic is. Each individual operation has a gas cost that's based on the computational resources necessary to perform that operation. Code optimization, as you can imagine, is crucial for Solidity. 

Why is gas necessary you might be asking?It's incredible stupid to have people pay to use your functions, isn't it? No, not exactly. Ethereum is extremely secure. The beauty of its security stems from the fact that every node on the network needs to run that same function to verify the output when you call it; the fact that so many nodes need to verify a function when it runs makes Ethereum decentralized and immutable. Having users pay is one way to prevent people from having an infinite loop or hog up all the network resources. 

So how can we save gas? One way is struct packing. Specifically, having multiple uints inside a struct using a smaller-sized uint when possible allows Solidity to pack variables together to take up less storage. Note that using uint8 versus uint won't change anything normally; however, inside a struct, the rules change. It's a good rule to also cluster identical data types together. 

So, Solidity has time units that provide native units for dealing with time (kind of like millis in Arduino). The variable ```now``` will give you the unix timestamp of the latest block (number of seconds since January 1st, 1970). Solidity also contains seconds, minutes, days, hours, weeks, and years as keywords.

Another thing that you can do in Solidity is pass a storage pointer to a struct as an argument to a private/internal function. In order words, if you have a function, the function can be something like ```function _functionName(StructName storage _parameterName) internal```. This would allow a user to pass a reference to the struct, which is useful in the instance you want to pass a reference to an object instead of the ID and looking it up inside the function.

Function modifiers also can take arguments as well. This is important in Solidity as you can have a modifier check a certain requirement (e.g. age limit) before you run a function. 

One really, really, ```really``` important thing about the Solidity blockchain is that view functions don't cost any gas when they're called externally by a user. This is because they don't change anything on the blockchain. Normally, you would have to create a transaction on the blockchain - running it on every single node - and costing a user gas. 

Please for the love of God use external view functions whenever possible. Do realize that internal view functions will cost gas because the other function creates a transaction on Ethereum and needs to be verified. 

Everytime you write or change a piece of data, it's permanently written in the blockchain forever. Please avoid writing data to storage unless it's absolutely needed. The ```memory``` keyword is useful for creating new arrays without needing to write anything to storage; it only exists until the end of the function call. This looks like the following (taken from cryptozombies tutorial): 

```javascript
function getArray() external pure returns(uint[]) {
  // Instantiate a new array in memory with a length of 3
  uint[] memory values = new uint[](3);
  // Add some values to it
  values.push(1);
  values.push(2);
  values.push(3);
  // Return the array
  return values;
}
```

Side note: for loops work the same (nearly the same) way in Solidity as they do in Javascript/C++. It can be helpful to use for-loops to traverse arrays and store data temporarily in them. 

## Making People Pay... in Solidity

Super quick summary from everything before. Private means callable from other functions in the contract; internal is like private but it can be called by inherited contracts; external can only be called outside the contract; public can be called anywhere, anytime. 

State modifiers include view, which indicates no data will be changed, and pure, which indicates no data saved or read from the blockchain. But there is another modifier that is just... beautiful. 

This modifier is ```payable``` and it's a function that can receive Ether. Because money (Ether) and data (transactions) live on Ethereum, you can call a function and pay money to the contract at the same time. ```ether``` (yes, lowercase) is a built-in keyword to reference the amount of Ether. Techincally this means you can call a function from web3.js (DApp's front-end) by doing the following (taken from Cryptozombies): 

```javascript
// Assuming `OnlineStore` points to your contract on Ethereum:
OnlineStore.buySomething({from: web3.eth.defaultAccount, value: web3.utils.toWei(0.001)})
```
Value, in this case, specifies how much Ether to send. Now, you probably want to withdraw that Ethereum from the contract eventually - so do add the following contract (assuming the Ownable contract is imported properly). 

```javascript
// From cryptozombies 
contract GetPaid is Ownable {
  function withdraw() external onlyOwner {
    address _owner =  owner();
    _owner.transfer(address(this).balance);
    // address(this).balance returns the total balance stored on the contract.
  }
}
```
If, for some reason, you want to randomly generate numbers in Solidity... it's a bit rough. There's the keccak256 hash function, which can be used to generate a random uint as so (from cryptozombies):

```javascript
// Generate a random number between 1 and 100:
uint randNonce = 0;
uint random = uint(keccak256(abi.encodePacked(now, msg.sender, randNonce))) % 100;
randNonce++;
uint random2 = uint(keccak256(abi.encodePacked(now, msg.sender, randNonce))) % 100;
```

This is pretty bad though because of the way blockchain works. In Ethereum, calling a function on the contract broadcasts it to node/nodes on the network as a transaction. The nodes collect many of these transactions and try to solve a proof of work algorithm and publish that as a block to the network. Once a node solves the proof of work algorithm, the other nodes verify the other node's list of transactions and accept the block. 

So why exactly does a random number generate using keccak give trouble? If I were to publish a transaction only to my own node and not share the results, I could effectively keep running a function until I get a desired result and solve the next block. 

There are external sources on how to properly deal with random numbers in Solidity. There is the concept of an ```oracle```, which helps you access resources safely outside of the Ethereum blockchain. 

## ERC721 & Crypto-Collectibles

So Ethereum and blockchain is fun, but this is the surface of how wacky and cool things can be. We're going to get into the fun, exciting world of ```tokens```. A token on Ethereum is just a smart contract that follows some common rule - it implements a standard set of functions that all the other token contract share from. The contract will have a mapping that indicates how much balance each address has. In other words, the token is a contract that keeps track of who owns how much of the token and contains function to enable trading of such tokens. 

So, applications that work for one token (specifically talking about the ERC20 token now) will work for the others. When an exchange adds a new ERC20 token, it needs to add another smart contract. Users can indicate where to send tokens to and the exchange can tell the contract to send the tokens back out to users when they request a withdraw. Tokens that act like currencies will find benefit from the exchange model (hmm... sounds familiar ;)). 

Okay, great, but what if I want to build a decentralized application that doesn't necessarily ```vibe``` with the notion of a currency. What I mean to say is that you can divide currency, like Ethereum, but it's a bit harder to cleanly divide something like a [crypto-kitty](https://www.cryptokitties.co/). You can't own 0.232342 of a Crypto-Kitty (I mean you could, but that's pretty gross and difficult to keep track of). So where am I getting with this?

There's another token standard called ```ERC721``` which is really solid for crypto-collectibles (and oh man are they fun). One really fun example is the Formula 1 (yeah, the racing company) non-fungible token - the [first car to be realsed for the F1 Delta Time](https://opensea.io/assets/0x3c62e8de798721963b439868d3ce22a5252a7e03/111). This sold for 415.9 Ethereum (which is around 112,708.9 USD at the time of writing). So ERC721 tokens are not interchangeable because each one is unique; you can only trade them in whole units and each one has a unique ID. The benefits of using a token standard is the fact that people could integrate the tokens into their platform easily. The ERC721 standard is the following:

```javascript
contract ERC721 {
  event Transfer(address indexed _from, address indexed _to, uint256 indexed _tokenId);
  event Approval(address indexed _owner, address indexed _approved, uint256 indexed _tokenId);

  function balanceOf(address _owner) external view returns (uint256);
  function ownerOf(uint256 _tokenId) external view returns (address);
  function transferFrom(address _from, address _to, uint256 _tokenId) external payable;
  function approve(address _approved, uint256 _tokenId) external payable;
}
``` 
These methods would need to be implemented in order to implement the token contract. In order to implement the contract, the first thing to do is copy the interface to its own Solidity file and import it using the following command (for ERC721): ```import "./erc721.sol";```. You can inherit from multiple contracts by adding a comma in the ```is``` contract statement. In utilizing ERC721 in your Solidity code, make sure that you read the contract properly (e.g. using the ```Transfer``` event after transferring Eth). Make sure to include the keyword ```emit``` before Transfer (and Approval). You want to be really careful that your user doesn't transfer the zombie to an address of 0 (burning a token, sending it to an unaccessible address). One security feature in writing smart contracts is preventing overflows and underflows. An overflow is when you increase a uint8 at 255 by 1 and an underflow is when you decrease a uint8 at 0 by 1. This is like a clock resetting (i.e. going from 00:00 to 23:59 and vice versa). This can create undesireable behavior. 

So to prevent these issues from ever being a problem, there is a library called SafeMath that prevents these issues by default. A library is a contract in Solidity that attaches functions to native data types. To use SafeMath you would write ```using SafeMath for uint256``` for example at the top of the function. Be sure to import the SafeMath library and include the .sol file in the directory. If you snoop around in the .sol file for SafeMath, you will come across the keyword ```assert```, which is similar to require except assert will not return a user's gas when a function fails (i.e. you want to use this when something goes horribly wrong in the code). 

But what about the case where you're using a uint16 or uint32? You need to actually implement two more libraries for that (SafeMath16 and SafeMath32). While Solidity should really automatically do all this for us,it doesn't as of my writing this. 

Something that's important to note that really should've been noted later is commenting. We use the ```//``` for single line comments. However, multi-line comments can be used by starting with ```/*``` and closing with ```*/``` just like in the Arduino IDE. The standard in Solidity is to use a format called ```natspec```, which looks like the following (taken from cryptozombies tutorial):

```javascript
/// @title A contract for basic math operations
/// @author Ronak B.
/// @notice explains to a user what the contract / function does. @dev is for explaining extra details to developers.
contract Math {
  /// @notice Multiplies 2 numbers together
  /// @param x the first uint.
  /// @param y the second uint.
  /// @return z the product of (x * y)
  /// @dev This function does not currently check for overflows
  //@param and @return are for describing what each parameter and return value of a function are for.
  function multiply(uint x, uint y) returns (uint z) {
    // This is just a normal comment, and won't get picked up by natspec
    z = x * y;
  }
}
```

## Front-End for Applications & Web3.js

Ethereum has a Javascript library from the Ethereum foundation called Web3.js. When you call a function on a smart contract, you need to query one of the nodes on the Ethereum network and tell it the address of the smart contract, the function you want to call, and the variables you want to pass to that function. Ethereum nodes communicate using ```JSON-RPC```, which looks like absolute horse-shit. Web3.js hides these queries with cleaner syntax. You can install web3.js to the project by using ```npm install web3```. There's also a github with the .js file and you can include the following import statement: ```<script language="javascript" type="text/javascript" src="web3.min.js"></script>```. 

So when you are writing the front-end application for the