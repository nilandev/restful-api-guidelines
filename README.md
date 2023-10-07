# RESTful API Design Best Practices

REST (Representational State Transfer) is a software architectural style that has become the de-facto standard for building API-driven applications. Some of the key characteristics of RESTful API's include:

* Client-server architecture: REST APIs are typically designed using a client-server architecture, where the client is responsible for making requests to the server and the server is responsible for responding to those requests.
* Statelessness: REST APIs are stateless, meaning that each request is independent of any other request. This makes REST APIs easier to scale and more resilient to failures.
* Cacheability: REST APIs typically return cacheable responses, which means that the client can store the responses and reuse them for subsequent requests. This can improve performance and reduce bandwidth usage.
* Layered system: REST APIs are typically designed as a layered system, where each layer is responsible for a specific task. This makes REST APIs easier to develop and maintain.
* Uniform interface: REST APIs use a uniform interface, which means that they use a consistent set of HTTP methods and URIs to perform different operations. This makes REST APIs easier to learn and use.

## 🥇 API Design Best Practices
* Use HTTP Methods Properly.
* Use Proper HTTP Status Codes
* Consistent design and using appropriate resource schema
* Implement HATEOAS
* API Versioning
* Pagination, Filtering and Searching
* Standard Error handling practices
* Documentation

## :key: API Security Guidelines
Checklist of the most important security countermeasures when designing, testing, and releasing your API.

## Authentication
- Don't use `Basic Auth` Use standard authentication (e.g. JWT, OAuth).
- Don't reinvent the wheel in `Authentication`, `token generating`, `password storing` use the standards.
- Use OAuth 2.0. It is the industry-standard protocol for authorization works for web, desktop, or mobile applications. Read more about OAuth 2.0 [here](https://oauth.net/2/).

### JWT (JSON Web Token)
- Use a random complicated key (`JWT Secret`) to make brute forcing tokens very hard.
- Don't extract the algorithm from the payload. Force algorithm in the backend (`HS256` or `RS256`). 
- Make token expiration (`TTL`, `RTTL`) as short as possible.
- Don't store sensitive data in the JWT payload, it can be decoded [easily](https://jwt.io/#debugger-io).

### OAuth
- Always validate `redirect_uri` on the server side to allow only whitelisted URLs.
- Always try to exchange for code not tokens (don't allow `response_type=token`).
- Use `state` parameter with a random hash to prevent CSRF on the OAuth authentication process.
- Define default scope, and validate scope parameters for each application. 

## Access
- Limit requests (Throttling) to avoid DDoS / Bruteforce attacks.
- Use HTTPS on the server side to avoid MITM (Man In The Middle Attack).
- Use `HSTS` header with SSL to avoid SSL Strip attack.

## Input
- Use proper HTTP method according to operation, `GET (read)`, `POST (create)`, `PUT (replace/update)` and `DELETE (to delete a record)`.
- Validate `content-type` on request Accept header ( Content Negotiation ) to allow only your supported format (e.g. `application/xml` , `application/json` ... etc) and respond with `406 Not Acceptable` response if not matched.
- Validate `content-type` of posted data as you accept (e.g. `application/x-www-form-urlencoded` , `multipart/form-data ,application/json` ... etc ).
- Validate User input to avoid common vulnerabilities (e.g. `XSS`, `SQL-Injection` , `Remote Code Execution` ... etc).
- Don't use any sensitive data ( `credentials` , `Passwords`, `security tokens`, or `API keys`) in the URL, but use standard Authorization header.

## Processing
- Check if all endpoints are protected behind the authentication to avoid broken authentication.
- User's own resource ID should be avoided. Use `/me/orders` instead of `/user/654321/orders`
- Don't use auto-increment ID use `UUID` instead.
- If you are parsing XML files, make sure entity parsing is not enabled to avoid `XXE` (XML external entity attack).
- If you are parsing XML files, make sure entity expansion is not enabled to avoid `Billion Laughs/XML bomb` via exponential entity expansion attack.
- Use CDN for file uploads.
- If you are dealing with a huge amount of data, use Workers and Queues to return responses fast to avoid HTTP Blocking. 
- Do not forget to turn the DEBUG mode OFF.

## Output
- Send `X-Content-Type-Options: nosniff` header.
- Send `X-Frame-Options: deny` header.
- Send `Content-Security-Policy: default-src 'none'` header.
- Remove fingerprinting headers - `X-Powered-By`, `Server`, `X-AspNet-Version` etc.
- Force `content-type` for your response, if you return `application/json` then your response `content-type` is `application/json`.
- Don't return sensitive data like `credentials`, `Passwords`, or `security tokens`.
- Return the proper status code according to the operation completed. (e.g. `200 OK` , `400 Bad Request` , `401 Unauthorized`, `405 Method Not Allowed` ... etc).

## Contribution
Feel free to contribute, :octocat:	fork -> edit -> submit pull request.
