# API Reference

This document provides technical reference for the Units API used by the web application.

## Overview

The Units backend API is a RESTful service that provides data and operations for the warehouse management system. The frontend communicates with this API to perform all business operations.

**Base URL**: `https://api.units.compass-dx.com/api/`

## Authentication

### Authentication Method
The API uses JWT (JSON Web Token) based authentication.

### Login
**Endpoint**: `POST /auth/login`

**Request Body**:
```json
{
  "email": "user@example.com",
  "password": "SecurePassword123!",
  "rememberMe": true
}
```

**Response**:
```json
{
  "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
  "expiryDate": "2024-12-31T23:59:59Z",
  "user": {
    "id": "user-123",
    "email": "user@example.com",
    "name": "John Doe",
    "userType": "A",
    "customerId": null
  }
}
```

**User Types**:
- `A`: Admin
- `C`: Customer

### Token Refresh
**Endpoint**: `POST /auth/refresh`

**Headers**:
```
Authorization: Bearer {token}
```

**Response**:
```json
{
  "token": "new-jwt-token",
  "expiryDate": "2024-12-31T23:59:59Z"
}
```

### Authenticated Requests
All subsequent requests must include the token in the Authorization header:

```
Authorization: Bearer {token}
```

## Common Patterns

### Pagination
List endpoints support pagination via query parameters:

**Parameters**:
- `page`: Page number (1-indexed)
- `perPage`: Results per page (default: 30, max: 100)

**Response includes**:
```json
{
  "data": [...],
  "pagination": {
    "currentPage": 1,
    "totalPages": 10,
    "totalRecords": 297,
    "perPage": 30
  }
}
```

### Filtering
List endpoints support filtering via query parameters:

**Example**:
```
GET /inboundrequests?status=pending&customerId=123
```

### Sorting
Use `sortBy` and `sortOrder` parameters:

**Example**:
```
GET /sku?sortBy=createdAt&sortOrder=desc
```

### Date Formats
- ISO 8601 format: `2024-12-06T12:00:00Z`
- Dates without time: `2024-12-06`

## Resource Endpoints

### 1. Inbound Requests

#### List Inbound Requests
**Endpoint**: `GET /inboundrequests`

**Query Parameters**:
- `customerId`: Filter by customer
- `status`: Filter by status (request, grn, counting, qc, putaway, completed)
- `fromDate`: Filter from date
- `toDate`: Filter to date
- `page`: Page number
- `perPage`: Results per page

**Response**:
```json
{
  "data": [
    {
      "id": "inbound-123",
      "referenceNumber": "IN-2024-0001",
      "customerId": "customer-456",
      "customerName": "ACME Corp",
      "supplierId": "supplier-789",
      "supplierName": "Supplier Inc",
      "expectedDate": "2024-12-10",
      "timeSlot": "09:00-12:00",
      "status": "request",
      "items": [
        {
          "skuId": "sku-001",
          "skuCode": "PROD-001",
          "description": "Product 1",
          "expectedQuantity": 100,
          "receivedQuantity": 0
        }
      ],
      "createdAt": "2024-12-06T10:00:00Z",
      "createdBy": "user-123"
    }
  ],
  "pagination": {...}
}
```

#### Create Inbound Request
**Endpoint**: `POST /inboundrequests`

**Request Body**:
```json
{
  "customerId": "customer-456",
  "supplierId": "supplier-789",
  "expectedDate": "2024-12-10",
  "timeSlotId": "timeslot-001",
  "specialInstructions": "Handle with care",
  "items": [
    {
      "skuId": "sku-001",
      "expectedQuantity": 100
    }
  ]
}
```

**Response**: Returns created inbound request object

#### Update Inbound Request
**Endpoint**: `PUT /inboundrequests/{id}`

#### Delete Inbound Request
**Endpoint**: `DELETE /inboundrequests/{id}`

#### Goods Receiving
**Endpoint**: `POST /inboundrequests/{id}/receive`

**Request Body**:
```json
{
  "vehicleLicense": "ABC-123",
  "driverName": "John Driver",
  "sealNumber": "SEAL-456",
  "receivedAt": "2024-12-06T14:30:00Z",
  "photos": ["base64-encoded-image-1", "base64-encoded-image-2"]
}
```

#### Counting
**Endpoint**: `POST /inboundrequests/{id}/count`

**Request Body**:
```json
{
  "items": [
    {
      "skuId": "sku-001",
      "actualQuantity": 98,
      "batchNumber": "BATCH-2024-001",
      "serialNumbers": ["SN-001", "SN-002"],
      "notes": "2 units damaged"
    }
  ]
}
```

#### Quality Control
**Endpoint**: `POST /inboundrequests/{id}/qc`

