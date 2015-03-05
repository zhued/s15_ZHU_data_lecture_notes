# Lecture Notes for Data Engineering w/ Ken Anderson

###[GitHub Repo](https://github.com/cu-data-engineering-s15)

# [Lecture 1 - 1/13/15](http://cu-data-engineering-s15.github.io/lecture_01/)

Anderson is asking us to make this as a first assignment. I'm excited for the class.

####General Flow of Class:

Thursday:
- New Area
- Intro
- Looking up frameworks

Tuesday:
Presentations

####Data analytics
  - Sampling ... Machine Learning
  - Statistics largely based on sampling. If you already know the answer, not really statistics.

#### Storage
  - Data modeling is very hard - i.e. data formatting in facebook. New posts will have a different format than the old posts. They wont convert the old posts into the new data type.
  - NoSQL
    - Graph
    - Key-Value Stores
    - Columnar

####Twitter
  - Twitter Clients -> Twitter <- Tweet
  - Sometimes twitter clients use different encoding than utf-8 
  - Twitter uses utf-8
  - End tweet is half utf-8 and half different encoding (hard to perform analytics on)
    - i.e. python would expect it to be all utf-8, blows up if different

####Info Viz
  - D3 (visualiztion - graphs)
  - excel / R (data analysis)

####Data Lifecycle
0. Question
  * Curation / Triage Persistence  - prioritization of data sources
  * Which source will give me the answer?
1. Collection / Generation
2. Cleanup
3. Storage
4. Processing / Analysis
5. Query / visualize / ACT (data transformed to knowledge we can act upon)
  * This usually gives you new questions

This lifecycle is in many startup companies that do big data
Teams of people within each step.


####Request Response Cycle
http://
http request methods
  * GET
  * POST
  * PUT
  * DELETE

Some request comes out, associated with url
server recieves url maps request to file and returns back a response


















# Lecture 2 - 1/15/15

#### Markup
Type of Markup Language

Two Types:
 * Standard Markdown (SM)
 * GitHub Flavored Markdown (GFM)

##### What Can I Do With Markdown
 * Style, word formatting
 * Images, Links
 * Code Blocks

#### Review
Web Browser --> Web Server, Map Server --> handler (usually separate entity)

#### REST - Representation State Transfer
* Resources 
  - URI (URL is a subclass of URI)
  - CRUD
    - Create
    - Read
    - Update
    - Destroy

#### HOMEWORK
DATABASE?

ids? input and output and ERRORS??




















# [Lecture 3 - 1/20/15](http://cu-data-engineering-s15.github.io/lecture_03/)

##Restful Web Services
* Architectural style for web services
  - Invented by Roy Fielding
* Approach to developing web services
* Service provides access to a linked set of resources
* For each resource you can perform operations on it simliar to the main operations

#### API Examples
```javascript
GET /api/1.0/users
//Retrieve list of users

GET /api/1.0/users/0
//Retrieve details of user 0

POST /api/1.0/users
//create a new user
```
* /api/1.0 is convention so that you can update your api
  * i.e. /api/1.1/users
  * keep your other api url running for transition

```javascript
PUT /api/1.0/users/0
Update user 0

DELETE /api/1.0/users/0
Delete user 0

GET /api/1.0/search?q=tattersail
Perform a search with the query tattersail.
```

#### Discussion - Request Response cycle
* Each operation may produce a result - Synchronously
  * With RESTful services, JSON format is king
* JSON - highly compressible
* Asynchronously - Use AJAX calls.
* POST and PUT methods typically send data
  * Also in JSON format
  * May be in the URL or in the body of the HTTP Request
    * GET, data may appear as query params
* Other formats are possible: HTML and XML are typical
* If a request needs to be authenticated
  * the authentication data appears in HTTP headers
  * i.e. used for DELETE - dont want just anyone to be able to delete users

#### Discussion - How do you think operations on two resources are handled?
```javascript
GET /api/1.0/posts/0/comments/1
Get the first comment on post 0

POST /api/1.0/posts/0/comments
Create a new comment on post 0
```

#### Issues
* Security: How do you authenticate users?
* Identity: How are ids assigned to resources?
* Failure: How do we handle failure sitatuions?
  * In example, handle it in JSON
  * Could have used http status codes
  * Most services use combination of both
* Persistence: How are resources stored?

#### EXAMPLE
* Contacts web service
* implemented in both ruby and javascript
* technologies used:
  * Sinatra
  * Rspec - Ruby testing
  * Typhoeus - http requests (libcurl wrapper)
  * Node - wrapper around chrome js engine (v8)
  * Express - alike sinatra


