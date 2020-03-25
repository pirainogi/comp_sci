#REST
* **REST**: REpresentational State Transfer
* architectural style for providing standards btw computer systems on the web.
  * easier for systems to communicate with each other
* REST-compliant systems are characterized by how they are stateless and separate the concerns of client and server

## Separation of Client and Server
* implementation of client and server can be independent without knowing each other
* code on the client side can be changed at any time without affecting the operation of the server
* code on the server side can be changed without affecting the operation of the client
* only need to know the format of messages to send to the other
* improved flexibility of the interface and improve scalability by simplifying the server components
* evolve independently

## Statelessness
* Server doesn't need to know what state the client is in and vice versa
* can understand the current message without needing to know the previous messages
* constraint of statelessness is enforced through using _resources_, not _commands_
  * nouns of the web: describe any object, document, or thing you may need to store or send to other services
  * do not rely on the implementation of interfaces
* reliable, quick performance, and scalability
  * components can be managed, updated, and reused without affecting the system as a whole

# Communication Between Client and Server

## Making Requests
* Client makes a request to the server to retrieve or modify data
  * HTTP verb
  * header
  * path
  * optional message

### HTTP Verbs
* GET
  * retrieve a specific resource or a collectioon of resources
* POST
  * create a new resource
* PUT/PATCH
  * update a specific resource
* DELETE
  * remove a specific resource

### Headers/Accept Parameters
* header: client sends the type of content that it is able to receive from the server
  * `Accept` field
  * ensures the server doesn't send data that can't be understood/processed by the client
* options for types of content are MIME (Multipurpose Internet Mail Extensions) Types
  * used to specify the content types in the `Accept` field
  * consists of a `type` and a `subtype` separated by a /
    * common types/subtypes:
      * `text`: `text/plain`, `text/html`, `text/css`
      * `image`: `image/png`, `image/jpeg`, `image/gif`
      * `audio`: `audio/wav`, `audio/mpeg`
      * `video`: `video/mp4`, `video/ogg`
      * `application`: `application/json`, `application/pdf`, `application/xml`, `application/octet-stream`

### Paths
* Requests must contain a path to a resource that the operation should be performed on
  * in RESTful APIs, paths should be designed to help the client know what is going on
* first part of the path should be the plural form of the resource
* should contain information necessary to locate a resource with the degree of specificity needed

## Sending Responses

### Content Types
* When the server is sending a data payload to the client, the server must include a `content-type` ini the header of the response
* alerts the client to the type of data it is sending in the body 
  * MIME Types again

### Response Codes
* Responses from the server contain status codes to alert the client to information about the success of the operation
* most common:
  * 200 (OK): successful HTTP request
    * GET and PATCH
  * 201 (CREATED): successful HTTP request that made an item
    * POST
  * 204 (NO CONTENT): successful HTTP request  where nothing is returned in the body
    * DELETE
  * 400 (BAD REQUEST): request cannot be processed because of bad request syntax, excessive size, or other client error
  * 403 (FORBIDDEN): don't have permission to access this resource
  * 404 (NOT FOUND): resource could not be found; could have been deleted or doesn't exist yet
  * 500 (INTERNAL SERVER ERROR): unexpected failure if no more specific information available



Source: !(rest)[https://www.codecademy.com/articles/what-is-rest]
