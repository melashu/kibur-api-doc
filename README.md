# 📗 Table of Contents

- [API Documentaion](#kibur-api)
  - [Data Format](#data-format)
  - [Endponts](#endpoint)
    - [Authentication](#auth)
      - [How to get the API KEY? ](#api-key)
    - [Users management (for admin user)](#user)
      - [How create user account?](#create)
      - [How to get list of users?](#list)
      - [How to delete a user?](#delete)
      - [How to update a user?](#update)
  - [Category (for admin user)](#category)
    - [How to create a new category?](#create-category)
    - [How to get a list of categories?](#list-category)
    - [How to delete a category?](#delete-category)
    - [How to update a category?](#update-category)
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

## API Endpoints <a name="endpoint"></a>
### Authentication <a name="auth"></a>
#### How to get the API KEY? <a name="api-key"></a>
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


### Users <a name="user"></a>
 #### How create user account?<a name="create"></a>
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
### How to get list of users? <a name="list"></a>
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
### How to delete a user? <a name="delete"></a>

You can send `delete` requests to `/api/v1/users/{user_id}`. Remember you must provide a user_id you wan to delete. If you successfully delete a user you will get a message like

```json
{
    "status": "done",
    "message": "Record deleted successfully"
}
```
### How to update a user? <a name="update"></a>
You can send `put/patch` requests to `/api/v1/users/{user_id}` and the body should be a json formated data. For example to change a password of a user the body should looks like
```json
{
    "user":{
       "password": "12345678"
  }
}
```
> Note: Remember you must provide a `user_id` you want to update.

### Categories <a name="category"></a>
#### How to create a new category? <a name="create-category"></a>
Only admin user can create a new category. To create a new category you can send `post` request to `/api/v1/categories` and the body of the request looks like 
```json
{
    "category":{
       "name": "Berger"
  }
}
```
> Note: `name` attribue is a mandatory parameter.

If you successfully create a category the api will return 
```json
{
    "id": 6,
    "name": "Berger",
    "status": "active",
    "number_of_menus": null
}
```
#### How to get a list of categories? <a name="list-category"></a>
To get a list of categories a `get` request to `/api/v1/categories`. The API return a list of user data looks like below 

```json
[
    {
        "id": 2,
        "name": "Berger",
        "status": "active",
        "number_of_menus": null
    },
    {
        "id": 4,
        "name": "Food",
        "status": "active",
        "number_of_menus": null
    } 
]
```
#### How to delete a category? <a name="delete-category"></a>
To delete a category send a `delete` request to `/api/v1/categories/{category_id}`. If you successfully delete a category the API will return.

```json
{
    "status": "done",
    "message": "Record deleted successfully"
}
```
> Note: You should pass a `category_id` you want to delete. 
#### How to update a category? <a name="update-category"></a>

To update a category send a `put/patch` request to to `/api/v1/categories/{category_id}` and the body of the request looks like

```json
{
    "category":{
       "name": "Berger"
  }
}
```

If you successfuly update a category the API will return 
```json
{
    "id": 2,
    "name": "Berger",
    "status": "active",
    "number_of_menus": 5
}
```

> Note: You should pass a `category_id` you want to update
### Menus
### Orders 
### How to get active orders?
### 