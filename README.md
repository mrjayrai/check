# API Endpoints Overview

Below is a markdown summary of the 17 API endpoints:

---

### 1. **POST `/api/users/register`**
Registers a new user.  
**Body:**
```json
{
  "name": "string",
  "email": "string",
  "password": "string",
  "role": "superAdmin|admin|warehouseManager|salesMan|customer|picker",
  "address": "string",
  "storeName": "string (if warehouseManager)",
  "subscription": "subscriptionId (required except for superAdmin)",
  "assignedTo": "userId (if salesMan)"
}
```

---

### 2. **POST `/api/users/login`**
Logs in a user.  
**Body:**
```json
{
  "email": "string",
  "password": "string"
}
```

---

### 3. **POST `/api/users/model/add`**
Adds a new subscription type.  
**Body:**
```json
{
  "subscriptionCode": "string",
  "subscriptionType": "Gold|Diamond",
  "applications": ["string", ...]
}
```

---

### 4. **GET `/api/users/model/get`**
Gets all subscription types.  
_No body required._

---

### 5. **POST `/api/warehouse/register`**
Registers a new warehouse.  
**Body:**
```json
{
  "name": "string",
  "location": "string",
  "owner": "userId",
  "manager": "userId (optional)"
}
```

---

### 6. **POST `/api/warehouse/getwarehouse/manager`**
Gets warehouses managed by a manager.  
**Body:**
```json
{
  "managerId": "userId"
}
```

---

### 7. **POST `/api/warehouse/getlowcount`**
Gets products with low stock in a warehouse.  
**Body:**
```json
{
  "warehouse": "warehouseId",
  "qt": number
}
```

---

### 8. **POST `/api/warehouse/outofstock`**
Gets out-of-stock products in a warehouse.  
**Body:**
```json
{
  "warehouse": "warehouseId"
}
```

---

### 9. **POST `/api/inventory/add`**
Adds inventory and products.  
**Form-data:**  
- `warehouse`: string  
- `owner`: string  
- `products`: JSON stringified array  
- Images: `images_0`, `images_1`, ... (files for each product)

---

### 10. **PUT `/api/inventory/update/:inventoryId`**
Updates inventory products.  
**Form-data:**  
- `products`: JSON stringified array  
- Images: `images_0`, `images_1`, ... (files for each product)

---

### 11. **POST `/api/store/add`**
Adds a new store.  
**Body:**
```json
{
  "name": "string",
  "location": "string",
  "contactNumber": "string",
  "email": "string",
  "openingHours": "string",
  "area": "string"
}
```

---

### 12. **POST `/api/salesmate/assign-market`**
Assigns a market (calendar) to a salesman.  
**Body:**
```json
{
  "startDate": "YYYY-MM-DD",
  "endDate": "YYYY-MM-DD",
  "routes": [
    {
      "dayOfWeek": "Sunday|Monday|...|Saturday",
      "stores": ["storeId", ...],
      "repeatWeekly": true|false
    }
  ],
  "assignedTo": "userId",
  "assignedBy": "userId"
}
```

---

### 13. **POST `/api/salesmate/get-calendar`**
Gets calendar summary for a salesman.  
**Body:**
```json
{
  "salesmanId": "userId",
  "startDate": "YYYY-MM-DD",
  "endDate": "YYYY-MM-DD"
}
```

---

### 14. **POST `/api/salesmate/add-catalogue`**
Adds or updates a catalogue for an admin.  
**Body:**
```json
{
  "adminId": "userId",
  "products": ["productId", ...]
}
```

---

### 15. **POST `/api/salesmate/get-catalogue`**
Gets catalogue products for an admin.  
**Body:**
```json
{
  "adminId": "userId"
}
```

---

### 16. **POST `/api/salesmate/generate-order`**
Generates a new order.  
**Body:**
```json
{
  "storeId": "storeId",
  "products": [
    {
      "product": "productId",
      "quantity": number,
      "price": number,
      "negotiationPrice": number
    }
  ],
  "orderedBy": "userId",
  "ModeofPayment": "COD|Advance|Online",
  "userOrderId": "orderId (optional)",
  "notes": "string (optional)"
}
```

---

### 17. **POST `/api/salesmate/get-calendar-area`**
Gets calendar stores by area for a salesman.  
**Body:**
```json
{
  "salesmanId": "userId",
  "startDate": "YYYY-MM-DD",
  "endDate": "YYYY-MM-DD",
  "area": "string"
}
```

---
