# Simple Grocery Store API - Testing

## Table of contents
* [Description](#Project-Description)
* [Requests](#Requests-Sent-to-the-API)
* [Examples of Test Cases](#Test-Cases-Examples)
* [How to run in Github](#How-to-run-in-Github)



## Project Description
- Overview
  This project is designed to test the "Simple Grocery Store API" using Postman and Newman. The tests include sending requests to various endpoints, validating the response by creating test cases to check status code, response time, response body, and returned data. Also check for authontication and authorization, make use of collection variables, dynamic variables, collection runner, and generating an HTML report using Newman.


### Prerequisites to run locally
  - Node.js and npm installed
  - Postman installed
  - Newman installed globally (`npm install -g newman`)


### API used
  Here you can find the documentation for the API:
  [Simple Grocery Store API](https://github.com/vdespa/Postman-Complete-Guide-API-Testing/blob/main/simple-grocery-store-api.md)



## Requests Sent to the API
  This Postman collection includes the following requests to all endpoints defined in the API documentation:
  * Note: Parameters and request body might be changed to support additional requests.
    + 'GET /status' - Returns the status of the API.
    + 'POST /api-clients' - Registers a new clint to the API, and try to register a client that already registered.
    + 'POST /carts' - Creates a new cart.
    + 'GET /products' - Returnes a list of products, returns specific number of products, returns products from a specific category, and returnes only available products.
    + 'POST /carts/:cartId/items' - Add an item to cart.
    + 'GET /carts/:cartId' - Returns a cart, and try to return a cart with an invalid ID.
    + 'GET /carts/:cartId/items' - Returnes a cart items, and try to return items of cart with invalid ID.
    + 'PATCH /carts/:cartId/items/:itemId' - Modifies a quantity of specific item in the cart.
    + 'PUT /carts/:cartId/items/:itemId' - Replaces an item in the cart with another product, and try to replace an item with invalid product ID.
    + 'DEL /carts/:cartId/items/:itemId' - Removes an item from the cart.
    + 'POST /orders' - Creates a new order by the registered client, and try to create an order with unauthorized user.
    + 'GET /orders' - Returnes a list of orders created by the registered client, and try to retrieve orders with an unauthorized user.
    + 'GET /orders/:orderId' - Returns a details of a specific order created by the user, and try to retrieve specific order with an unauthorized user.
    + 'PATCH /orders/:orderId' - Updates order details that created by a registered user, try to update specific order with an unauthorized user, and try to update order with invalid ID.
    + 'DEL /orders/:orderId' - Removes a specific order created by registered user, try to remove specific order with an unauthorized user, and try to remove order with invalid ID.







