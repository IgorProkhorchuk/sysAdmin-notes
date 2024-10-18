| **Code** | **Category**           | **Explanation**                                                                                       |
|----------|------------------------|-------------------------------------------------------------------------------------------------------|
| **1xx**  | **Informational**      | **Request received, continuing process**                                                              |
| **100**  | Continue               | The server has received the request headers and the client should proceed to send the request body.    |
| **101**  | Switching Protocols    | The requester has asked the server to switch protocols, and the server has agreed to do so.            |
| **102**  | Processing             | The server is processing the request but no response is available yet.                                 |
| **103**  | Early Hints            | Primarily used with the `Link` header to allow the user agent to start preloading resources.           |
| **2xx**  | **Success**            | **The action was successfully received, understood, and accepted**                                     |
| **200**  | OK                     | The request was successful and the server returned the requested resource.                             |
| **201**  | Created                | The request was successful, and a new resource was created as a result.                                |
| **202**  | Accepted               | The request has been accepted for processing, but the processing is not yet complete.                  |
| **203**  | Non-Authoritative Info | The request was successful but the returned meta-information is from a cached or other source.         |
| **204**  | No Content             | The request was successful but there is no content to send in the response.                            |
| **205**  | Reset Content          | Tells the client to reset the document view that caused the request to be sent.                        |
| **206**  | Partial Content        | The server is delivering only part of the resource due to a range header sent by the client.           |
| **207**  | Multi-Status           | WebDAV; conveys multiple responses for multiple independent operations.                                |
| **208**  | Already Reported       | WebDAV; the resource has already been enumerated in a previous part of the response.                   |
| **226**  | IM Used                | The server fulfilled a GET request and used an instance-manipulation to return a transformed response.  |
| **3xx**  | **Redirection**        | **Further action must be taken to complete the request**                                               |
| **300**  | Multiple Choices       | The request has more than one possible response.                                                       |
| **301**  | Moved Permanently      | The requested resource has been permanently moved to a new URL.                                        |
| **302**  | Found                  | The requested resource resides temporarily at a different URL.                                         |
| **303**  | See Other              | Directs the client to retrieve the resource from another URL, typically after a POST.                  |
| **304**  | Not Modified           | Indicates that the resource has not been modified since the version specified by the request headers.   |
| **305**  | Use Proxy              | The requested resource must be accessed through the proxy given by the `Location` header.              |
| **306**  | (Unused)               | No longer used but was previously used for a proxy redirection.                                        |
| **307**  | Temporary Redirect     | Similar to 302 but ensures the method remains unchanged.                                               |
| **308**  | Permanent Redirect     | Similar to 301 but the request method must not change.                                                 |
| **4xx**  | **Client Errors**      | **The request contains bad syntax or cannot be fulfilled**                                             |
| **400**  | Bad Request            | The server could not understand the request due to invalid syntax.                                     |
| **401**  | Unauthorized           | Authentication is required, and it has failed or has not yet been provided.                            |
| **402**  | Payment Required       | Reserved for future use (often used for payment services).                                             |
| **403**  | Forbidden              | The server understood the request but refuses to authorize it.                                         |
| **404**  | Not Found              | The server could not find the requested resource.                                                      |
| **405**  | Method Not Allowed     | The request method is known by the server but is not supported for the requested resource.             |
| **406**  | Not Acceptable         | The server cannot produce a response matching the Accept headers sent in the request.                  |
| **407**  | Proxy Authentication Required | The client must authenticate with the proxy before sending the request.                               |
| **408**  | Request Timeout        | The server timed out waiting for the request.                                                          |
| **409**  | Conflict               | The request could not be completed due to a conflict with the current state of the resource.           |
| **410**  | Gone                   | The requested resource is no longer available and will not be available again.                         |
| **411**  | Length Required        | The request did not specify the length of its content, which is required by the server.                |
| **412**  | Precondition Failed    | The server does not meet one of the preconditions that the requester put on the request.               |
| **413**  | Payload Too Large      | The request is larger than the server is willing or able to process.                                   |
| **414**  | URI Too Long           | The URI provided was too long for the server to process.                                               |
| **415**  | Unsupported Media Type | The request entity has a media type which the server or resource does not support.                     |
| **416**  | Range Not Satisfiable  | The client asked for a portion of the file (byte serving), but the server cannot supply that portion.  |
| **417**  | Expectation Failed     | The server cannot meet the requirements of the Expect request-header field.                            |
| **418**  | I'm a teapot           | Defined in RFC 2324, returned by teapots when asked to brew coffee (joke response).                    |
| **421**  | Misdirected Request    | The request was directed to a server that cannot produce a response.                                   |
| **422**  | Unprocessable Entity   | WebDAV; the server understands the content type but is unable to process the instructions.             |
| **423**  | Locked                 | WebDAV; the resource that is being accessed is locked.                                                 |
| **424**  | Failed Dependency      | WebDAV; the request failed because of a failure of a previous request.                                 |
| **425**  | Too Early              | The server is unwilling to risk processing a request that might be replayed.                           |
| **426**  | Upgrade Required       | The client should switch to a different protocol.                                                      |
| **428**  | Precondition Required  | The server requires the request to be conditional.                                                     |
| **429**  | Too Many Requests      | The user has sent too many requests in a given amount of time ("rate limiting").                       |
| **431**  | Request Header Fields Too Large | The server is unwilling to process the request because its header fields are too large.          |
| **451**  | Unavailable for Legal Reasons | The server is denying access to the resource as a consequence of a legal demand.                     |
| **5xx**  | **Server Errors**      | **The server failed to fulfill a valid request**                                                       |
| **500**  | Internal Server Error  | The server encountered an unexpected condition that prevented it from fulfilling the request.          |
| **501**  | Not Implemented        | The server does not support the functionality required to fulfill the request.                         |
| **502**  | Bad Gateway            | The server, while acting as a gateway or proxy, received an invalid response from the upstream server. |
| **503**  | Service Unavailable    | The server is not ready to handle the request, often due to maintenance or overload.                   |
| **504**  | Gateway Timeout        | The server was acting as a gateway or proxy and did not receive a timely response from the upstream.   |
| **505**  | HTTP Version Not Supported | The server does not support the HTTP version used in the request.                                  |
| **506**  | Variant Also Negotiates | The server has an internal configuration error.                                                       |
| **507**  | Insufficient Storage   | WebDAV; the server is unable to store the representation needed to complete the request.               |
| **508**  | Loop Detected          | WebDAV; the server detected an infinite loop while processing a request.                               |
| **510**  | Not Extended           | Further extensions to the request are required for the server to fulfill it.                           |
| **511**  | Network Authentication Required | The client needs to authenticate to gain network access.                                         |

