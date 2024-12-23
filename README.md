# Store API Documentation

## Overview

The Store API provides functionality for managing a product catalog. It supports CRUD operations and advanced querying features such as filtering, sorting, pagination, and field selection. This API is built using Node.js, Express.js, and MongoDB.

## Features

- Retrieve all products
- Advanced filtering by product attributes
- Sort products by specific fields
- Select specific fields to return in the response
- Pagination support for managing large datasets

## Technologies Used

- **Node.js**: JavaScript runtime
- **Express.js**: Web framework for building RESTful APIs
- **MongoDB**: NoSQL database
- **Mongoose**: ODM library for MongoDB

## Product Model

The `Product` model represents the structure of the product documents stored in MongoDB.

### Schema

| Field       | Type    | Required | Default      | Description                                      |
| ----------- | ------- | -------- | ------------ | ------------------------------------------------ |
| `name`      | String  | Yes      | N/A          | Name of the product                              |
| `price`     | Number  | Yes      | N/A          | Price of the product                             |
| `featured`  | Boolean | No       | `false`      | Indicates if the product is featured             |
| `rating`    | Number  | No       | `4.5`        | Rating of the product                            |
| `createdAt` | Date    | No       | `Date.now()` | Date the product was created                     |
| `company`   | String  | Yes      | N/A          | Company name, restricted to specific enum values |

### Enum Values for `company`

- ikea
- liddy
- caressa
- marcos

## Installation and Setup

1. Clone the repository:

   ```bash
   git clone <repository-url>
   cd <repository-name>
   ```

2. Install dependencies:

   ```bash
   npm install
   ```

3. Set up the environment variables:
   Create a `.env` file in the root directory and configure the following:

   ```env
   MONGO_URI=<your-mongodb-connection-string>
   PORT=5000
   ```

4. Start the application:
   ```bash
   npm start
   ```

## API Endpoints

### Base URL

```
http://localhost:5000/api/v1/products
```

### Endpoints

#### 1. Get All Products (Static)

- **URL**: `/static`
- **Method**: `GET`
- **Description**: Retrieve all featured products.
- **Response**:
  ```json
  {
    "products": [
      {
        "_id": "64bff3a4cd77db09c97a00ec",
        "name": "Sample Product",
        "price": 49.99,
        "featured": true,
        "rating": 4.5,
        "createdAt": "2024-01-01T00:00:00.000Z",
        "company": "ikea"
      }
    ]
  }
  ```

#### 2. Get All Products

- **URL**: `/`
- **Method**: `GET`
- **Description**: Retrieve all products with optional query parameters for filtering, sorting, field selection, and pagination.
- **Query Parameters**:

  - `featured` (boolean)
  - `company` (string)
  - `name` (string, partial match supported)
  - `sort` (string, comma-separated fields)
  - `fields` (string, comma-separated fields)
  - `numericFilters` (string, supports operators `>`, `>=`, `=`, `<`, `<=` for fields like `price` and `rating`)
  - `page` (integer, default: `1`)
  - `limit` (integer, default: `10`)

- **Response**:
  ```json
  {
    "products": [
      {
        "_id": "64bff3a4cd77db09c97a00ec",
        "name": "Sample Product",
        "price": 49.99,
        "featured": false,
        "rating": 4.5,
        "createdAt": "2024-01-01T00:00:00.000Z",
        "company": "ikea"
      }
    ],
    "nbHits": 1
  }
  ```

## Error Handling

Errors are handled using custom middleware.

### Error Response Structure

```json
{
  "msg": "Something went wrong, please try again"
}
```

### Example 404 Error Response

- **Status Code**: `404`
- **Response**:
  ```json
  "Route does not exist"
  ```

## License

This project is licensed under the MIT License.
