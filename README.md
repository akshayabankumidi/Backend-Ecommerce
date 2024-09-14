## Visual References

## Database Schema and API Routes
![image](https://github.com/user-attachments/assets/bebbde0b-87f0-4e1e-975b-cb11688512b9)

## Assumed frontend flow of the e-commerce application
![newpngecommers](https://github.com/user-attachments/assets/cea99b08-6357-4bb1-94f7-9fb94fdbc6cb)

# E-commerce Backend API Documentation

## Base URL
https://backend-ecommerce-wine-seven.vercel.app/

## Authentication
Most endpoints require a valid JWT token in the Authorization header:
`Authorization: Bearer <token>`

## Endpoints

### 1. User Registration
- **URL**: `/api/auth/register`
- **Method**: `POST`
- **Request Body**:
  ```json
  {
    "username": "string",
    "email": "string",
    "password": "string",
    "type": "string"
  }
  ```
- **Response**: 
  - Status: 201 Created
  - Body: 
    ```json
    {
      "id": "integer",
      "username": "string",
      "email": "string",
      "type": "string"
    }
    ```
- **Sample Request**:
  ```json
  {
    "username": "user4",
    "email": "user4@gmail.com",
    "password": "useR@444",
    "type": "seller"
  }
  ```
- **Sample Response**:
  ```json
  {
    "id": 2,
    "username": "user4",
    "email": "user4@gmail.com",
    "type": "seller"
  }
  ```

### 2. User Login
- **URL**: `/api/auth/login`
- **Method**: `POST`
- **Request Body**:
  ```json
  {
    "identifier": "string",
    "password": "string"
  }
  ```
- **Response**:
  - Status: 200 OK
  - Body:
    ```json
    {
      "token": "string",
      "user": {
        "id": "integer",
        "username": "string",
        "email": "string",
        "type": "string"
      }
    }
    ```
- **Sample Request**:
  ```json
  {
    "identifier": "user4@gmail.com",
    "password": "useR@444"
  }
  ```
- **Sample Response**:
  ```json
  {
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
    "user": {
      "id": 2,
      "username": "user4",
      "email": "user4@gmail.com",
      "type": "seller"
    }
  }
  ```

### 3. Create Product
- **URL**: `/api/products`
- **Method**: `POST`
- **Auth Required**: Yes
- **Request Body**:
  ```json
  {
    "name": "string",
    "description": "string",
    "price": "float",
    "category": "string",
    "discount": "float"
  }
  ```
- **Response**:
  - Status: 201 Created
  - Body: Created product object
- **Sample Request**:
  ```json
  {
    "name": "paperboat",
    "description": "paperboat aamras",
    "price": 30,
    "category": "drinks",
    "discount": 0
  }
  ```
- **Sample Response**:
  ```json
  {
    "id": 3,
    "name": "paperboat",
    "description": "paperboat aamras",
    "price": "30.00",
    "category": "drinks",
    "seller_id": 2,
    "discount": "0.00",
    "created_at": "2024-09-14T06:46:31.438Z",
    "updated_at": "2024-09-14T06:46:31.438Z"
  }
  ```

### 4. Get Product by Name
- **URL**: `/api/products?name=text`
- **Method**: `GET`
- **Response**:
  - Status: 200 OK
  - Body: Array of product objects
- **Sample Request**: `/api/products?name=paperboat`
- **Sample Response**:
  ```json
  [
    {
      "id": 3,
      "name": "paperboat",
      "description": "paperboat aamras",
      "price": "30.00",
      "category": "drinks",
      "seller_id": 2,
      "discount": "0.00",
      "created_at": "2024-09-14T06:46:31.438Z",
      "updated_at": "2024-09-14T06:46:31.438Z"
    }
  ]
  ```

### 5. Get Product by Category
- **URL**: `/api/products?category=text`
- **Method**: `GET`
- **Response**:
  - Status: 200 OK
  - Body: Array of product objects
- **Sample Request**: `/api/products?category=drinks`
- **Sample Response**:
  ```json
  [
    {
      "id": 3,
      "name": "paperboat",
      "description": "paperboat aamras",
      "price": "30.00",
      "category": "drinks",
      "seller_id": 2,
      "discount": "0.00",
      "created_at": "2024-09-14T06:46:31.438Z",
      "updated_at": "2024-09-14T06:46:31.438Z"
    }
  ]
  ```

### 6. Update Product
- **URL**: `/api/products/:id`
- **Method**: `PATCH`
- **Auth Required**: Yes
- **Request Body**: Same as Create Product, all fields optional
- **Response**:
  - Status: 200 OK
  - Body: Updated product object
- **Sample Request**:
  ```json
  {
    "name": "paperboat",
    "description": "paperboat aamras",
    "price": 32,
    "category": "drinks",
    "discount": 0
  }
  ```
- **Sample Response**:
  ```json
  {
    "id": 3,
    "name": "paperboat",
    "description": "paperboat aamras",
    "price": "32.00",
    "category": "drinks",
    "seller_id": 2,
    "discount": "0.00",
    "created_at": "2024-09-14T06:46:31.438Z",
    "updated_at": "2024-09-14T07:43:40.236Z"
  }
  ```

### 7. Delete Product
- **URL**: `/api/products/:id`
- **Method**: `DELETE`
- **Auth Required**: Yes
- **Response**:
  - Status: 200 OK
  - Body: Deleted product object and success message
- **Sample Response**:
  ```json
  {
    "message": "Product deleted successfully",
    "product": {
      "id": 3,
      "name": "paperboat",
      "description": "paperboat aamras",
      "price": "32.00",
      "category": "drinks",
      "seller_id": 2,
      "discount": "0.00",
      "created_at": "2024-09-14T06:46:31.438Z",
      "updated_at": "2024-09-14T07:43:40.236Z"
    }
  }
  ```

### 8. Add to Cart
- **URL**: `/api/cart`
- **Method**: `POST`
- **Auth Required**: Yes
- **Request Body**:
  ```json
  {
    "productId": "integer"
  }
  ```
- **Response**:
  - Status: 201 Created
  - Body: Created cart item object
- **Sample Request**:
  ```json
  {
    "productId": 1
  }
  ```
- **Sample Response**:
  ```json
  {
    "id": 5,
    "user_id": 2,
    "product_id": 1,
    "created_at": "2024-09-14T07:46:47.288Z",
    "updated_at": "2024-09-14T07:46:47.288Z"
  }
  ```

### 9. Remove from Cart
- **URL**: `/api/cart/:id`
- **Method**: `DELETE`
- **Auth Required**: Yes
- **Response**:
  - Status: 200 OK
  - Body: Success message
- **Sample Response**:
  ```json
  {
    "message": "Item removed from cart"
  }
  ```

### 10. Get Cart
- **URL**: `/api/cart`
- **Method**: `GET`
- **Auth Required**: Yes
- **Response**:
  - Status: 200 OK
  - Body: Array of cart item objects
- **Sample Response**:
  ```json
  [
    {
      "id": 5,
      "user_id": 2,
      "product_id": 1,
      "created_at": "2024-09-14T07:46:47.288Z",
      "updated_at": "2024-09-14T07:46:47.288Z"
    }
  ]
  ```

## Error Responses
All endpoints may return the following error responses:
- 400 Bad Request: Invalid input
- 401 Unauthorized: Missing or invalid token
- 403 Forbidden: Insufficient permissions
- 404 Not Found: Resource not found
- 500 Internal Server Error: Server-side error

Error response body:
```json
{
  "error": "string (error message)"
}
```

## Notes
- The `type` field in the user registration is used to distinguish between different user roles (buyer, seller).
- Product creation and modification are restricted to users with buyer roles.
- The `identifier` field in the login request can be either the user's email or username.
