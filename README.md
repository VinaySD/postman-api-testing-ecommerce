# OpenCart API Testing with Postman, Newman & Jenkins

API testing project for the OpenCart shopping cart workflow using **Postman**, **JavaScript test scripts**, **Newman**, and **Jenkins**.

The project focuses on validating a complete cart API flow from session/token creation through product addition, cart retrieval, quantity update, and product removal.

## API Testing Flow

<p align="center"> 
  <img src="docs/screenshots/cart-api-flow.gif"
       alt="OpenCart Cart API Testing Flow"
       width="1100">
</p>

## Tech Stack

- **API Client:** Postman
- **API Automation / CLI:** Newman
- **Test Scripting:** Postman JavaScript
- **CI Tool:** Jenkins
- **Application:** OpenCart
- **Version Control:** Git & GitHub

## API Test Coverage

| Test ID | Scenario | Method | Endpoint |
|---|---|---|---|
| TC_API_001 | Create Session / Token | POST | `/api/login` |
| TC_API_002 | Add Product to Cart | POST | `/api/cart/add` |
| TC_API_003 | Get Cart Content | GET | `/api/cart/products` |
| TC_API_004 | Edit Product Quantity | POST | `/api/cart/edit` |
| TC_API_005 | Remove Product from Cart | POST | `/api/cart/remove` |

## Test Automation

The Postman collection contains automated assertions for:

- HTTP status code validation
- Response success-message validation
- API token extraction from the login response
- Cart ID extraction from the cart response
- Collection/environment variable handling
- Sequential execution of dependent API requests

The API token is captured after session creation and reused by later cart requests. The cart ID is captured from the cart response and used for edit/remove operations.

## Newman Execution

### Install Newman

```bash
npm install -g newman
```

### Install HTML Reporter

```bash
npm install -g newman-reporter-html
```

### Run the collection

```bash
newman run collections/OpenCart_Cart_API.postman_collection.json
```

### Generate an HTML report

```bash
newman run collections/OpenCart_Cart_API.postman_collection.json -r html
```

See [`docs/execution-guide.md`](docs/execution-guide.md) for additional execution approaches.

## Local Newman Test Result

The collection was successfully executed locally using Newman.

**Execution summary:**

| Metric | Result |
|---|---:|
| Iterations | 1 |
| Requests | 5 |
| Failed Requests | 0 |
| Test Scripts | 10 |
| Failed Test Scripts | 0 |
| Pre-request Scripts | 6 |
| Assertions | 9 |
| Failed Assertions | 0 |
| Total Duration | 577 ms |
| Average Response Time | 30 ms |

> The results above represent one successful local execution of the collection.

## Jenkins Integration

The collection was configured for Jenkins execution using Newman.

The Jenkins execution captured in the project encountered a connection failure because Jenkins could not reach the local OpenCart server (`ECONNREFUSED`).

This is documented intentionally rather than presenting the Jenkins run as successful.

```text
Jenkins
   ↓
Newman
   ↓
Local OpenCart API
   ↓
ECONNREFUSED
```

This indicates an environment/connectivity issue in that Jenkins run.

## Repository Structure

```text
postman-api-testing-ecommerce/
│
├── collections/
│   └── OpenCart_Cart_API.postman_collection.json
│
├── environments/
│   └── OpenCart_Local.postman_environment.json
│
├── docs/
│   ├── execution-guide.md
│   ├── test-scenarios.md
│   └── screenshots/
│       └── cart-api-flow.gif
│
├── README.md
└── .gitignore
```

## Environment Configuration

The project uses variables such as:

```text
baseUrl
api_token_val
product_id
quantity
cart_id_key
```

Sensitive credentials should not be committed to GitHub.

Use placeholders in the public environment file, and keep real API keys or private credentials in a local-only environment file.

## How to Run

### 1. Clone the repository

```bash
git clone https://github.com/<YOUR_GITHUB_USERNAME>/postman-api-testing-ecommerce.git
cd postman-api-testing-ecommerce
```

### 2. Import the collection into Postman

Import:

```text
collections/OpenCart_Cart_API.postman_collection.json
```

### 3. Configure the environment

Import:

```text
environments/OpenCart_Local.postman_environment.json
```

Update the local OpenCart host and other required values.

### 4. Run the collection

Run it from Postman or execute it using Newman.

## Documentation

- [API Test Scenarios](docs/test-scenarios.md)
- [Execution Guide](docs/execution-guide.md)

## Current Scope

The current collection focuses on the positive cart workflow and response validations.

Negative scenarios are not yet included, such as:

- Invalid API credentials
- Invalid product ID
- Invalid quantity
- Missing required parameters
- Invalid cart ID
- Unauthorized requests

These can be added as future improvements.

## Future Improvements

- Add negative and boundary test scenarios
- Add data-driven testing with Newman
- Add reusable environment configurations
- Generate and archive HTML test reports
- Complete a successful Jenkins CI execution
- Add GitHub/Jenkins automated pipeline execution
- Expand API coverage beyond cart operations

## Author

**Vinay Chaudhari**

QA / SDET Portfolio Project
