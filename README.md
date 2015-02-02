# Lecture Notes for Data Engineering w/ Ken Anderson

###[GitHub Repo](https://github.com/cu-data-engineering-s15)

# Lecture 1 - 1/13/15

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




















# Lecture 3 - 1/20/15

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










# Lecture 5 - 1/22/15

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



















# Lecture 5 - 1/27/15

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

















*Lecture 6 - 1/29/15

### Express
* Web application framework written in javascript for use in Node.js

#### Express example 
* In class demo...





