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