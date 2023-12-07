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
    - [Menus](#menus)
      - [How to create a menu?](#create-menu)
      - [How to get a list of menus?](#list-menus)
      - [How to delete a menu?](#delete-menu)
      - [How to update a menu?](#update-menu)
    - [Orders](#orders)
      - [How to create different orders in one group?](#group-orders) 

      - [How to create separate orders?](#separate-orders)

      - [How to get completed orders?](#completed-orders)
      - [How to get active orders?](#active-orders)
      - [How to update active orders?](#update-orders)
      - [How to delete active orders?](#delete-orders)
      - [How to get short sales summery?](#short-sales-summery)
      - [How to get full sales summery?](#full-sales-summery)
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
If you want to get a number of menus which is belongs to a give category, you can use `number_of_menus` property.

> Note: You should pass a `category_id` you want to update
### Menus <a name="menus"></a>
Menus are a list of items the cafeteria will provide to a customer.
#### How to create a menu? <a name="create-menu"></a>
To create a menu you need to send a `post` request to `/api/v1/menus` and the body of the request should looks like.

```json
{
    "menu":{
       "name": "Tegabino",
       "price": 120,
       "user_id": 14,
       "category_id": 2,
       "pin_to_top": true
 }
}
```
> Note: `Except` `pin_to_top` all attributes are `required`.

The `user_id` in a menu indicates the person responsible for preparing the registered menu. When a new order for this menu is placed, a notification about the order will be sent directly to the user associated with the menu.

In simpler terms, the user associated with the `user_id` will be alerted and tasked with fulfilling the order when a new order for their menu is created.

The `category_id` parameter specifies the category to which a particular menu belongs. Whenever a new menu is added, the `number_of_menus` property of the corresponding category is incremented.

If you successfully created a menu the API will return 

```json
{
    "id": 27,
    "name": "Tegabino",
    "price": 120.0,
    "pin_to_top": true,
    "created_by": "Munit Amare",
    "category": {
        "id": 2,
        "name": "Berger",
        "status": "active",
        "number_of_menus": 7
    },
    "user": {
        "id": 14,
        "first_name": "Biniam",
        "last_name": "Amare",
        "role": "food"
    }
}
```
#### How to get a list of menu? <a name="list-menus"></a>

To get a list of menus send `get` request to `/api/v1/menus` and the API response looks like

```json
{
    "Berger": [
        {
            "id": 13,
            "name": "Ayenet",
            "price": 100.0,
            "pin_to_top": true,
            "category": {
                "id": 2,
                "name": "Berger"
            },
            "user": {
                "id": 14,
                "first_name": "Biniam",
                "last_name": "Amare"
            }
        }
    ],
    "Food": [
        {
            "id": 18,
            "name": "Ayenet",
            "price": 100.0,
            "pin_to_top": false,
            "category": {
                "id": 3,
                "name": "Food"
            },
            "user": {
                "id": 14,
                "first_name": "Biniam",
                "last_name": "Amare"
            }
        }
    ]
}
```

The API organizes the returned menus according to their respective categories and sorts them based on the `pin_to_top` property.

#### How to delete a menu? <a name="delete-menu"></a>

To delete a menu send a `delete` request to `/api/v1/menus/{menu_id}`

If the menu successfully deleted the API will return 
```json
{
    "status": "done",
    "message": "Record deleted successfully"
}
```
> Note: Remember you must provide a `menu_id` you want to delete.

#### How to update a menu? <a name="update-menu"></a>

To update a menu send a `put/patch` request to `/api/v1/menus/{menu_id}` and the request body will looks like
```json
{
    "menu":{
       .....
       "name": "Ayent"
       .....
}
}
```

If you successfully update a menu the API will return 

```json
{
    "name": "Ayent",
    "id": 10,
    "price": 100.0,
    "pin_to_top": true,
    "category": {
        "id": 2,
        "name": "Berger"
    },
    "user": {
        "id": 14,
        "first_name": "Biniam",
        "last_name": "Amare"
    }
}
```
> Note: Remember you must provide a `menu_id` you want to delete.
### Orders <a name="orders"></a>
#### How to create different new orders in one group? <a name="group-orders"></a>
Every order including a single order will treated with in an order group. So when ever you pass an order it must be an array of order. For example, the casher may want to create different orders in `one` group. To do this you can send `post` request to `/api/v1/orders` and the body of the request should looks like 

```json
{
    "casher_name": "Munit",
    "waiter_name": "Bini",
    "user_id": 14,
    "orders": [
        {
      "menu_id": 14,
      "quantity": 4
       },
    {
      "menu_id": 15,
      "quantity": 6
    }]
}

```
> Note: If you are creating new order you must pass `casher_name`, `waiter_name`, `user_id`, and `orders` attribute. `orders` must be an array of order object and each object must have `menu_id` and `quantity`. `user_id` refers to the user who is responsible to prepare the order, you can get this id from the `menu`.

If order was successfully creates the API response looks like

```json
{
    "id": 36,
    "status": "active",
    "number_of_orders": 2,
    "created_at": "2023-12-04T18:58:36.247Z",
    "updated_at": "2023-12-04T18:58:36.270Z",
    "casher_name": "Melashu Casher",
    "waiter_name": "Bini",
    "created_by": "casher",
    "user": {
        "id": 14,
        "first_name": "Biniam",
        "last_name": "Amare"
    },
    "orders": [
        {
            "quantity": 4,
            "menu": {
                "name": "Ayenet",
                "price": 100.0
            }
        },
        {
            "quantity": 6,
            "menu": {
                "name": "Ayenet",
                "price": 100.0
            }
        }
    ]
}
 
```

If something went wrong the API will give you proper error message. For example, if you make the menu blank the API will return

```json
[
    {
        "menu": [
            "must exist"
        ]
    }
]
```

#### How to add to existing order group? <a name="existing-orders"></a>

Adding new order to the existing order group is the same as creating a new order but the only thing you need to do is pass an `order_group_id` and an array of `orders` with `post` request to `/api/v1/orders`. 

The body of the request should be

```json
{
    "order_group_id": 40,
    "orders": [
    {
      "menu_id": 14,
      "quantity": 4
    },{
        "menu_id": 15,
        "quantity": 10
    }
    ]
}
```
> Note, even if you need to add a single order you must pass it as an array of order.

If the order succsfully created, the API will return

```json
{
    "id": 40,
    "status": "active",
    "number_of_orders": 2,
    "created_at": "2023-12-04T19:51:24.138Z",
    "updated_at": "2023-12-04T19:51:24.138Z",
    "casher_name": "Melashu Casher",
    "waiter_name": "Bini",
    "created_by": "casher",
    "user": {
        "id": 14,
        "first_name": "Biniam",
        "last_name": "Amare"
    },
    "orders": [
        {
            "quantity": 4,
            "menu": {
                "name": "Ayenet",
                "price": 100.0
            }
        },
        {
            "quantity": 10,
            "menu": {
                "name": "Ayenet",
                "price": 100.0
            }
        }
    ]
}
```


#### How to create separate orders? <a name="separate-orders"></a>

Sometimes the casher may want to create a collection of orders separatly in this case you can send a `post` request to `/api/v1/orders/create_single_order`. The body of the request should have the following format

```json
{
    "casher_name": "Munit",
    "waiter_name": "Bini",
    "user_id": 14,
    "orders": [{
      "menu_id": 14,
      "quantity": 4
    },{
      "menu_id": 15,
      "quantity": 10
    }]
}
```

> Note, all the parameters are required 

If the order succsfully created the API will return

```json
[
    {
        "id": 113,
        "quantity": 4,
        "menu": {
            "id": 14,
            "name": "Ayenet",
            "price": 100.0,
            "pin_to_top": true
        },
        "order_group": {
            "id": 46,
            "status": "active",
            "number_of_orders": 1,
            "casher_name": "Melashu Casher",
            "waiter_name": "Bini",
            "created_by": "casher"
        }
    },
    {
        "id": 114,
        "quantity": 10,
        "menu": {
            "id": 15,
            "name": "Ayenet",
            "price": 100.0,
            "pin_to_top": false
        },
        "order_group": {
            "id": 47,
            "status": "active",
            "number_of_orders": 1,
            "casher_name": "Melashu Casher",
            "waiter_name": "Bini",
            "created_by": "casher"
        }
    }
]
```

#### How to get completed orders? <a name="completed-orders"></a>
To get a list of completed orders you can send `get` request to `/api/v1/orders/{from}/{to}`

This end point accepts two optional parameters `from` and `to`. Both must be a `date` or `Datetime` object. Parameter `from` indicates the date order creation starts and parameter `to` indicates the date order creation ends. If you don't pass any value the API will return `todays` completed order.

For example, if you send get requests to `/api/v1/orders/`

> Note, since we didn't pass `from` and `to` parameters the API will return todays completed order.

The API returns 

```json
[
    {
        "id": 46,
        "status": "completed",
        "number_of_orders": 1,
        "created_at": "2023-12-04T20:24:47.476Z",
        "updated_at": "2023-12-04T20:49:24.013Z",
        "casher_name": "Melashu Casher",
        "waiter_name": "Bini",
        "created_by": "casher",
        "user": {
            "id": 14,
            "first_name": "Biniam",
            "last_name": "Amare",
            "role": "food"
        },
        "orders": [
            {
                "quantity": 4,
                "menu": {
                    "name": "Ayenet",
                    "price": 100.0
                }
            }
        ]
    }
]
```
If you want to pass `from` and `to` parameters, you can do like 

`/api/v1/orders/Mon, 05 Dec 2023/Mon, 06 Dec 2023`

The first one indicates the start date and the second one indicates the end date. 

> Note: For `admin` user this endpoint returns `all` `completed` orders but for `non-admin` users(cashers) it only return orders created by their own. 

#### How to get active orders? <a name="active-orders"></a>
The adminstrator and inside workers may need to access active orders. To get active orders you can send `get` request to  `api/v1/active/orders/{:user_id}`.
> Here `user_id` is an optional parameter.

To display the active orders to admin user just send `get` request to `api/v1/active/orders` with out `user_id` and if you want to fetch active order belongs to specific user just pass a `user_id` parameter.

Casher's need to access their active orders, so you can send `get` request to `api/v1/my/active/orders`

#### How to update active orders? <a name="update-orders"></a>
When the inside worker withdraw the order they need to confirm the order as completed. To do this you can send `put` request to `api/v1/approve/{id}`. The `id` parameter refers the order group id that we need to change the status to completed.

For example,

Sending `put` request to `api/v1/approve/28` returns 

```json
{
    "id": 28,
    "status": "completed",
    "number_of_orders": 2,
    "casher_name": "Munita",
    "waiter_name": "Bini",
    "approved_by": "Eden",
    "orders": [
        {
            "id": 50,
            "quantity": 4
        },
        {
            "id": 51,
            "quantity": 6
        }
    ]
}
```
> Note: the `id` parameter is required parameter. 

In case the casher want to update the order group, you can send `put` request to `/api/v1/order_groups/{id}`.

For example, if you want to update the waiter name for a given order group, send `put` request to `/api/v1/order_groups/45` and the body of the request should looks like

```json
{
    "order_group": {
        "waiter_name": "Solomon"
    }
}
```
If order group successfully updated then the API will return 
```json
{
    "id": 45,
    "status": "active",
    "number_of_orders": 1,
    "casher_name": "Melashu Casher",
    "waiter_name": "Solomon",
    "approved_by": null,
    "orders": [
        {
            "id": 112,
            "quantity": 10,
        }
    ]
}
```
Sometime it may be required to update indvisual order with in an order group. 
 For such cases, you can send `put` request to `/api/v1/orders/{id}` and the body of the request should have the following format.

For example, lets update the quantity of an order. Send `put` request to 

`/api/v1/orders/52`

 ```json
 {
    "order": {
        "quantity": 2
    }
}
 ```

 If the order was successfully updated then the API will return 
 ```json
{
    "id": 52,
    "quantity": 1,
    "menu": {
        "id": 14,
        "name": "Ayenet",
        "price": 100.0,
        "pin_to_top": true,
        "created_by": "Munit Amare"
    },
    "order_group": {
        "id": 29,
        "number_of_orders": 2,
        "waiter_name": "Bini"
    }
}
 ```
> Note: The `id` parameter is required.
#### How to delete active orders? <a name="delete-orders"></a>

Sometimes the casher may want to delete the order group or indvidual orders.

If the casher want to delete a specific order group, then you can send `delete` request to `/api/v1/order_groups/{id}`

for example, send `delete` request to `/api/v1/order_groups/9`

If the order group successfully deleted, the API will return 

```json
{
    "status": "done",
    "message": "Record deleted successfully"
}
```
If the casher want to delete specific order, then you can send `delete` request to `/api/v1/orders/{id}` 

for example, send `delete` request  to 
`/api/v1/orders/53`

If the order successfully deleted the API will return 

```json
{
    "status": "done",
    "message": "Record deleted successfully"
}
```

> Note: the `id` parameter is required parameter. 

#### How to get short sales summery? <a name="short-sales-summery"></a>

The admin and the casher may want to see short current day order summery, In such case you can send request to `/api/v1/orders/total_order_summery/{user_name}`


> Note: Here `user_name` parameter is an optional parameter if you didn't include user name in your request, the API considers the request comes from the admin user and return the summery of orders created by different casher.

for example if you send a request `get` to
`/api/v1/orders/total_order_summery`, the api consider this request is from the adminuser and it returns 

```json
{
    "total_order": 60,
    "total_order_amount": 26500.0
}
```
If you include a `casher's` user_name on your request the API returns the short summary which belongs to a specific casher.

For example if you send a `get` request to 
`/api/v1/orders/total_order_summery/mitu` the API returns

```json
{
    "total_order": 36,
    "total_order_amount": 13056.0
}
```

#### How to get full sales summery? <a name="full-sales-summery"></a>

