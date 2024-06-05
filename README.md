# Simple Grocery Store API - Testing

## Table of contents
* [Description](#Project-Description)
* [Requests](#Requests-Sent-to-the-API)
* [Examples of Test Cases](#Test-Cases-Examples)
* [How to run in Github](#How-to-run-in-Github)



## Project Description
- Overview
  This project is designed to test the "Simple Grocery Store API" using Postman and Newman. It includes sending requests to various endpoints, validating the response by creating test cases to check status code, response time, response body, and returned data. Also check for authontication and authorization, validating response schema, make use of collection variables, dynamic variables, collection runner, and generating an HTML report using Newman.


### API used
  Here you can find the documentation for the API:
  [Simple Grocery Store API](https://github.com/vdespa/Postman-Complete-Guide-API-Testing/blob/main/simple-grocery-store-api.md)


### Scenario used in Testing:
- Check API is UP.
- Register a client.
- Create a new cart.
- Search for all products.
- Search for one random product.
- Add the product to the cart.
- Repeat steps (4-6) again.
- Review a cart details and its items.
- Modify the quantity of one item.
- Replace one item from the cart with another product.
- Remove one item from the cart.
- Create an order using cart.
- Review all created orders and order details.
- Modify order details to add comment.
- Delete an order.


### Prerequisites to run locally
  - Node.js and npm installed
  - Postman installed
  - Newman installed globally (`npm install -g newman`)



## Requests Sent to the API
  This Postman collection includes the following requests to all endpoints defined in the API documentation:
  * Note: Parameters and request body might be changed to support additional requests.
    + `GET /status` - Returns the status of the API.
    + `POST /api-clients` - Registers a new clint to the API, and try to register a client that already registered.
    + `POST /carts` - Creates a new cart.
    + `GET /products` - Returnes a list of products, returns specific number of products, returns products from a specific category, and returnes only available products.
    + `POST /carts/:cartId/items` - Add an item to cart.
    + `GET /carts/:cartId` - Returns a cart, and try to return a cart with an invalid ID.
    + `GET /carts/:cartId/items` - Returnes a cart items, and try to return items of cart with invalid ID.
    + `PATCH /carts/:cartId/items/:itemId` - Modifies a quantity of specific item in the cart.
    + `PUT /carts/:cartId/items/:itemId` - Replaces an item in the cart with another product, and try to replace an item with invalid product ID.
    + `DEL /carts/:cartId/items/:itemId` - Removes an item from the cart.
    + `POST /orders` - Creates a new order by the registered client, and try to create an order with unauthorized user.
    + `GET /orders` - Returnes a list of orders created by the registered client, and try to retrieve orders with an unauthorized user.
    + `GET /orders/:orderId` - Returns a details of a specific order created by the user, and try to retrieve specific order with an unauthorized user.
    + `PATCH /orders/:orderId` - Updates order details that created by a registered user, try to update specific order with an unauthorized user, and try to update order with invalid ID.
    + `DEL /orders/:orderId` - Removes a specific order created by registered user, try to remove specific order with an unauthorized user, and try to remove order with invalid ID.



## Test Cases Examples
+ Check Status Code (200 OK, 401 Unauthorized, 404 Not found, etc.):
```
	pm.test("Check that status code is 404", function () {
		pm.response.to.have.status(404);
	});
```
+ Validate Error Message:
```
	pm.test("Check that error message indicates an error in orderId", function () {
	    pm.expect(pm.response.text().toLowerCase()).to.include("error", "order");
	    pm.expect(pm.response.text().toLowerCase()).to.include("id");
	});
```
+ Validate Response Time to be less than specific value:
```
	pm.test("Verify that response time is less than 1500ms", function () {
	    pm.expect(pm.response.responseTime).to.be.below(1500);
	});
```
+ Check for specific Key in the Response Body:
```
	pm.test("Check that access token is returned", function () {
	    pm.expect(pm.response.json()).to.have.property("accessToken");
	});
```
+ Check that Response Body contains the same number of searched products:
```
	pm.test("Chect that response body contains " + pm.collectionVariables.get("randomNumber") + " products", function () {
	    pm.expect(pm.response.json().length).to.eql(pm.collectionVariables.get("randomNumber"));
	});
```
+ Check that Response Body contains products of only searched categories:
```
	pm.test("Check that response body only contains products of type: " + pm.collectionVariables.get("category"), function () {
	    for (var i = 0; i < pm.response.json().length; i++)
	        pm.expect(pm.response.json()[i].category).to.eql(pm.collectionVariables.get("category"));
	});
```
+ Check that Response Body is written in JSON format:
```
	pm.test("Check that returned data in json format", function () {
	    pm.expect(pm.response.headers.get("Content-Type")).to.include("application/json;");
	});
```
+ Validate that Response body has a valid schema:
```
	// define the schema
	var schema = {
	    "type": "object",
	    "required": ["id", "category", "name", "manufacturer", "price", "current-stock", "inStock"],
	    "properties": {
	        "id":                   {"type": "number"},
	        "category":             {"type": "string"},
	        "name":                 {"type": "string"},
	        "manufacturer":         {"type": "string"},
	        "price":                {"type": "number"},
	        "current-stock":        {"type": "number"},
	        "inStock":              {"type": "boolean"}
	    }
	};
	// test the response with the schema
	pm.test("Response has a valid Schema", function () {
	    pm.response.to.have.jsonSchema(schema);
	});
```








