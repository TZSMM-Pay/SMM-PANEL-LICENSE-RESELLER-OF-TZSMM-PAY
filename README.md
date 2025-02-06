# Reseller API Documentation

## Overview

This API allows resellers to manage user plans, check order status, retrieve license information, and automate service purchases.

### Base URL

```
https://tzsmmpay.com/api/smmpanel/v1
```

## Authentication

All API requests must include a valid `key`, which can be obtained from [tzsmmpay.com](https://tzsmmpay.com/reseller).

## Endpoints

### 1. Get Available Services

**Endpoint:**

```
GET /api/smmpanel/v1?action=services&key=YOUR_API_KEY
```

**Response:**

```json
[
  {
    "service": 2,
    "name": "Monthly Silver",
    "type": "Package",
    "category": "TZSMM Pay License",
    "min": 1,
    "max": 1,
    "rate": 0.56,
    "currency": "USD"
  }
]
```

---

### 2. Get Order Status

**Endpoint:**

```
GET /api/smmpanel/v1?action=status&key=YOUR_API_KEY&order=ORDER_ID
```

**Parameters:**

| Parameter | Type   | Required | Description                                     |
| --------- | ------ | -------- | ----------------------------------------------- |
| key       | string | Yes      | Your reseller API key                           |
| action    | string | Yes      | Must be `status`                                |
| order     | int    | No       | Order ID (for a single order)                   |
| orders    | string | No       | Comma-separated order IDs (for multiple orders) |

**Response (Single Order):**

```json
{
  "charge": "0.56",
  "start_count": 0,
  "status": "Completed",
  "remains": 0,
  "currency": "USD"
}
```

**Response (Multiple Orders):**

```json
{
  "132": {
    "charge": "0.56",
    "start_count": 0,
    "status": "Completed",
    "remains": 0,
    "currency": "USD"
  },
  "130": {
    "charge": "0.56",
    "start_count": 0,
    "status": "Completed",
    "remains": 0,
    "currency": "USD"
  },
  "8": {
    "error": "Incorrect order ID"
  }
}
```

---

### 3. Get Balance

**Endpoint:**

```
GET /api/smmpanel/v1?action=balance&key=YOUR_API_KEY
```

**Response:**

```json
{
  "currency": "USD",
  "balance": "0.32"
}
```

---

### 4. Place a New Order

**Endpoint:**

```
GET /api/smmpanel/v1?action=add&key=YOUR_API_KEY&service=SERVICE_ID&link=USER_EMAIL
```

**Parameters:**

| Parameter | Type   | Required | Description                            |
| --------- | ------ | -------- | -------------------------------------- |
| key       | string | Yes      | Your reseller API key                  |
| action    | string | Yes      | Must be `add`                          |
| service   | int    | Yes      | Service ID from the available services |
| link      | string | Yes      | User email for license activation      |

**Response:**

```json
{
  "order": 23501
}
```





### Error Responses

| Error Code | Message                             |
| ---------- | ----------------------------------- |
| 401        | `Invalid API key`                   |
| 400        | `Incorrect request`                 |
| 404        | `Invalid order ID`                  |
| 402        | `You don't have sufficient balance` |

## Notes

- Ensure the API key is valid.
- Orders can be checked in bulk using the `orders` parameter.
- Resellers must maintain sufficient balance before making purchases.

For support, visit [tzsmmpay.com](https://tzsmmpay.com/reseller).

