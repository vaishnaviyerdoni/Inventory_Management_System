
# Inventory Management System



## Table of Contents
| Sr No | Content                         | 
| ----- | ---------------------------| 
| 1     | Introduction                     | 
| 2     |  Features                          | 
| 3     | Tech Stack                        |
| 4     |Installation Instructions    |
| 5     |Project File structure        |
| 6     |     Usage                          |
| 7     |API Endpoints                   |





## Introduction
**Inventory Management System** is a full stack web application that enables Admin and Staff to manage inventory, monitor stock levels and manage the user accounts.
It also allows Customers along with admin and staff, to place orders for the goods based on the availability  of product in the inventory.
The Inventory Management System is built in *Java Programming Language* for backend logic, *SQL Server* as Database and *HTML*, *CSS* and *JavaScript* for Frontend interface.
## Tech Stack

- **Backend:** Java Programming Language
- **Database:** SQL Server
- **Frontend:** HTML, CSS, JavaScript
- **Tools:** Apache Tomcat, JDBC

## Features

- User Registration and User Authentication
- Role based Dashboards
- CRUD operations for Inventory
- Placing and Updating Order
- Passcode and Email reset
- User deletion



## File Structure
- /Business_Layer    ---Business Logic
- /Controller_Layer  ---Java Servlet
- /DAO_Layer         ---CRUD operations and DB Connection
- /Exceptions        ---Custom Written Exceptions
- /Model_Layer       ---POJO Classes
- /WebContent        ---HTML, CSS, JS
## Installation Instructions

1. Clone the repository.
2. Import the project to your preferred IDE, I used VSCode, but you can use whichever IDE you're comfortable with.
3. Set up the database in SQL server using the inventory.sql from the db folder.
4. Configure the JDBC Connection adjusting the Connection in DBConnection.java from DAO_Layer folder.
5. Deploy the System on Apache tomcat.
```bash
  jar -cvf InventorySystem.war -C WebContent/ .
```
6. Go to following link to register and you'll be redirected to Login.
```bash
  http://localhost:8080/InventorySystem/User/register.html
```
7. You're ready to use the System!

    
## Usage
Visit the following link to register:
```bash
http://localhost:8080/InventorySystem/User/register.html
```
Once registered successfully, you can login and based on your role: Admin, Staff or Customer, you will be taken to the respective Dashboard.

You can navigate the dashboard using the button and each buttons will take you to your desired page, like a user can place order, update their credentials. Admin can delete the unnecessary records
whereas admin or staff can view, update and keep track of inventory and order information.


## API Endpoints

## 1. Inventory

### GET

#### Get all items
```http
 GET /InventorySystem/inventory?action=viewAll
```

| Parameter | Type     | Description                              | Required |
| :-------- | :------- | :----------------------------------------|----------|
| `None`    |`None`    | `Returns all the Items in the inventory` | `No`     |

#### Get items by category
```http
  GET /InventorySystem/inventory?action=viewByCategory&category=${category}
```

| Parameter | Type     | Description                                      | Required |
| :-------- | :------- | :------------------------------------------------|----------|
| `category`| `String` |`Returns the items in Inventory by their category`|`Yes`     |

#### Get the price of an Item
```http
  GET /InventorySystem/inventory?action=getPricebyItemID&itemId=${itemId}&itemName=${itemName}
```

| Parameter | Type     | Description                              | Required |
| :-------- | :------- | :----------------------------------------|----------|
| `itemId`  | `int`    | `The unique id for each item in inventory`| `Yes`   |
| `itemName`| `String` | `The name of the item`                    | `Yes`   |

### POST

#### Insert an item in the Inventory
```http
 POST /InventorySystem/inventory
```

| Parameter | Type     |              Description                   | Required |
|-----------| :--------|:-------------------------------------------|----------|
| `userId`  | `String` | `Unique id of user Inserting the Item`     |  `Yes`   |
| `itemName`| `String` | `Name of item to be inserted`              |  `Yes`   |
| `category`| `String` | `category of the Item(eg. Stationary-book)`|  `Yes`   | 
| `price`   | `double` | `price of the Item`                        |  `Yes`   |
| `quantity`| `int`    | `quantity of item in inventory`            |  `Yes`   |
| `LowStockThreshold`  | `int`|`Threshold of low stock`             |  `Yes`   |

### PUT

#### Update the price of the item
```http
 PUT /InventorySystem/inventory
```
| Parameter | Type     | Description                                | Required |
| :-------- | :------- | :----------------------------------------  |----------|
| `itemId`  | `int`    | `The unique id for each item in inventory` | `Yes`    |
| `userId`  | `int`    | `The unique id of user Updating price`     | `Yes`    |
| `newPrice`| `double` | `The new price for the item`               | `Yes`    |

