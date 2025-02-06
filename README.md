# Reseller API Documentation

## Overview
This API allows resellers to manage user plans, check order status, and automate service purchases.

### Base URL
```
https://yourdomain.com/api
```

## Authentication
All API requests must include a valid `api_key`, which can be obtained from [tzsmmpay.com](https://tzsmmpay.com/reseller).

## Endpoints

### 1. Add Plan
**Parameters:**
| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| api_key | string | Yes | Your reseller API key |
| action | string | Yes | Must be `add` |
| service | int | Yes | Plan ID |
| link | string | Yes | User link |
| email | string | Yes | Customer email |

**Response:**
```json
{
  "order": 12345
}
```

### 2. Get Order Status
**Parameters:**
| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| api_key | string | Yes | Your reseller API key |
| action | string | Yes | Must be `status` |
| order | int | No | Order ID (for a single order) |
| orders | string | No | Comma-separated order IDs (for multiple orders) |

**Response (Single Order):**
```json
{
  "charge": "0.27819",
  "start_count": "3572",
  "status": "Partial",
  "remains": "157",
  "currency": "USD"
}
```

**Response (Multiple Orders):**
```json
{
  "1": {
    "charge": "0.27819",
    "start_count": "3572",
    "status": "Partial",
    "remains": "157",
    "currency": "USD"
  },
  "10": {
    "error": "Incorrect order ID"
  },
  "100": {
    "charge": "1.44219",
    "start_count": "234",
    "status": "In progress",
    "remains": "10",
    "currency": "USD"
  }
}
```

## Error Responses
| Error | Message |
|--------|---------|
| 401 | `Invalid API key` |
| 400 | `Incorrect request` |
| 404 | `Invalid order ID` |
| 402 | `You don't have sufficient balance` |

## Notes
- Ensure the API key is valid.
- Orders can be checked in bulk using the `orders` parameter.
- Resellers must maintain sufficient balance before making purchases.

For support, visit [tzsmmpay.com](https://tzsmmpay.com/reseller).

