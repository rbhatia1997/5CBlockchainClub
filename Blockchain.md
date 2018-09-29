# Introduction to Blockchain

## Very Basic Fundamentals of Blockchain 
This part of the tutorial is heavily influenced by the following [link](https://hackernoon.com/learn-blockchains-by-building-one-117428612f46). Now, what is Blockchain? It's an immutable (not changeable), sequential chain of records. Such records are called **blocks.** They contain transactions or any type of data you want to store in them. They're linked together using hashes. 

### What are Hashes?
This part of the tutorial is heavily influenced by the following [link](https://learncryptography.com/hash-functions/what-are-hash-functions). A hash function takes an input value, and from the input value, creates an output determined on what the input value is. 

To make this easier, consider a simple function: y = f(x). A function will take an input, x, and give out the output (y) based on the input x. Now, a *hash function* takes an input (which doesn't necessarily need to be a number) and outputsa hash. For example, if I were to input "hello" into a function called md5, I would get a long list of hexadecimal output (e.g. `5eb63bbe01eeeed093cb22bb8...`).Most hashes are displayed as hexadecimal output. Importantly, the hash function in this case (md5) output a 32-character long hexdecimal output. 

Now, hash functions generally are one-way or irreversible (hmm.. there may be a reason why we would consider them for blockchain [see: immutable]). Therefore, we can actually use such functions to prove that something is the same as another thing without revealing the information beforehand. 

A good example is that if I have the answer to how many Jellybeans are in a jar in my room and I want to challenge my friends to get the correct answer, I can make sure that they won't cheat by asking them to compare the hash that they receive from their answer to a hash that I give them. I can run the answer througha hash function to recieve that hash. Hashes are often used in the context of verifying information without revealing it to the people who are verifying. 

##  