```ruby
def handle_request(method, uri, data = nil)
    url      = "#{base_uri}/#{uri}"
    info     = { "Content-Type" => "application/json" }
    params   = {method: method, body: data, headers: info }
    request  = Typhoeus::Request.new(url, params)
    request.run
    response = request.response

    raise NotConnected if response.code == 0 # not connected
    if response.code == 200 # successful request response cycle
      result = JSON.parse(response.body) 
      #puts result.inspect
      if result["status"]
        yield result["data"]
      else
        raise FailureResult.new(result["error"])
      end
    else
      raise NotOk
    end
    raise ServiceError
  end
```

















# Lecture 4 - 1/22/15

#### Git Presentation
* Stages of file: Untracked, Unmodified, Modified, Staged, Remote
* git
  * init - initialize
  * clone - clone a repo
  * branch - new branch
  * checkout - move into another branch
  * add - add files
  * commit - commits stuff
  * merge - merge a branch with another branch
* Resolve Conflicts
  * find conflicts
  * <<<<< start
  * ===== differnces
  * >>>>> end of conflicts

#### GitHub Presentation
* Pull requests are new for GitHub
* Forking creates repo under your own head
* Cloning create repo with collaborators of that repo community























# [Lecture 5 - 1/27/15](http://cu-data-engineering-s15.github.io/lecture_05/)

####NODE.JS
* Most code in node is pacckaged inside of a module
* http is a core module, provided by Node itself
* npm (node package manager) - gives access to extend node

```javascript
// Load the http module to create an http server.
var http = require('http');

// Configure our HTTP server to respond with Hello World to all requests.
var server = http.createServer(function (request, response) {
  response.writeHead(200, {"Content-Type": "text/plain"});
  response.end("Hello World\n");
});

// Listen on port 8000, IP defaults to 127.0.0.1
server.listen(8000);

// Put a friendly message on the terminal
console.log("Server running at http://127.0.0.1:8000/");
```




























# [Lecture 6 - 1/29/15](http://cu-data-engineering-s15.github.io/lecture_06)

### Express
* Web application framework written in javascript for use in Node.js

#### Express example 
* In class demo...


























# [Lecture 7 - 2/3/15](http://cu-data-engineering-s15.github.io/lecture_07/)

### AngularJS

Client-side web application framework written in Javascript for use in most web browsers

### Core Concepts
* Data Binding
  * The value of an HTML tag can be associated with a model object. When one changes, Angular updates the other automatically.
* Controllers
  * State and methods that can be accessed within that section of the page
  * Can modularize your web app and decompose data and functionality into small, manageable chunks

* Services
* Directives
* Embeddeble
* Injectable



























# [Lecture 8 - 2/5/15]()
















# [Lecture 9 - 2/10/15](http://cu-data-engineering-s15.github.io/lecture_09/)


### this Keyword
* the value of this is determined on how you call it.
* implicit binding, explicit binding, etc.

### requireJS
* kicks off loading of app specific code
* requireJS then starts to look at dependencies and starts to execute them in order
* requireJS can configure things like:
  * bootstrap
  * angular
  * ngRoute
  * jQuery
* requireJS also lets you load js that you wrote such as:
  * routes.js
  * /controllers
  















# [Lecture 10 - 2/12/15](http://cu-data-engineering-s15.github.io/lecture_10/)

## Twitter - Consumer Keys, Access Tokens
* OAuth allows app to act on behalf of users 
  * i.e. post tweets etc
* Might ship your application with consumer keys.
* When user launches app, send them to twitter to login and grant access
* Twitter will then send an access token/secret for application to store on behalf
















  
# [Lecture 11 - 2/17/15](http://cu-data-engineering-s15.github.io/lecture_11/)


## TwitterRequest 
* is the top level class of a tweet
* contains helpers:
  * logging
  * rates
  * params
  * props

#### Contract
* TwitterRequest has a public collect method that yields data back to its caller.
* Subclasses of twitterequest need:
  * url 
  * request_name
  * twitter_endpoint -> rate limits
  * success -> handler for successful response for twitter
* Subclasses may implement:
  * error
  * authorization

#### Rates
* ensures that rates are checked on each request
```ruby
def make_request
  check_rates
  request = Typhoeus::Request.new(url, options)
  log.info("REQUESTING: #{request.base_url}?#{display_params}")
  response = request.run
  @rate_count = @rate_count - 1
  response
end

def check_rates
  refresh_rates if @@rates.size == 0
  refresh_rates if Time.now > twitter_window
  return if @rate_count > 0
  delta = twitter_window - Time.now
  log.info "Sleeping for #{delta} seconds"
  sleep delta
  refresh_rates
end
```




































# [Lecture 12 - 2/17/15](http://cu-data-engineering-s15.github.io/lecture_12/)

## Web Analytics Application - Scaling Problems
* Problem: Can't keep up with write demand, which affects read requests
* Not a perfect solution: Batch updates to database after getting some amount requests. 
  * Add a queue between web server and a database. Attach a signle worker to queue and that will start working on the queue.
  * Problem -> even if you have 20 different workers you still have a bottleneck, the database. It cannot handle the load that the workers want to do.
