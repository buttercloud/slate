# Errors

The myTRS API uses the following error codes:


Error Code | Meaning
---------- | -------
400 | Bad Request -- Your request is malformed
402 | Unauthorized -- Your API key is wrong
404 | Not Found -- The specified registration could not be found
406 | Not Acceptable -- You requested a format that isn't json
500 | Internal Server Error -- We had a problem with our server. Try again later.
503 | Service Unavailable -- We're temporarially offline for maintanance. Please try again later.