**Request Body**:
```json
{
  "items": [
    {
      "skuId": "sku-001",
      "acceptedQuantity": 95,
      "rejectedQuantity": 3,
      "qcStatus": "partial",
      "notes": "3 units failed inspection",
      "photos": ["base64-encoded-image"]
    }
  ]
}
```

#### Putaway
**Endpoint**: `POST /inboundrequests/{id}/putaway`

**Request Body**:
```json
{
  "items": [
    {
      "skuId": "sku-001",
      "quantity": 95,
      "locationId": "location-001",
      "locationCode": "A-01-05"
    }
  ]
}
```

### 2. Outbound Requests (Orders)

#### List Orders
**Endpoint**: `GET /outboundrequests`

**Query Parameters**:
- `customerId`: Filter by customer
- `status`: Filter by status
- `fromDate`, `toDate`: Date range
- `page`, `perPage`: Pagination

**Response**:
```json
{
  "data": [
    {
      "id": "order-123",
      "orderNumber": "ORD-2024-0001",
      "customerId": "customer-456",
      "customerName": "ACME Corp",
      "deliveryAddress": {...},
      "requestedDate": "2024-12-15",
      "status": "unassigned",
      "items": [
        {
          "skuId": "sku-001",
          "skuCode": "PROD-001",
          "quantity": 50,
          "allocatedQuantity": 50,
          "pickedQuantity": 0
        }
      ],
      "shippingMethod": "carrier",
      "carrierId": "carrier-001",
      "createdAt": "2024-12-06T10:00:00Z"
    }
  ],
  "pagination": {...}
}
```

#### Create Order
**Endpoint**: `POST /outboundrequests`

**Request Body**:
```json
{
  "customerId": "customer-456",
  "deliveryAddressId": "address-789",
  "requestedDate": "2024-12-15",
  "timeSlotId": "timeslot-002",
  "shippingMethod": "carrier",
  "carrierId": "carrier-001",
  "serviceLevel": "standard",
  "specialInstructions": "Deliver to reception",
  "items": [
    {
      "skuId": "sku-001",
      "quantity": 50
    }
  ]
}
```

#### Assign Picker
**Endpoint**: `POST /outboundrequests/{id}/assign`

**Request Body**:
```json
{
  "pickerId": "user-picker-001"
}
```

#### Record Picking
**Endpoint**: `POST /outboundrequests/{id}/pick`

**Request Body**:
```json
{
  "items": [
    {
      "skuId": "sku-001",
      "pickedQuantity": 50,
      "locationId": "location-001",
      "batchNumber": "BATCH-2024-001"
    }
  ]
}
```

#### Outbound QC
**Endpoint**: `POST /outboundrequests/{id}/qc`

**Request Body**:
```json
{
  "qcStatus": "passed",
  "notes": "All items verified"
}
```

#### Record Packing
**Endpoint**: `POST /outboundrequests/{id}/pack`

**Request Body**:
```json
{
  "packages": [
    {
      "packageType": "box",
      "length": 40,
      "width": 30,
      "height": 20,
      "weight": 5.5,
      "trackingNumber": "TRACK-123456"
    }
  ]
}
```

#### Dispatch Order
**Endpoint**: `POST /outboundrequests/{id}/dispatch`

**Request Body**:
```json
{
  "dispatchedAt": "2024-12-06T16:00:00Z",
  "carrier": "carrier-001",
  "trackingNumber": "TRACK-123456"
}
```

### 3. SKU Management

#### List SKUs
**Endpoint**: `GET /sku`

**Query Parameters**:
- `customerId`: Filter by customer
- `categoryId`: Filter by category
- `brandId`: Filter by brand
- `search`: Search in code/description
- `page`, `perPage`: Pagination

**Response**:
```json
{
  "data": [
    {
      "id": "sku-001",
      "skuCode": "PROD-001",
      "description": "Product 1 Description",
      "categoryId": "category-001",
      "categoryName": "Electronics",
      "brandId": "brand-001",
      "brandName": "BrandX",
      "supplierId": "supplier-001",
      "dimensions": {
        "length": 10,
        "width": 8,
        "height": 5,
        "unit": "cm"
      },
      "weight": {
        "value": 0.5,
        "unit": "kg"
      },
      "unitOfMeasure": "piece",
      "barcode": "1234567890123",
      "imageUrl": "https://cdn.example.com/images/sku-001.jpg",
      "reorderPoint": 10,
      "safetyStock": 5,
      "currentStock": 150,
      "createdAt": "2024-01-01T00:00:00Z"
    }
  ],
  "pagination": {...}
}
```

#### Create SKU
**Endpoint**: `POST /sku`