#### Update the Stock 
```http
 PUT /InventorySystem/inventory
```
| Parameter | Type     | Description                                | Required |
| :-------- | :------- | :------------------------------------------|----------|
| `itemId`  | `int`    | `The unique id for each item in inventory` | `Yes`    |
| `userId`  | `int`    | `The unique id of user Updating price`     | `Yes`    |
|`newQuantity`|`double`| `The quantity to add in inventory`         | `Yes`    |

### DELETE

#### Delete the item from  the inventory
```http
 DELETE /InventorySystem/inventory?action=deleteItem&itemId=${itemId}&userId=${userId}
```
| Parameter | Type |             Description               | Required |
| :---------|:-----|:--------------------------------------|:---------|
| `itemId`  | `int`| `Unique id of the item to be deleted` | `Yes`    |
| `userId`  | `int`| `Unique id of user deleting the item` | `Yes`    |

## 2. User

### GET

#### To view all the users
```http
 GET /InventorySystem/user?action=viewUserInfo&userId=${userId}
```
| Parameter | Type |             Description             | Required |
| :---------|:-----|:------------------------------------|:---------|
| `userId`  | `int`|`Unique id of user viewing the users`|   `Yes`  |

### POST

#### Register User
```http
 POST  /InventorySystem/user
```
| Parameter | Type     | Description                                    | Required |
| :-------- | :------- | :----------------------------------------------|----------|
| `userName`| `String` | `The unique username of user's choice`         |  `Yes`   |
| `passcode`| `String` | `The passcode of user's choice`                |  `Yes`   |
| `email`   | `String` | `User's email address`                         |  `Yes`   |
| `role`    | `String` |`User must choose role (admin, staff, customer)`|  `Yes`   |


 `**Note:** System allows 5 admin and 10 staff registrations, rest will have to be customers.`

#### User Login
```http
  POST /InventorySystem/user
```
| Parameter | Type     | Description                                    | Required |
| :-------- | :------- | :----------------------------------------------|----------|
| `userId`  | `int`    | `unique id for each user`                      |  `Yes`   |
| `userName`| `String` | `The unique username of user's choice`         |  `Yes`   |
| `passcode`| `String` | `The passcode of user's choice`                |  `Yes`   |
| `role`    | `String` | `User role (admin, staff, customer)`           |  `Yes`   |

### PUT
#### Update the passcode
```http
 PUT /InventorySystem/user
```
| Parameter | Type     | Description                                 | Required |
| :-------- | :------- | :-------------------------------------------|----------|
| `userId`  | `int`    | `The unique id of user Updating passcode`   | `Yes`    |
| `userName`| `String` | `The unique username of the user`           | `Yes`    |
|`newPasscode`|`String`| `The new passcode that user wants to update`| `Yes`    |

#### Update the email
```http
 PUT /InventorySystem/user
```
| Parameter | Type     | Description                               | Required |
| :-------- | :------- | :-----------------------------------------|----------|
| `userId`  | `int`    | `The unique id of user Updating passcode`   | `Yes`  |
| `userName`| `String` | `The unique username of the user`           | `Yes`  |
| `newEmail`|`String`  | `The new Email that user wants to update`   | `Yes`  |

### DELETE 

#### User deletes their account
```http
 DELETE /InventorySystem/user?action=UserDeletesTheirAccount&userId=${(userId}&userName=${userName}
```
| Parameter | Type    | Description                  | Required |
|:----------|:--------|:-----------------------------|:---------|
|`userName` |`String` | `unique userName of the user`| `Yes`    |
|`userId`   |`int`    | `unique id for each user`    | `Yes`    |

#### Admin deletes user
```http
 DELETE /InventorySystem/user?action=AdminDeletesUser&AdminUserId=${AdminUserId}&UserId=${UserId}
```
| Parameter | Type    | Description                   | Required |
|:----------|:--------|:------------------------------|:---------|
|`AdminId`  |`int`    | `Admin's unique userId`       | `Yes`    |
|`userId`   |`int`    | `userId of user to be deleted`| `Yes`    |

## 3. Order

#### GET

#### get information about all orders
```http
 GET /InventorySystem/order?action=getAllOrders&userId=${userId}
```
| Parameter | Type    | Description                 | Required |
|:----------|:--------|:----------------------------|:---------|
|`userId`   |`int`    | `unique id for each user`   | `Yes`    |

