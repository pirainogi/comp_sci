## Cookies
- Small files stored on a user’s computer (4 kb)
- Hold modest amount of data specific to a particular client and website
- Can be accessed by the web server or the client computer
- Server delivers a page tailored to a particular user

## HTTP Protocol
#### Hypertext transfer protocol
- Underlying protocol used by the world wide web
  -  Defines how messages are formatted and transmitted
- Language that browsers speak
  - every time you load a web page, you are making an HTTP request to the site’s server
  - server sends back an HTTP response
- When the client makes a request it includes `headers`
  - contains all of the information that the server needs in order to fulfill the request
    - the type of request
    - the resource (path)
    - the domain
    - other metadata like what type of browser is making the request

### URI
- When you make a request on the web, you send it through **Uniform Resource Identifiers**
- Broken into three parts
  - the protocol
    - the way that we are sending our request
  - the domain
    - characters that identify the unique location of the web server that hosts that particular website
  - the resource
    - particular part of the website that we want to load

### HTTPS
- secure version

### Verbs
- HEAD
- GET
- POST
- PUT
- DELETE
- TRACE
  - echoes back the received request
- OPTIONS
  - returns the HTTP methods that the server supports
- CONNECT
  - Converts the request to a TCP/IP tunnel for SSL
- PATCH

### Dynamic
- sites that change based on user input
