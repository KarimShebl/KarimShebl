
# FakeStore API Test Collection

This repository contains a Postman test collection for the [Fake Store API](https://fakestoreapi.com/). The collection includes tests for various endpoints such as users, authentication, products, and carts.

## Files Included

- `FakeStoreApiTests.postman_collection.json`: The Postman collection file containing all requests and tests.
- `README.md`: This file, with instructions on how to set up and run the collection.

## Prerequisites

Before running the collection, make sure you have the following:

- Postman installed on your computer. You can download it from [postman.com/downloads](https://www.postman.com/downloads/).
- A basic understanding of how to use Postman.
- An environment variable named `url` set to `https://fakestoreapi.com`.

## How to Use

1. **Import the Collection:**
   - Open Postman.
   - Click on the “Import” button.
   - Select the file `FakeStoreApiTests.postman_collection.json` from your system.

2. **Set Up the Environment:**
   - In Postman, go to the “Environments” tab and create a new environment.
   - Add a variable named `url` with the following value:

     ```
     Key: url
     Initial Value: https://fakestoreapi.com
     Current Value: https://fakestoreapi.com
     ```

   - Save the environment and select it from the top-right environment dropdown.

3. **Run the Collection:**
   - Navigate to the “Collections” tab.
   - Select `FakeStoreApiTests`.
   - Click the “Run” button to open the Collection Runner.
   - Choose the environment you just created.
   - Click “Start Run” to execute the requests.


## What’s Covered

The collection includes tests for the following endpoints:

### Users
- `POST /users` – Create a new user
- `GET /users` – Retrieve all users
- `GET /users/{id}` – Retrieve a user by ID

### Authentication
- `POST /auth/login` – Log in and retrieve a token

### Products
- `GET /products` – Retrieve all products
- `GET /products/{id}` – Retrieve a specific product by ID
- `GET /products/category/{category}` – Get products by category
- `GET /products/categories` – List all product categories

### Carts
- `POST /carts` – Create a new cart
- `GET /carts` – Retrieve all carts
- `GET /carts/user/{userId}` – Get carts by user ID
- `DELETE /carts/{id}` – Delete a cart by ID