# API Test Scenarios

## Overview

This document describes the test scenarios implemented in the OpenCart Cart API Postman collection.

The collection covers the basic cart workflow:

```text
Create Session / Token
        ↓
Add Product to Cart
        ↓
View Cart Content
        ↓
Edit Product Quantity
        ↓
Remove Product from Cart
```

## Test Scenarios

| ID | Test Scenario | Method | Endpoint | Validation |
|---|---|---|---|---|
| TC_API_001 | Create Session / Token | POST | `/api/login` | Verify HTTP 200 and successful session message |
| TC_API_002 | Add Product to Cart | POST | `/api/cart/add` | Verify HTTP 200 and successful cart modification message |
| TC_API_003 | Get Cart Content | GET | `/api/cart/products` | Verify HTTP 200 and capture `cart_id` from the response |
| TC_API_004 | Edit Product Quantity | POST | `/api/cart/edit` | Verify HTTP 200 and successful cart modification message |
| TC_API_005 | Remove Product from Cart | POST | `/api/cart/remove` | Verify HTTP 200 and successful cart modification message |

## Detailed Scenarios

### TC_API_001 — Create Session / Token

**Purpose:** Create an API session and capture the returned API token.

**Request:**
- Method: `POST`
- Endpoint: `/api/login`
- Body: `username`, `key`

**Test validations:**
- Verify HTTP status code is `200`.
- Verify the success message.
- Extract `api_token` from the JSON response.
- Store the token in the collection variable `api_token_val`.

**Expected Result:**

The API session should be created successfully and the returned token should be stored for subsequent requests.

---

### TC_API_002 — Add Product to Cart

**Purpose:** Add a product to the shopping cart.

**Request:**
- Method: `POST`
- Endpoint: `/api/cart/add`
- Body: `product_id`, `quantity`

**Test data configured in the collection:**
- `product_id`: `40`
- `quantity`: `2`

**Test validations:**
- Verify HTTP status code is `200`.
- Verify the success message.

**Expected Result:**

The selected product should be added or the shopping cart should be successfully modified.

---

### TC_API_003 — Get Cart Content

**Purpose:** Retrieve the cart contents for the selected product.

**Request:**
- Method: `GET`
- Endpoint: `/api/cart/products`
- Parameter: `product_id`

**Test validations:**
- Verify HTTP status code is `200`.
- Extract `cart_id` from the first product in the response.
- Store the value as `cart_id_key`.

**Expected Result:**

The API should return the cart contents and provide the cart item ID required by subsequent cart operations.

---

### TC_API_004 — Edit Product Quantity

**Purpose:** Update the quantity of an existing cart item.

**Request:**
- Method: `POST`
- Endpoint: `/api/cart/edit`
- Body: `key`, `quantity`

**Test data configured in the collection:**
- `key`: `{{cart_id_key}}`
- `quantity`: `5`

**Test validations:**
- Verify HTTP status code is `200`.
- Verify the success message.

**Expected Result:**

The cart item quantity should be successfully updated.

---

### TC_API_005 — Remove Product from Cart

**Purpose:** Remove the selected product from the shopping cart.

**Request:**
- Method: `POST`
- Endpoint: `/api/cart/remove`
- Body: `key`

**Test validations:**
- Verify HTTP status code is `200`.
- Verify the success message.
- Clear temporary collection/environment variables after execution.

**Expected Result:**

The selected cart item should be successfully removed.

## Dynamic Data Handling

The collection uses Postman variables to pass data between requests:

```text
api_token_val
product_id
quantity
cart_id_key
```

The API token is captured from the login response, while the cart ID is captured from the cart-content response. This allows later requests to use dynamically generated values instead of hard-coded response data.

## Current Test Coverage

The current collection validates:

- HTTP status code
- Response success message
- API token extraction
- Cart ID extraction
- Variable handling between requests
- Sequential cart workflow

## Scope Note

This document describes the tests currently implemented in the collection. Negative scenarios such as invalid credentials, invalid product IDs, invalid quantities, missing parameters, and unauthorized requests are not included in the current collection.
