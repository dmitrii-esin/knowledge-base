# Mastering RESTful API Design: A Practical Guide

RESTful API (Representational State Transfer API) is a network interface design style used for interactions between network applications. REST is a set of architectural principles and constraints rather than a standard or protocol. When a web service is "RESTful," it follows REST principles and provides an efficient, reliable, and scalable network service.

In a RESTful service, each request should contain all the necessary information to process the request. The server should not retain any state information about client requests.

A RESTful architecture may consist of multiple layers, each performing a specific function. This structure allows for the development of more complex and powerful applications.

## URI Design
In RESTful API design, URLs (Uniform Resource Locators) typically represent resources (objects), while HTTP methods (such as GET, POST, PUT, DELETE, etc.) represent operations on these resources (verbs). This design style emphasizes the state and representation of resources rather than actions.

## Verb + Object
Verbs in RESTful APIs are usually the five HTTP methods, corresponding to CRUD operations:
```
GET: Read
POST: Create
PUT: Update
PATCH: Update (typically for partial updates)
DELETE: Delete
```
According to the HTTP specification, verbs should always be in uppercase.

## The Object Must Be a Noun
When designing an API, the URL (Uniform Resource Locator) usually represents a resource that serves as the object of an HTTP verb. According to RESTful design principles, URLs should be nouns rather than verbs because they represent a "resource" collection or a single instance, not an action.

Incorrect Examples:
```
/getAllCars
/createNewCar
/deleteAllRedCars
```
These URLs include verbs (such as get, create, delete), which describe actions rather than the resources themselves. This design does not conform to RESTful semantic standards.

Correct Approach:
URLs should focus on describing resources rather than operations. Below are examples of compliant URL designs:

```
/users: Represents a collection of users
/users/123: Represents a single user with a specific ID (123)
```
In the above examples, /users and /users/123 are both nouns, representing a collection of users and a specific user resource, respectively. Such URL design makes APIs easier to understand and aligns with RESTful resource-oriented principles.

By following this naming convention, we ensure that API paths are clear, consistent, and easy to understand and maintain.

## Plural URLs
Using plural form in URLs is generally recommended for consistency and clarity, as they typically represent collections of resources.

When your URL points to a collection of resources, use plural nouns. For example, use /users instead of /user to represent a collection of all users.

Even when pointing to a single resource, using the plural form is recommended. For example, /users/123 represents the user with ID 123. This approach maintains URL consistency.

When resources have hierarchical relationships, the URL should reflect this structure. For example, /users/123/posts can represent the collection of posts for user 123.

## Avoid Deeply Nested URLs
A common scenario is when resources require multiple levels of classification, leading to deeply nested URLs, such as retrieving a certain category of articles by a specific author:

```
GET /authors/12/categories/2
```
Such URLs are difficult to extend, and their semantics are unclear, often requiring extra effort to understand. A better approach is to use query parameters beyond the first level:

```
GET /authors/12?categories=2
```
Another example is querying published articles. You might design the URL like this:

```
GET /articles/published
```
However, using query parameters is clearly a better approach:

```
GET /articles?published=true
```

## Status Codes
Status Codes Must Be Precise
For every client request, the server must respond with an HTTP status code and data.

An HTTP status code is a three-digit number divided into five categories:

```
1xx: Informational
2xx: Success
3xx: Redirection
4xx: Client Errors
5xx: Server Errors
```
These five categories contain over 100 status codes covering most possible situations. Each status code has a standard (or conventionally accepted) meaning, allowing the client to determine what happened just by checking the status code. Therefore, the server should return the most precise status code possible.

APIs do not need 1xx status codes. Below is an explanation of the other four categories.

### 2xx Status Codes
Different HTTP request methods should return corresponding status codes to indicate the request result. While 200 OK is a general success response, more precise status codes should be used depending on the method:

```
GET: 200 OK – The request was successful, and the resource is returned.
POST: 201 Created – A new resource was successfully created, and the response typically includes the resource's URI.
PUT: 200 OK or 204 No Content – Used for full resource updates. If content is returned, use 200; if not, use 204.
PATCH: 200 OK or 204 No Content – Used for partial updates, similar to PUT. 204 indicates no content returned.
DELETE: 204 No Content – Indicates the resource was successfully deleted, usually with no content in the response.
202 Accepted – The request has been accepted but not yet processed, useful for asynchronous operations.
206 Partial Content – Indicates a partial response, commonly used when a client requests part of a large file using the Range header.
```

### 3xx Status Codes
APIs typically do not use 301 (Permanent Redirect) or 302 (Temporary Redirect, including 307) since they are mostly relevant for browser-level navigation. APIs can handle such scenarios at the application level instead.

