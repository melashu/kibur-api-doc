# 📗 Table of Contents

- [📖 API Documentaion](#kibur-api)
  - [🛠 Data Format](#data-format)
    - [Tech Stack](#tech-stack)
    - [Key Features](#key-features)
- [💻 Getting Started](#getting-started)
  - [Setup](#setup)
  - [Prerequisites](#prerequisites)
  - [Install](#install)
  - [Usage](#usage)
  - [Run tests](#run-tests)
  - [Deployment](#triangular_flag_on_post-deployment)
- [👥 Authors](#authors)
- [🔭 Future Features](#future-features)
- [🤝 Contributing](#contributing)
- [⭐️ Show your support](#support)
- [🙏 Acknowledgements](#acknowledgements)
- [📝 License](#license)
# Kibur api documentation <a name="kibur-api"></a>
This is a documentation for Kibur API. 
## Data format for input and output request <a name="data-format"></a>
For every `POST` and `PUT/PATCH` requests, you can provide data in JSON format. For GET requests, the API will return data in JSON format. For all requests, you must include the Authorization token as a `Bearer token`. The Authorization header should be formatted as follows:

```ruby
 headers: {..., "Authorization" => "Bearer {API_KEY}"}
```

## API Endpoints
### Authentication
#### How to get the API KEY?
To get the api key you need to authenticate using `user_name` and `password` and send `get` request to

 `/api/v1/user/login`

 If you provide correct `user_name` and `password` the API will return 

 ```json
 {
    "token": "API_KEY",
    "user": {
        "id": "..",
        "username": "..",
        "role": ".."
   }
}
 ```


### Users 
 #### How create user account?
To establish a new user account first you need to login as `admin` only admin user can create a user account, and a `POST` request must be sent to the `/api/v1/users` endpoint. Mandatory attributes include `first_name, last_name, user_name, role, and password`.

The input format looks like 
```json
{
   "user":{
       "first_name" : "Melashu",
       "last_name": "Casher",
       "user_name": "casher",
       "role": "casher",
       "password": "12345678"
    }
}
```
### How to get list of users?
You can send `get` request to `api/v1/users` and the API returns Array of user object like 

```json
[
    {
        "id": 13,
        "first_name": "Biniam",
        "last_name": "Amare",
        "user_name": "bini12",
        "role": "casher"
    },
    {
        "id": 11,
        "first_name": "Munit",
        "last_name": "Amare",
        "user_name": "mitu",
        "role": "admin"
    }
]

```
### How to delete a user?

You can send `delete` requests to `/api/v1/users/{user_id}`. Remember you must provide a user_id you wan to delete. If you successfully delete a user you will get a message like

```json
{
    "status": "done",
    "message": "Record deleted successfully"
}
```
### How to update a user?
You can send `put/patch` requests to `/api/v1/users/{user_id}` and the body should be a json formated data. For example to change a password of a user the body should looks like
```json
{
    "user":{
       "password": "12345678"
  }
}
```
> Note: Remember you must provide a `user_id` you want to update.

 
### Authentication
### Categories
### Menus
### Orders 
### How to get active orders?
### 