* Not a perfect solution: Vertically scaling -> will fail at some point and takes a lot of money.
  * Doesn't solve underlying problem i.e. one machine that is the bottle neck
* In relational world -> to solve, shard the databse.
  1. need multiple copies of the database 
  2. then partition your data across those databases with a partition strategy
    * Often take an Md5 hash of some aspect of the input data and then mod that value by the number of shards
    * Then write data to indicated shard
    * Do the same thing for reads to locate the data needed to fill request
  3. NOTE: need a good hash function that distributes the reads and writes evenly
* Problems:
  * Sharding is application level -> you have to manage number of shards
  * If shards changes, have to remap entire db and turn your app off.
  * if you make a mistake when resharding, takes time to fix.

## NoSQL to the rescue
* NoSQL db avoid mutable data
  * Can't lose correct data because once written, it is immutable and cant be updated
  * if a val changes write a new immutable copy
* Fault tolerance
  * if disk error occurs, NoSQL db switches to its replica automatically
  * reshards db automatically
  * when old machine comes back and it reshards again.
  * can expect performance to go down while rebalancing occurs

## Types of NoSQL DBs
* Key Value
* Graphs
* Columnar
* Documents

#### Key Value
* Key value is a simple database that when presented with a string (key) returns an arbitrarily large set of data (value)
* Have no query language. Just act like hash tables.
* Vals are untyped, you can store any type of data in these databases
* Benefits -> simplicity

#### Graph Stores
* store graph structures rather than table/row/column
* probide structural query languages
  * examples: find all pairs of person nodes who have at least 3 children together, live in CO, married more than 15 years
* provide ability to do graph traversals efficiently
* Examples -> Neo4J, Titan, Infinite Graph, Info Grid

#### Columnar Store
* Column family stores
* able to scale to enormous amounts of data
* often able to achieve very fast writes, while also maintaining reasonable read performance
  * Column Family: table of related data
  * Colum families consist of rows that have unique row keys
  * Rows consist of columns (potentially millions of them)
  * Columns consist of a key and a value
  * Value itself might be a JSON map that in turn has keys and values
* Hash tables all the way down
* tries its best to keep a whole row on disc so that its a single stream -> only thing holding it down network latency and disc latency

#### Document stores
* Like key-value but a little more structure
* insert documents ( a bag of key-value pairs )
* each document gets indexed in a variety of ways
* docs can be found via queries on any attr
* documents can be grouped into collecitons
* collections can be grouped into databases
* Each database is then used by a particular applicaiton to get its work done






























# [Lecture 13 - 2/17/15](http://cu-data-engineering-s15.github.io/lecture_13/)

## CouchDB
* Document Database
  * Implemented in Erlang. Lot of use in telecommunications
  * Massive concurrency, fault tolerance, distributed systems
  * All of these features are on display in the design of CouchDB
* CouchDB's design embraces the web
  * High availability trades consistency for EVENTUAL consistency

#### Document Model
* Document databases: self-contained data
* CouchDB stores documents
* Each document contains everything that might be needed by an application.
  * Avoid foreign keys etc, each document meant to stand on its own.
  * Usually no references
* No schema enforced, each document can have a different set of attributes

#### CAP Theorem - PICK 2
* Consistency -> All clients see the same data even in the presence of concurrent updates.
* Availability -> All clients able to read or write the data store when they want
* Partition Tolerance -> DB can be split across multiple servers

#### Choices
1. Consistency and Availability -> what relational dbs provide, low partition tolerance.
2. Availiability and Partition Tolerance -> Provides the ability to scale horizontally and always be abailible for requests. 
  * Can only guarantee eventual consistency
  * 3 clients issue same query and get different results -> can design around this
  * i.e. don't really need total consistency all the time (facebook likes)
3. Consistency and Partition Tolerance -> provide consistency across multiple dbs, but not always available for client requests 

**Couch DB choose the second option**

#### Specifics
* CouchDB uses B-tree storage engine.
  * allows searches, insertions, and deletions in log time.
* Employs MapReduce over B-Tree to compute _views_ of the data allowing for parallel and incremental computation.
* No Locking
  * same idea that git uses -> multiple users can edit a repo.
  * Each read of a doc returns a version of the document that was the latest when read started
  * document can be written while it is being read, the next read will then return the new document
* Validation -> validation functions can be written in javascript
  * Each time an update for a document is submitted the proposed change is passed to the validation function
  * the validation function then chooses to accept or deny the update
* Merge Conflicts
  * Can encounter merge conflicts.










































# Lecture 14 - 2/17/15

## MongoDB Student Presentation
































# [Lecture 16 - 3/5/15](http://cu-data-engineering-s15.github.io/lecture_16/)

## MongoDB Specifics

