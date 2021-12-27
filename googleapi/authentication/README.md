## Google Authentication API

Step 1 - Create service account

Step 1a - Grant access to project edit

Step 1b - Download keys [ JSON format ]

Step 2 - Enable Drive API

Step 3 - Enable Google Docs API

Step 4 - Enable Google Sheets API

Step 5 - Use below code to confirm if credentials are working

```python
from googleapiclient.discovery import build
from google.oauth2 import service_account


creds = service_account.Credentials.from_service_account_file('credentials.json', scopes=['openid', 'https://www.googleapis.com/auth/userinfo.email', 'https://www.googleapis.com/auth/userinfo.profile'])
user_info_service = build('oauth2', 'v2', credentials=credentials)
user_info = user_info_service.userinfo().get().execute()
print(user_info['email'])
```

### Let's break above code

### Part 1: Create credential object

```python
from google.oauth2 import service_account
creds = service_account.Credentials.from_service_account_file('credentials.json', scopes=['openid', 'https://www.googleapis.com/auth/userinfo.email', 'https://www.googleapis.com/auth/userinfo.profile'])
```

- A Credentials object holds refresh and access tokens that authorize access to a single user's data. 
    - These objects are applied to httplib2.Http objects to authorize access. They only need to be applied once and can be stored. This section describes the various methods to create and use Credentials objects.

    - Note: Credentials can be automatically detected in Google App Engine and Google Compute Engine. See Using OAuth 2.0 for Server to Server Applications.
        - https://github.com/googleapis/google-api-python-client/blob/main/docs/oauth-server.md#examples

- The google.oauth2.credentials.Credentials class holds OAuth 2.0 credentials that authorize access to a user's data.

- The google.oauth2.service_account.Credentials class is only used with OAuth 2.0 Service Accounts. 

- Create a Credentials object from the service account's credentials and the scopes your application needs access to

    - The google.oauth2.service_account.Credentials class is only used with OAuth 2.0 Service Accounts. No end-user is involved for these server-to-server API calls, so you can create this object directly.

### Scope list:
- https://developers.google.com/identity/protocols/oauth2/scopes

### Parts:

1. from_service_account_file - constructor
2. Credentials - class
3. service_account - module
4. google.oauth2 - library

### Part 2: Build a service object

```python
from googleapiclient.discovery import build
user_info_service = build('oauth2', 'v2', credentials=credentials)
```

- You build a a service object by calling the build function with the name and version of the API and the authorized Credentials object.

- Make requests to the API service using the interface provided by the service object
- use the build() function to create a service object. It takes an API name and API version as arguments.
    - supported APIs: https://github.com/googleapis/google-api-python-client/blob/main/docs/dyn/index.md
-  When build() is called, a service object will attempt to be constructed with methods specific to the given API.
- httplib2, the underlying transport library, makes all connections persistent by default. Use the service object with a context manager or call close to avoid leaving sockets open.
- Creating a request does not actually call the API. To execute the request and get a response, call the execute() function:
- API List: https://developers.google.com/apis-explorer/


### Parts

1. googleapiclient - library / package
2. discovery - submodule/module
3. build - function
4. userinfo - API function
5. get - method
6. execute - function


### Collections:

```python
user_info = user_info_service.userinfo().get().execute()
```

- Each API service provides access to one or more resources. A set of resources of the same type is called a collection. 
- The names of these collections are specific to the API.
- The service object is constructed with a function for every collection defined by the API.
- Here is userinfo() is collection function.

you create the collection object like this:

```python
user_info = user_info_service.userinfo()
```
It is also possible for collections to be nested

### Methods and requests

```python
user_info = user_info_service.userinfo().get()
```

- Every collection has a list of methods defined by the API. 
- Calling a collection's method returns an HttpRequest object.
- If the given API collection has a method named `userinfo` that can takes an argument.

### Execution and response

```python
user_info = user_info_service.userinfo().get().execute()
```

- Creating a request does not actually call the API. To execute the request and get a response, call the execute() function:


### Reference:

- https://developers.google.com/identity/protocols/oauth2/service-account
- https://github.com/googleapis/google-api-python-client/blob/main/docs/oauth.md#service-account-credentials
- https://github.com/googleapis/google-api-python-client/blob/main/docs/oauth.md
- https://google-auth.readthedocs.io/en/master/reference/google.oauth2.service_account.html
- https://google-auth.readthedocs.io/en/latest/_modules/google/oauth2/service_account.html
- https://google-auth.readthedocs.io/en/latest/_modules/google/oauth2/service_account.html?highlight=service_account
- https://google-auth.readthedocs.io/en/master/reference/google.oauth2.service_account.html
- https://google-auth.readthedocs.io/en/latest/user-guide.html
- https://googleapis.github.io/google-api-python-client/docs/epy/index.html
- https://github.com/googleapis/google-api-python-client/blob/main/docs/start.md
- https://github.com/googleapis/google-api-python-client/blob/main/docs/dyn/index.md
- https://developers.google.com/apis-explorer/
- https://github.com/googleapis/google-api-python-client/blob/main/docs/README.md
- https://github.com/googleworkspace/python-samples
- https://googleapis.github.io/google-api-python-client/docs/dyn/
