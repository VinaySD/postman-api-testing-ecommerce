# Execution Guide

This guide explains how to execute the OpenCart Postman API collection using Newman and how the collection can be integrated with Jenkins.

## Prerequisites

Install Newman and the Newman HTML reporter:

```bash
npm install -g newman
npm install -g newman-reporter-html
```

Make sure Node.js and npm are installed before running these commands.

---

## 1. Run the Collection Locally Using Newman

### Basic execution

Run the collection directly from the local JSON file:

```bash
newman run collections/OpenCart_Cart_API.postman_collection.json
```

### Generate an HTML report

```bash
newman run collections/OpenCart_Cart_API.postman_collection.json -r html
```

The HTML report can be used to review the request execution and test results.

---

## 2. Run the Collection Using a Remote Postman URL

If the collection is shared through Postman, Newman can execute it using the shared collection URL:

```bash
newman run <POSTMAN_COLLECTION_URL> -r html
```

Example:

```bash
newman run https://www.getpostman.com/collections/<COLLECTION_ID> -r html
```

Replace `<COLLECTION_ID>` with the actual shared Postman collection ID.

---

## 3. Run the Collection Through Jenkins

The collection can also be executed from Jenkins.

### Local Jenkins

Start Jenkins and create a Jenkins job that executes the Newman command.

Example build command:

```bash
newman run collections/OpenCart_Cart_API.postman_collection.json -r html
```

### Jenkins with the GitHub repository

Configure Jenkins to use your GitHub repository as the source:

```text
https://github.com/<YOUR_GITHUB_USERNAME>/postman-api-testing-ecommerce.git
```

After Jenkins checks out the repository, execute Newman against the collection:

```bash
newman run collections/OpenCart_Cart_API.postman_collection.json -r html
```

---

## 4. Execution Flow

```text
Postman Collection
        ↓
      Newman
        ↓
 API Test Execution
        ↓
   HTML Report
        ↓
     Jenkins
```

---

## 5. Notes

- Keep API keys and other sensitive credentials out of the GitHub repository.
- Use placeholders for environment-specific values.
- Keep the Postman collection inside the `collections/` directory.
- Keep environment files inside the `environments/` directory.
- Use the HTML report to review automated test execution results.
