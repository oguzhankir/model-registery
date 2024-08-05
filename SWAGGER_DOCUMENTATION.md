# API Documentation

## Overview

This document provides detailed information about the API endpoints for the service, including authentication, status checks, model management, and inference.

## Endpoints

### 1. Login Endpoint

Authenticate and obtain an access token.

- **URL:** `/login`
- **Method:** `POST`
- **Parameters:**
  - `username` (string): The username for authentication.
  - `password` (string): The password for authentication.

#### Request Example

```bash
curl --location --request POST 'http://127.0.0.1:8000/login?username=admin&password=password123' \
--header 'accept: application/json'
```

#### Response Example

```json
{
  "access_token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiJhZG1pbiIsImV4cCI6MTcyMTM0NzIxMH0.Xf_MqqzzD6172OaEq4qfKU4pDMc3isdHHunwJmIgKmE"
}
```

### 2. Status Endpoint

Check the health status of the application.

- **URL:** `/status`
- **Method:** `GET`
- **Headers:**
  - `Authorization: Bearer {access_token}`

#### Request Example

```bash
curl --location 'http://127.0.0.1:8000/status' \
--header 'Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiJhZG1pbiIsImV4cCI6MTcyMTM0NzIxMH0.Xf_MqqzzD6172OaEq4qfKU4pDMc3isdHHunwJmIgKmE'
```

#### Response Example

```json
{
    "status": "healthy",
    "memory": {
        "total": 8221806592,
        "available": 5298999296,
        "percent": 35.5,
        "used": 2694094848,
        "free": 2069798912
    },
    "cpu_usage": "0.5%",
    "disk_usage": {
        "total": 62671097856,
        "used": 7234826240,
        "free": 52219555840,
        "percent": 12.2
    }
}
```

### 3. Metrics Endpoint

Endpoint for Prometheus to collect service metrics. No result is returned for local requests.

- **URL:** `/metrics`
- **Method:** `GET`

#### Request Example

```bash
curl --location 'http://localhost:8000/metrics'
```

### 4. Upload Model Endpoint

Upload a model and its artifacts to the model registry.

- **URL:** `/upload_model`
- **Method:** `POST`
- **Parameters:**
  - `model_name` (string): Name of the model.
  - `model_description` (string): Description of the model.
  - `model_version` (string): Version of the model.
  - `model_file` (file): The model file.
  - `artifact_files` (files): Additional artifact files.

- **Headers:**
  - `Authorization: Bearer {access_token}`

#### Request Example

```bash
curl --location 'http://127.0.0.1:8000/upload_model?model_name=test_model&model_description=This%20is%20a%20test%20model.&model_version=1&deployment=True' \
--header 'Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiJhZG1pbiIsImV4cCI6MTcyMTU2MDU4NH0.pJMafqyQPmMirfKd10WhkXSlNhGYEMv-VOPpZ_vHnUE' \
--form 'model_file=@"/path/to/Model_0.pkl"' \
--form 'artifact_files=@"/path/to/config.json"'
```

#### Response Example

```json
{
    "model_id": 3,
    "model_version_id": 3,
    "model_path": "test_model/1/Model_0.pkl",
    "artifact_paths": [
        "test_model/1/artifacts/config.json"
    ],
    "status": "deployed"
}
```

### 5. Get Model Endpoint

Retrieve a specific model version from the model registry.

- **URL:** `/get_model`
- **Method:** `GET`
- **Parameters:**
  - `model_name` (string): Name of the model.
  - `model_version` (string): Version of the model.

- **Headers:**
  - `Authorization: Bearer {access_token}`

#### Request Example

```bash
curl --location 'http://127.0.0.1:8000/get_model?model_name=test_model&model_version=1' \
--header 'Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiJhZG1pbiIsImV4cCI6MTcyMTU2MDU4NH0.pJMafqyQPmMirfKd10WhkXSlNhGYEMv-VOPpZ_vHnUE'
```

### 6. Inference Endpoint

Obtain prediction results for a specific model and customer.

- **URL:** `/inference`
- **Method:** `GET`
- **Parameters:**
  - `model_name` (string): Name of the model.
  - `model_version` (string): Version of the model.
  - `customer_id` (int): ID of the customer.
  - `purchase_date_id` (string): ID of the purchase date.

- **Headers:**
  - `Authorization: Bearer {access_token}`

#### Request Example

```bash
curl --location 'http://127.0.0.1:8000/inference?model_name=test_model&model_version=1&customer_id=1&purchase_date_id=2024-01-01' \
--header 'Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiJhZG1pbiIsImV4cCI6MTcyMTU2MDU4NH0.pJMafqyQPmMirfKd10WhkXSlNhGYEMv-VOPpZ_vHnUE'
```

#### Response Example

```json
{
    "prediction": 259.079028535477
}
```

