# Introduction to Blockchain

## Very Basic Fundamentals of Blockchain 
This part of the tutorial is heavily influenced by the following [link](https://hackernoon.com/learn-blockchains-by-building-one-117428612f46). In fact, it should be seen as an addendum to this tutorial with more clarification. Now, what is Blockchain? It's an immutable (not changeable), sequential chain of records. Such records are called **blocks.** They contain transactions or any type of data you want to store in them. They're linked together using hashes. 

### What are Hashes?
This part of the tutorial is heavily influenced by the following [link](https://learncryptography.com/hash-functions/what-are-hash-functions). A hash function takes an input value, and from the input value, creates an output determined on what the input value is. 

To make this easier, consider a simple function: y = f(x). A function will take an input, x, and give out the output (y) based on the input x. Now, a *hash function* takes an input (which doesn't necessarily need to be a number) and outputsa hash. For example, if I were to input "hello" into a function called md5, I would get a long list of hexadecimal output (e.g. `5eb63bbe01eeeed093cb22bb8...`).Most hashes are displayed as hexadecimal output. Importantly, the hash function in this case (md5) output a 32-character long hexdecimal output. 

Now, hash functions generally are one-way or irreversible (hmm.. there may be a reason why we would consider them for blockchain [see: immutable]). Therefore, we can actually use such functions to prove that something is the same as another thing without revealing the information beforehand. 

A good example is that if I have the answer to how many Jellybeans are in a jar in my room and I want to challenge my friends to get the correct answer, I can make sure that they won't cheat by asking them to compare the hash that they receive from their answer to a hash that I give them. I can run the answer througha hash function to recieve that hash. Hashes are often used in the context of verifying information without revealing it to the people who are verifying. 

##  HTTP Requests & How They Work

Before we begin, it may be useful to download this free software called [Postman](https://www.getpostman.com/). This is useful as an HTTP Client, but we'll get to this later! 

I'm basically going to paraphrase from this website [here](https://www.w3schools.com/tags/ref_httpmethods.asp) for this next part. If you want to read it instead of my commentary, go ahead. 

### What is HTTP?

Let's start by discussing what HTTP even means. It stands for Hypertext Transfer Protocol. It creates communication between clients and servers. A browser, like Chrome, may submit an HTTP request to a server and the server will respond to the client (browser). You may be familiar when people make "404 not working" jokes; what they are referring to is an error message. Specifically, in the Hypertext Transfer Protocol (HTTP) standard response code. It is what happens when a client wants to follow a broken or dead link. 

### HTTP Methods

There are many types of HTTP methods, which include GET, POST, PUT, and DELETE. 

**GET Method** is used to request data. It's a very popular HTTP method. Important to note that data is visible to everyone in the URL!

**POST Method** is used to send data to a server and create or update a resource. The data to be sent to the server is stored in something called the "request body" of the HTTP request. Data isn't displayed in the URL. Also no restrictions on data length. 

**PUT Method** is used to send data to a server and create or update a resource. You may ask, why is this different than the POST method? Essentially, the PUT method will produce the same results when called repeatedly whereas the POST method will create the same resource multiple times. 

**DELETE Method** is used to delete a resource specified. That's pretty self-explanatory. 

I could discuss the HEAD method or OPTIONS method, but the methods above are the most common. A quick google search solves most queries here. 

Why do we care about HTTP Requests? Well, in the tutorial, we will be talking to the Blockchain via HTTP requests. 

## Things to Download 

It's unfortunate that we can't just jump into coding without downloading resources to help us. I wish we lived in a perfect world where all the libraries and code we'd need were just already in every computer. That being said, here are things you need to download. 

Make sure the latest version of [Python](https://www.python.org/downloads/) is downloaded onto your computer. 

Additionally, make sure [pip](https://www.makeuseof.com/tag/install-pip-for-python/) is on your computer. What's pip? It's a package manager for Python - it stands for pip installs packages. 

sAlso, this is an aside, if you're a Mac user, you may want to install something called [homebrew](https://brew.sh/). It makes installing packages pretty easy - for example, in order to install python on my computer, all I had to do was type in `brew install python3`. This should also let you have pip installed automatically! 

Additionally, you'll want to install Flask and the Requests library. Apparently this can be done using the following command: `pip install Flask==0.12.2 requests==2.18.4` through terminal or command prompt. This actually gave me an error message because of the way permissions worked on the computer I was using. I fixed this by adding `sudo` (super-user-do) before pip in my command. 

Now, you're going to want an IDE (Integrated development environment), which helps software applications provide tools for software development. They're pretty neat; we're going to need one for coding in Python. I love Visual Studio or Sublime; for python specifically, people use [PyCharm](https://www.jetbrains.com/pycharm/). Now, after all this, we can finally get to Blockchain. 

## Representing a Blockchain 

Please note that this is taken from the tutorial I referenced in the beginning of the document. Now, before examining the code, let's look at what this is saying. If this is looking like an alien language, I would read a primer on Python before continuing. There are plenty online; Python is a fantastic language to learn as it's focused on readability. In fact, Python is said to be optimized to be written almost like english or pseudo-code. 

In the code below, we have a Python class. We can create this class through our terminal window actually by running the command `touch blockchain.py`. This creates a blockchain.py file in the current directory (file) that your computer's in. The .py indicates that we want a Python file. 

Cool. So now we have a Blockchain class whose constructor creates an initial empty list (to store the blockchain) and another to store transactions. Okay what does that mean. Well, classes are a way of bundling data and functionality together. Creating a new class means creating a new object, allowing new instances of that type to be made. Let's say I have a cookie class. And I want more cookies because I'm hungry. I could create multiple instances of the cookie class which would have attributes attached to it that make it a cookie but it could also have things called methods that let it be different than just... a normal cookie. So let's say I have a cookie class. We agree that Peanut Butter and Cookie Dough are instances of cookie (as they're both cookies). However, the thing that differentiates these from just a normal cookie (plain cookie) is the toppings! So we may have methods that allow us to add Peanut Butter or Cookie Dough. Hopefully that makes sense.

It may help to read up here on Python [classes](https://docs.python.org/3/tutorial/classes.html). All right, so intially we have a class called Blockchain that then has a class instantiation operation (creates an empty blockchain object). This is what's happening in the part of the code that says `def __init__(self)`. When we say `def` we are defining a function that will allow us to do things; this is fairly well commented for the code. The `@` symbol is a [decorator](https://wiki.python.org/moin/PythonDecorators), which dynamically alter the functionality of a function, method, or class without needing to change the source code. 

The tl;dr of the above is that we now have a Blockchain class responsible for managing the chain. It stores transactions and will have helper methods (functions that "belong" to an object, as mentioned previously, helping it change its attributes). This will allow us to add new blocks to the chain! So add the following to your blockchain.py file:

```python 
   class Blockchain(object):
    def __init__(self):
        self.chain = []
        self.current_transactions = []
        
    def new_block(self):
        # Creates a new Block and adds it to the chain
        pass
    
    def new_transaction(self):
        # Adds a new transaction to the list of transactions
        pass
    
    @staticmethod
    def hash(block):
        # Hashes a Block
        pass

    @property
    def last_block(self):
        # Returns the last Block in the chain
        pass
```

## New Block on the Blockchain 

So what even is a block? Well, it has a timestamp, a list of transactions, a proof (verifies a calculation), and the hash of the previous block. Let's visualize it. 

```python 
block = {
    'index': 1,
    'timestamp': 1506057125.900785,
    'transactions': [
        {
            'sender': "8527147fe1f5426f9dd545de4b27ee00",
            'recipient': "a77f5cdfa2934df3954a5c7c7da5df1f",
            'amount': 5,
        }
    ],
    'proof': 324984774000,
    'previous_hash': "2cf24dba5fb0a30e26e83b2ac5b9e29e1b161e5c1fa7425e73043362938b9824"
}
```

Legitness. So how can we think of this? So each new block contains the hash of the previous block. Therefore, we have a chain. Think of it this way. I am climbing a mountain. I decide to hook myself up to someone climbing the mountain behind me. I have their hash information (a link to them). Then, I give my hook to the person in front of me. The person in front of me is like the new blockchain, and has me attached (has my hash information, link to me). We are linked. Obviously, this is an oversimplification, I just want to get at the point that there is a chain being made. Importantly, unlike the mountain example, if a hacker changed an earlier block, all the subsequent blocks contain an incorrect hash. This is the **core idea behind blockchain**. 

## Adding Transactions to Block

We need a way to add transactions. Let's add a method (thing that lets us change our class). We do this using a new_transaction() method. Looks like this:

```python
class Blockchain(object):
    ...
    
    def new_transaction(self, sender, recipient, amount):
        """
        Creates a new transaction to go into the next mined Block
        :param sender: <str> Address of the Sender
        :param recipient: <str> Address of the Recipient
        :param amount: <int> Amount
        :return: <int> The index of the Block that will hold this transaction
        """

        self.current_transactions.append({
            'sender': sender,
            'recipient': recipient,
            'amount': amount,
        })
```

This will add a transaction to the list and return the index of the block that the transaction is added to (next block to be mined). Now, let's create new blocks like it's Minecraft. 

So, when our blockchain is created (instantiated - creating an instance of a class), we need to "seed" it with a genesis block. What does this even mean? Well, it gets really religious, but think of this like the holy block - the first block on the blockchain. It has no predecessors. It is the OG block. Now, we need to add a proof to the genesis block, which is the result of mining. 

Additionally, we need to add more methods to allow for this to even happen:

```python
import hashlib
import json
from time import time


class Blockchain(object):
    def __init__(self):
        self.current_transactions = []
        self.chain = []

        # Create the genesis block
        self.new_block(previous_hash=1, proof=100)

    def new_block(self, proof, previous_hash=None):
        """
        Create a new Block in the Blockchain
        :param proof: <int> The proof given by the Proof of Work algorithm
        :param previous_hash: (Optional) <str> Hash of previous Block
        :return: <dict> New Block
        """

        block = {
            'index': len(self.chain) + 1,
            'timestamp': time(),
            'transactions': self.current_transactions,
            'proof': proof,
            'previous_hash': previous_hash or self.hash(self.chain[-1]),
        }

        # Reset the current list of transactions
        self.current_transactions = []

        self.chain.append(block)
        return block

    def new_transaction(self, sender, recipient, amount):
        """
        Creates a new transaction to go into the next mined Block
        :param sender: <str> Address of the Sender
        :param recipient: <str> Address of the Recipient
        :param amount: <int> Amount
        :return: <int> The index of the Block that will hold this transaction
        """
        self.current_transactions.append({
            'sender': sender,
            'recipient': recipient,
            'amount': amount,
        })

        return self.last_block['index'] + 1

    @property
    def last_block(self):
        return self.chain[-1]

    @staticmethod
    def hash(block):
        """
        Creates a SHA-256 hash of a Block
        :param block: <dict> Block
        :return: <str>
        """

        # We must make sure that the Dictionary is Ordered, or we'll have inconsistent hashes
        block_string = json.dumps(block, sort_keys=True).encode()
        return hashlib.sha256(block_string).hexdigest()
  
```

## How are new blocks created or mined?

Yeah, this is a lot to take in. Blockchain is mentally taxing but it's worth it in the end - eat a snack or something, you've earned it. Now, new blocks are created or **mined** on the blockchain through a proof of work algorithm (PoW). This isn't to be confused with prisoner of war. The goal of this algorithm is to discover a number that solves a problem - it should be difficult to find but easy to verify in terms of computation. Any person on the network can work to solve this. 

Let's give an example. What if wanted to have a hash of an integer multiplifed by another integer end in 0. Let's say we fix one of the integers. If we implemented this in python, we'd get:

```python
from hashlib import sha256
x = 5
y = 0  # We don't know what y should be yet...
while sha256(f'{x*y}'.encode()).hexdigest()[-1] != "0":
    y += 1
print(f'The solution is y = {y}')
```

We get y = 21 because the produced hash ends in zero. A hash looks like some really long number with letters in it: `1253e9373e...5e3600155e860`. For BitCoin, the proof of work algorithm is called HashCash. It's pretty cash money of them. Also it's used for limiting email spam and DDoS. That's cool. It's pretty similar to the example above and it's what "miners" solve in order to create a new block; the difficulty is determined by the number of characters in a string. Miners are rewarded for their solution by recieving a coin in something called a transaction. It's like some Runescape stuff going on. The cool thing is that the network can easily verify the transaction (solution). So implementing a algorithm similarly for the blockchain tutorial, let's say we want a number p that when hashed with the previous block's solution gives us a hash with 4 leading 0s: 

```python 
import hashlib
import json

from time import time
from uuid import uuid4


class Blockchain(object):
    ...
        
    def proof_of_work(self, last_proof):
        """
        Simple Proof of Work Algorithm:
         - Find a number p' such that hash(pp') contains leading 4 zeroes, where p is the previous p'
         - p is the previous proof, and p' is the new proof
        :param last_proof: <int>
        :return: <int>
        """

        proof = 0
        while self.valid_proof(last_proof, proof) is False:
            proof += 1

        return proof

    @staticmethod
    def valid_proof(last_proof, proof):
        """
        Validates the Proof: Does hash(last_proof, proof) contain 4 leading zeroes?
        :param last_proof: <int> Previous Proof
        :param proof: <int> Current Proof
        :return: <bool> True if correct, False if not.
        """

        guess = f'{last_proof}{proof}'.encode()
        guess_hash = hashlib.sha256(guess).hexdigest()
        return guess_hash[:4] == "0000"
```

Now, obviously, you can make the algorithm more difficult by modifying the number of leading zeros. It can make a massive difference in time taken to just add another leading zero. 

