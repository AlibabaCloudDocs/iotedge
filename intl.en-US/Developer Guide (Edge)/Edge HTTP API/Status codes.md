# Status codes

The following table lists the status codes of the edge API.

|Code|Response message|Description|
|:---|:---------------|:----------|
|200|Success|The call was successful.|
|201|Created|The request was successful and the server created new resources.|
|302|Move temporarily|The URL was redirected.|
|400|Bad Request|The error code may be reported due to the following two reasons: -   The semantic of the request was invalid. The current request cannot be understood by the server. The client will not send the same request unless the request is modified.
-   The request parameters contained an error. |
|401|Unauthorized|The current request requires user authentication. This means that the cookie has expired and you need to call the CreateAuthCookie API operation to obtain the updated cookie. Otherwise, you cannot call other API operations.|
|403|Forbidden|The server understood the request. However, the server refused to execute the request. You must verify whether the current user has the permissions to perform the API operation.|
|404|Not Found|The request failed because no resources were found on the server. You must check whether the parameters in the request are correct.|
|405|Method Not Allowed|The HTTP method specified in the request cannot be used to request the specified resource. For example, the POST method is not supported.|
|421|Too Many Connections|The number of connections established between the server and the IP address where the current client is located has reached the upper limit. **Note:** The IP address is the address of the client that is seen on the server, such as the address of the client gateway or a proxy server used by the client. |
|500|Internal Server Error|The server encountered an unexpected error and was unable to process the request. This error code is usually returned when an error occurs in the source code of the server.|
|503|Service Unavailable|The server is currently unable to process requests due to temporary server maintenance or server overload. |