**Request Body**:
```json
{
  "skuCode": "PROD-002",
  "description": "Product 2 Description",
  "customerId": "customer-456",
  "categoryId": "category-001",
  "brandId": "brand-001",
  "supplierId": "supplier-001",
  "dimensions": {
    "length": 10,
    "width": 8,
    "height": 5,
    "unit": "cm"
  },
  "weight": {
    "value": 0.5,
    "unit": "kg"
  },
  "unitOfMeasure": "piece",
  "barcode": "1234567890124",
  "images": ["base64-encoded-image"],
  "reorderPoint": 10,
  "safetyStock": 5
}
```

#### Update SKU
**Endpoint**: `PUT /sku/{id}`

#### Delete SKU
**Endpoint**: `DELETE /sku/{id}`

#### Get Stock Levels
**Endpoint**: `GET /sku/{id}/stock`

**Response**:
```json
{
  "skuId": "sku-001",
  "totalStock": 150,
  "availableStock": 140,
  "allocatedStock": 10,
  "locations": [
    {
      "locationId": "location-001",
      "locationCode": "A-01-05",
      "quantity": 100,
      "batchNumber": "BATCH-2024-001",
      "expiryDate": "2025-12-31"
    }
  ]
}
```

### 4. Warehouse Management

#### List Warehouses
**Endpoint**: `GET /warehouses`

**Response**:
```json
{
  "data": [
    {
      "id": "warehouse-001",
      "name": "Main Warehouse",
      "code": "WH-MAIN",
      "address": {
        "street": "123 Warehouse St",
        "city": "Riyadh",
        "country": "Saudi Arabia",
        "postalCode": "12345"
      },
      "contactPerson": "Warehouse Manager",
      "phone": "+966XXXXXXXXX",
      "totalCapacity": 10000,
      "usedCapacity": 6500,
      "areas": [
        {
          "id": "area-001",
          "name": "Zone A",
          "code": "A",
          "areaType": "ambient"
        }
      ]
    }
  ]
}
```

#### Get Warehouse Details
**Endpoint**: `GET /warehouses/{id}`

Includes full hierarchy: Areas → Racks → Locations

#### List Locations
**Endpoint**: `GET /warehouses/{warehouseId}/locations`

**Query Parameters**:
- `areaId`: Filter by area
- `rackId`: Filter by rack
- `available`: Filter available locations (true/false)

### 5. Customer Management

#### List Customers
**Endpoint**: `GET /customers`

**Response**:
```json
{
  "data": [
    {
      "id": "customer-001",
      "companyName": "ACME Corporation",
      "taxId": "123456789",
      "email": "contact@acme.com",
      "phone": "+966XXXXXXXXX",
      "address": {...},
      "status": "active",
      "contractStartDate": "2024-01-01",
      "pricingTier": "premium"
    }
  ]
}
```

#### Create Customer
**Endpoint**: `POST /customers`

#### Update Customer
**Endpoint**: `PUT /customers/{id}`

#### Customer Addresses
**Endpoint**: `GET /customers/{id}/addresses`

**Endpoint**: `POST /customers/{id}/addresses`

### 6. User Management

#### List Users
**Endpoint**: `GET /users`

**Query Parameters**:
- `userType`: Filter by type (A/C)
- `customerId`: Filter by customer
- `status`: Filter by status (active/inactive)

**Response**:
```json
{
  "data": [
    {
      "id": "user-001",
      "email": "user@example.com",
      "name": "John Doe",
      "userType": "C",
      "customerId": "customer-001",
      "status": "active",
      "lastLogin": "2024-12-06T10:00:00Z"
    }
  ]
}
```

#### Create User
**Endpoint**: `POST /users`

**Request Body**:
```json
{
  "email": "newuser@example.com",
  "name": "Jane Smith",
  "userType": "C",
  "customerId": "customer-001",
  "sendInvitation": true
}
```

#### Update User
**Endpoint**: `PUT /users/{id}`

#### Deactivate User
**Endpoint**: `DELETE /users/{id}` or `PUT /users/{id}` with `status: "inactive"`

### 7. Reporting

#### Inbound Report
**Endpoint**: `GET /reports/inbound`

**Query Parameters**:
- `fromDate`: Start date
- `toDate`: End date
- `customerId`: Filter by customer
- `supplierId`: Filter by supplier
- `warehouseId`: Filter by warehouse

**Response**:
```json
{
  "summary": {
    "totalInbounds": 50,
    "totalItems": 5000,
    "averageProcessingTime": 2.5,
    "discrepancyRate": 2.3
  },
  "details": [...]
}
```

#### Order Report
**Endpoint**: `GET /reports/orders`

**Query Parameters**:
- `fromDate`, `toDate`: Date range
- `customerId`: Filter by customer
- `status`: Filter by status