However, APIs may use 303 See Other, which references another URL. Like 302 and 307, it means "temporary redirect," but 303 is used specifically for POST, PUT, and DELETE requests. Unlike 302, browsers do not automatically follow a 303 redirect but instead allow the user to decide the next step.

Example response:

```
HTTP/1.1 303 See Other
Location: /api/orders/12345
4xx Status Codes
4xx status codes indicate client errors. Common ones include:
```

```
400 Bad Request – The server does not understand the client's request and does not process it.
401 Unauthorized – The user did not provide authentication credentials or failed authentication.
403 Forbidden – The user authenticated successfully but lacks permission to access the resource.
404 Not Found – The requested resource does not exist or is unavailable.
405 Method Not Allowed – The user authenticated successfully but is using an HTTP method that is not allowed.
410 Gone – The requested resource has been permanently removed.
415 Unsupported Media Type – The requested format is not supported. For example, if the API only returns JSON, but the client requests XML, this status should be returned.
422 Unprocessable Entity – The client provided an attachment that could not be processed, resulting in a failed request.
429 Too Many Requests – The client has exceeded the allowed number of requests.
5xx Status Codes
5xx status codes indicate server errors. APIs generally do not expose internal server details to users, so only two status codes are 
commonly used:
500 Internal Server Error – The client request was valid, but the server encountered an unexpected issue while processing it.
503 Service Unavailable – The server is temporarily unable to process requests, often used during maintenance periods.
```

## Server Responses
Do Not Return Plain Text
API responses should not be plain text but structured JSON objects to ensure a standard format. The server's Content-Type header should be set to application/json.

The client should also specify that it accepts JSON responses by setting the Accept header in its request:
```
GET /orders/2 HTTP/1.1
Accept: application/json
```
Do Not Return a 200 Status Code for Errors
An incorrect approach is to always return 200 OK, even when an error occurs, and include the error details in the response body. This forces the client to parse the response body to determine whether the request failed, undermining the purpose of status codes.

Bad Example:
```
HTTP/1.1 200 OK
Content-Type: application/json
{
  "status": "failure",
  "data": {
    "error": "Expected at least two items in list."
  }
}
```
In this case, the request failed, but the server still returned 200 OK. The client has to check the "status": "failure" field in the response body to detect the error. This approach is not RESTful and makes error handling more complex and error-prone.

Correct Example:
The status code should indicate the result of the request. Errors should be conveyed using the appropriate status codes while the response body provides more details.

For example, if the request is invalid, the server should return 400 Bad Request, with error details in JSON format:

```
HTTP/1.1 400 Bad Request
Content-Type: application/json
{
  "error": "Invalid payload.",
  "detail": {
    "surname": "This field is required."
  }
}
```

Here, 400 clearly indicates an invalid request, while the response body provides specific error details to help the client understand the issue.

## Providing Links
In RESTful APIs, including links in responses is a common practice. This follows the Hypermedia as the Engine of Application State (HATEOAS) principle, which enhances API discoverability and self-descriptiveness.

Here are two common ways to include links:

Using HAL (Hypertext Application Language)
HAL is a popular hypermedia format that represents relationships between resources. It uses the _links field in JSON responses:
```
{
  "id": 1,
  "name": "Example",
  "_links": {
    "self": {
      "href": "http://api.example.com/resource/1"
    },
    "related": {
      "href": "http://api.example.com/resource/2"
    }
  }
}
```
Embedding Links Directly in JSON
```
{
  "id": 1,
  "name": "Example",
  "links": {
    "self": "http://api.example.com/resource/1",
    "related": "http://api.example.com/resource/2"
  }
}
```

## Content Return Policies
In RESTful API design, POST requests are used to create new resources. Whether the response should include the newly created resource depends on implementation needs. There are two common approaches:

### 1. Return the Created Resource
This approach includes a 201 Created status code and the full details of the new resource in the response. It also includes a Location header pointing to the resource’s URI.

```
HTTP/1.1 201 Created
Location: /resources/123
Content-Type: application/json
{
  "id": 123,
  "name": "New Resource"
}
```

### 2. Do Not Return Content
Alternatively, the server may choose to return only a 201 Created or 204 No Content response with a Location header, omitting resource details. This minimizes data transfer and lets the client decide whether to retrieve the resource later.

```
HTTP/1.1 201 Created
Location: /resources/123
```

## Conclusion
RESTful APIs follow the HTTP protocol, emphasizing resource representation and stateless interactions. By using standard HTTP methods (GET, POST, PUT, DELETE) and precise status codes, RESTful architectures provide a simple, efficient, and easy-to-maintain way to build network applications. This approach enhances scalability, flexibility, and maintainability for web services.