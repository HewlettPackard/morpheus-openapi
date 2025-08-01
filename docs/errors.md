---
title: Errors
---
When the Morpheus API encounters an error, the response will have an HTTP status of 400 of greater, instead of 200 OK. The error response body contains JSON with information to help troubleshoot the error.

#### 400 Bad Request
This error is returned if your request is invalid. Usually this is because a parameter is missing or the value is invalid. Try modifying your payload and retrying the request.

#### 401 Unauthorized
The unauthorized error will be encountered unless you pass the authorization header.

The 401 error code is returned if your access token is invalid or expired.

#### 403 Forbidden
This error is seen if you try to access an endpoint without the required permissions.

For this error example, use the token of user that does not have any admin permissions.

#### 404 Not Found
This error indicates the specified endpoint path does not exist. Check the URL of your request and try again.

The 404 error code is returned if a resource could be not be found by the specified ID.

#### 500 Internal Server Error
This error indicates something went wrong with the request and an unexpected error has occurred.

This example does not actually work and will return 404 instead. Hopefully you do not encounter a 500 error.

#### List of Error Codes
The Morpheus API uses the following error codes:

[block:parameters]
{
  "data": {
    "h-0": "Error Code",
    "h-1": "Description",
    "0-0": "400",
    "1-0": "401",
    "2-0": "403",
    "3-0": "404",
    "4-0": "405",
    "5-0": "406",
    "6-0": "410",
    "7-0": "418",
    "8-0": "429",
    "9-0": "500",
    "10-0": "503",
    "0-1": "Bad Request -- Your request failed. Check your request parameters and try again.",
    "1-1": "Unauthorized -- Your API key is invalid. Check your Authorization header.",
    "2-1": "Forbidden -- Your API key does not have the required role or permissions.",
    "3-1": "Not Found -- The specified resource could not be found.",
    "4-1": "Method Not Allowed -- You tried to access a resource with an invalid method.",
    "5-1": "Not Acceptable -- You requested a format that isn't json.",
    "6-1": "Gone -- The entity requested has been removed from our servers.",
    "7-1": "I'm a teapot.",
    "8-1": "Too Many Requests -- You're asking too much of the server. Slow down!",
    "9-1": "Internal Server Error -- We had a problem with our server. Try again later.",
    "10-1": "Service Unavailable -- We're temporarially offline for maintanance. Please try again later."
  },
  "cols": 2,
  "rows": 11
}
[/block]