#### get the order information by orderId
```http
 GET /InventorySystem/order?action=viewByOrderId&orderId=${orderId}&userId=${userId}
```
|Parameter| Type| Description              | Required |
|---------|-----|--------------------------|----------|
|`userId `|`int`|`unique id for each user` | `Yes`    |
|`orderId`|`int`|`unique id for each order`| `Yes`    |

#### get the order information by userId

| Parameter | Type    | Description                 | Required |
|:----------|:--------|:----------------------------|:---------|
|`userId`   |`int`    | `unique id for each user`   | `Yes`    |

#### get price of an order
```http
 GET /InventorySystem/order?action=getPrice&orderId=${orderId}
```
| Parameter | Type     | Description                              | Required |
| :-------- | :------- | :----------------------------------------|----------|
| `orderId` | `int`    | `The unique id for each order in system` | `Yes`    |

#### get all items that are ordered from Inventory
```http
 GET /InventorySystem/order?action=viewItems&userId=${userId}
```
| Parameter | Type    | Description                 | Required |
|:----------|:--------|:----------------------------|:---------|
|`userId`   |`int`    | `unique id for each user`   | `Yes`    |

#### get the items belonging to an individual order
```http
 GET /InventorySystem/order?action=ItemsbyOrderId&userId=${userId}&orderId=${orderId }
```
| Parameter | Type     | Description                              | Required |
| :-------- | :------- | :----------------------------------------|----------|
| `orderId` | `int`    | `The unique id for each order in system` | `Yes`    |

### POST

### Place order
```http
 POST /InventorySystem/order
```
|Parameter      | Type   |  Description              | Required |
|---------------| -------|---------------------------|----------|
|`userId`       |`int`   | `unique id for each user` |  `Yes`   |
|`orderDate`    |`String`| `date of placing order`   |  `Yes`   |
|`customer name`|`String`| `name of user`            |  `Yes`   |

### Add Items to the order
```http
 POST /InventorySystem/order
```
| Parameter | Type     | Description                                    | Required |
| :-------- | :------- | :----------------------------------------------|----------|
| `orderId` | `int`    | `unique id for each order`                     |  `Yes`   |
| `userId`  | `int`    | `unique id for each user`                      |  `Yes`   |
| `items   `| `String` | `The items that user wants to buy`             |  `Yes`   |
| `quantity`| `int`    | `quantity of each item needed to be bought`    |  `Yes`   |

### PUT

### Update the total price of an order
```http
 PUT /InventorySystem/order
```
|Parameter|  Type  |Description                      |Required|
|:--------|:-------|:--------------------------------|--------|
| `price` |`double`| `The price that will be updated`| `Yes`  |
|`orderId`|`int`   | `The unique id of the order`    | `Yes`  |
| `userId`|`int`   |  `The unique id of the user`    | `Yes`  |

### Update the order status
```http
 PUT /InventorySystem/order
```
|Parameter|  Type  |Description                      |Required|
|:--------|:-------|:--------------------------------|--------|
| `Status`|`String`|`The status that will be updated`| `Yes`  |
|`AdminId`|`int`   | `The unique id of the order`    | `Yes`  |
| `userId`|`int`   |  `The unique id of the user`    | `Yes`  |

### Update quantity of items in an order
```http
 PUT /InventorySystem/order
```

| Parameter | Type| Description                                        | Required |
|-----------|-----|----------------------------------------------------|----------|
|`itemsId`  |`int`|`unique id given to each item that has been ordered`| `Yes`    |
|`userId`   |`int`|`unique id for each user`                           | `Yes`    |
|`nQuantity`|`int`|`The new updated quantity of items to add in order` | `Yes`    |
|`itemId`   |`int`|`The unique id for each item in the inventory`      | `Yes`    |


### Delete

### Admin deletes order
```http
 DELETE /InventorySystem/order?action=AdminDeletesOrder&userId=${userId}&orderId=${orderId}
```
|Parameter|Type |Description                       | Required |
|---------|-----|----------------------------------|----------|
|`UserId` |`int`|`Unique userId of Admin`          |  `Yes`   |
|`orderId`|`int`|`unique id of order to be deleted`|  `Yes`   |

### Admin deletes item
```http
 DELETE /InventorySystem/order?action=AdminDeletesItem&userId=${userId}&itemsId=${itemsId}
```
|Parameter |Type |Description                       | Required |
|----------|-----|----------------------------------|----------|
|`UserId`  |`int`|`Unique userId of Admin`          |  `Yes`   |
|`itemsId` |`int`|`unique id of item to be deleted` |  `Yes`   |

`**Note:** Delete items before deleting order.`