# Rest_API_Collection

This is a collection of scripts or knowledge about REST API.

An API, or Application Programming interface, is a server that you can use to retrieve and send data to using code.

When we want to receive data from an API, we need to make a **Request** .

```pythonscript
import requests
```

## (1) GET request

This request is used to retrieve data. 

Required parameter: **URL**

Example:
- response = requests.get('http://web.mta.info/developers/turnstile.html')

The get() function returns a response object. 
Receive the status code for the request:
- print(response.status_code) 


