# Errors

The Everalbum API tries to use the most appropriate HTTP Status Code for a given response. These are some examples of what might be wrong if you're getting an error. This is by no means extensive and per-endpoint error expectations should be documented in the future.

Error Code | Meaning
---------- | -------
400 | Bad Request -- Your request sucks
401 | Unauthorized -- Your auth_token is wrong
403 | Forbidden -- You're not allowed to access this content
404 | Not Found -- The resource was not found or doesn't exist
405 | Method Not Allowed -- You tried to access a something with the wrong HTTP verb
406 | Not Acceptable -- You requested a format that isn't JSON
500 | Internal Server Error -- The server blew up while handling your response. Possibly a mal-formed request or issue with the API.
503 | Service Unavailable -- We're temporarily offline for maintenance. Please try again later.