**Response**:
```json
{
  "summary": {
    "totalOrders": 100,
    "totalItems": 2500,
    "fulfillmentRate": 98.5,
    "averageCycleTime": 1.8
  },
  "details": [...]
}
```

#### SKU Report
**Endpoint**: `GET /reports/sku`

**Query Parameters**:
- `customerId`: Filter by customer
- `categoryId`: Filter by category

**Response**:
```json
{
  "summary": {
    "totalSKUs": 500,
    "totalValue": 250000,
    "lowStockItems": 15,
    "outOfStockItems": 3
  },
  "skus": [...]
}
```

#### Stock Movement Report
**Endpoint**: `GET /reports/stock-movements`

**Query Parameters**:
- `fromDate`, `toDate`: Date range
- `skuId`: Filter by SKU
- `customerId`: Filter by customer
- `movementType`: Filter by type (inbound/outbound/adjustment)

**Response**:
```json
{
  "data": [
    {
      "date": "2024-12-06T14:30:00Z",
      "skuCode": "PROD-001",
      "movementType": "inbound",
      "quantity": 100,
      "fromLocation": null,
      "toLocation": "A-01-05",
      "referenceNumber": "IN-2024-0001",
      "notes": "New stock receipt"
    }
  ]
}
```

### 8. Master Data

#### Suppliers
- `GET /suppliers` - List suppliers
- `POST /suppliers` - Create supplier
- `PUT /suppliers/{id}` - Update supplier
- `DELETE /suppliers/{id}` - Delete supplier

#### Brands
- `GET /brands` - List brands
- `POST /brands` - Create brand
- `PUT /brands/{id}` - Update brand
- `DELETE /brands/{id}` - Delete brand

#### Carriers
- `GET /carriers` - List carriers
- `POST /carriers` - Create carrier
- `PUT /carriers/{id}` - Update carrier
- `DELETE /carriers/{id}` - Delete carrier

#### Packing Materials
- `GET /packingmaterials` - List materials
- `POST /packingmaterials` - Create material
- `PUT /packingmaterials/{id}` - Update material
- `DELETE /packingmaterials/{id}` - Delete material

## Error Handling

### HTTP Status Codes
- `200 OK`: Successful request
- `201 Created`: Resource created successfully
- `400 Bad Request`: Invalid request data
- `401 Unauthorized`: Authentication required or failed
- `403 Forbidden`: Insufficient permissions
- `404 Not Found`: Resource not found
- `409 Conflict`: Resource conflict (e.g., duplicate SKU code)
- `422 Unprocessable Entity`: Validation errors
- `500 Internal Server Error`: Server error

### Error Response Format
```json
{
  "error": {
    "code": "VALIDATION_ERROR",
    "message": "SKU code already exists",
    "details": {
      "field": "skuCode",
      "value": "PROD-001"
    }
  }
}
```

### Common Error Codes
- `INVALID_EMAIL_PASSWORD`: Login credentials incorrect
- `USER_NOT_FOUND`: User doesn't exist
- `INVALID_TOKEN_ACCESS`: Token invalid or expired
- `SKU_CODE_ALREADY_EXISTS`: Duplicate SKU code
- `TENANT_EMAIL_ALREADY_BEING_USED`: Email already in use

## Rate Limiting

The API may implement rate limiting to prevent abuse. If rate limited, you'll receive:

**Status**: `429 Too Many Requests`

**Headers**:
```
X-RateLimit-Limit: 1000
X-RateLimit-Remaining: 0
X-RateLimit-Reset: 1638316800
```

## Webhooks (If Supported)

If the API supports webhooks, subscribers can receive real-time notifications for events:

### Event Types
- `inbound.received`: Goods received
- `inbound.completed`: Inbound completed
- `order.created`: New order
- `order.dispatched`: Order dispatched
- `inventory.low_stock`: Low stock alert

### Webhook Payload Example
```json
{
  "event": "order.dispatched",
  "timestamp": "2024-12-06T16:00:00Z",
  "data": {
    "orderId": "order-123",
    "trackingNumber": "TRACK-123456"
  }
}
```

## Best Practices

1. **Always include Authorization header** for authenticated requests
2. **Handle token expiry** - Refresh token before expiry
3. **Implement retry logic** for transient errors (5xx)
4. **Validate data client-side** before sending to API
5. **Use pagination** for large datasets
6. **Cache reference data** (suppliers, brands, etc.) to reduce API calls
7. **Log API errors** for debugging
8. **Implement timeout** for API requests (30-60 seconds)

## Next Steps

- Review [Architecture](./architecture.md) for system design
- See [Configuration](./configuration.md) for API setup
- Check [Troubleshooting](./troubleshooting.md) for common API issues
