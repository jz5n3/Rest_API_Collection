# Rest_API_Collection

This is a collection of scripts or knowledge about REST API.

An API, or Application Programming interface, is a server that you can use to retrieve and send data to using code.

## Components

**Endpoint** : The URL that tied to a specific resource within an API.

**Method** : 
1. GET: retrieve data
2. PUT: replace data 
3. POST: create data
4. DELETE: delete data
             
**Data** : If you are using a method that involves changing data in a REST API, you will need to include a data payload with the request that includes all data that will be created for modified.

**Headers** : Contain any metedata that needs to be included with the request, such as authentication tokens, the content type should be returned, and any caching policies.

When we want to receive data from an API, we need to make a **Request** .

```pythonscript
import requests
```

### (1) GET request

This request is used to retrieve data. 

Required parameter: **URL, parameters**


The get() function returns a response object.
```pythonscript
response = requests.get('https://api.open-notify.org/astros.json') # no parameter required

# if parameter is required, parameters can be defined as a dictionary
parameters={}
response = requests.get('https://api.open-notify.org/astros.json', params=parameters) 

# if authentication is required, there are many ways to define authentication
# username & password
response = requests.get('https://api.github.com/user', auth=HTTPBasicAuth('username', 'password'))
# access token
my_headers = {'Authorization' : 'Bearer {access_token}'}
response = requests.get('http://httpbin.org/headers', headers=my_headers)
# other authentication methods: digest, Kerberos, NTLM, AuthBase

# if you need to make multiple requests within a single session, utilize Session objects
session = requests.Session()
session.headers.update({'Authorization': 'Bearer {access_token}'})
response = session.get('https://httpbin.org/headers')
```

Receive the status code for the request:
```pythonscript
print(response.status_code) 
```

- 200: Everything went okay, and the result has been returned.
- 301: The server is redirecting you to a different endpoint. This can happen when a company switches domain names, or an endpoint name is changed.
- 400: The server thinks you made a bad request. This can happen when you don't send along the right data, among other things.
- 401: The server thinks you are not authenticated. This can happen when you send wrong credentials to access an API.
- 403: You don't have right permissions to see the content.
- 404: The resource you tried to access wasn't found on the server
- 503: The server is not ready to handle the request.

Each API is commonly called **endpoint** .

See the data we received back from the API:
```pythonscript
response.json()
```
Handle json data:
- json.dump(): takes in a python object, and convets it to a string.
- json.loads(): takes a JSON string, and convetts it to a python object.

```pythonscript
import json

def jprint(obj):
    # create a formatted string of the Python JSON object
    text = json.dumps(obj, sort_keys=True, indent=4)
    print(text)

jprint(response.json())
```

### (2) POST / PUT request

```pythoscript
# Create a new resource
response = requests.post('https://httpbin.org/post', data = {'key':'value'})
# Update an existing resource
requests.put('https://httpbin.org/put', data = {'key':'value'})
```

**Access REST Headers***
```pythonscript
print(response.headers["date"]) 
'Wed, 11 June 2020 19:32:24 GMT'
```

## Robust API Request Example
```pythonscript
try:
    response = requests.get('http://api.open-notify.org/astros.json', timeout=5)
    response.raise_for_status()
    # Code here will only run if the request is successful
except requests.exceptions.HTTPError as errh:
    print(errh)
except requests.exceptions.ConnectionError as errc:
    print(errc)
except requests.exceptions.Timeout as errt:
    print(errt)
except requests.exceptions.RequestException as err:
    print(err)
```

