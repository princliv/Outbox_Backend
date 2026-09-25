# API Endpoints with Request Body/Payload - Part 2

**Services, Trainers & Admin**

This document lists API endpoints that require a request body or payload for Sub Services, Trainer Management, and Admin services.

**Base URL:** `/api/v1`

---

## 4. Sub Service Endpoints (`/api/v1/subservice`)

### 4.1 Create Sub Service
**POST** `/subservice/createSubService`
**Content-Type:** `multipart/form-data`
```
image: <file>
name: "Haircut"
serviceTypeId: "service_id"
groomingDetails: "[{\"weightType\":\"small\",\"price\":100,\"description\":\"Small pet\"}]"
```

### 4.2 Update Sub Service
**PUT** `/subservice/updateSubService/:subServiceId`
**Content-Type:** `multipart/form-data`
```
image: <file>
name: "Haircut Updated"
groomingDetails: "[{\"weightType\":\"small\",\"price\":120}]"
```

### 4.3 Get All Sub Services
**POST** `/subservice/getAllSubService`
```json
{
  "page": 1,
  "limit": 10,
  "search": "haircut"
}
```

---

## 5. Trainer Endpoints (`/api/v1/trainer`)

### 5.1 Create Trainer
**POST** `/trainer/create-trainer`
**Content-Type:** `multipart/form-data`
```
profile_image: <file>
email: "trainer@example.com"
first_name: "John"
last_name: "Doe"
phone_number: "1234567890"
gender: "male"
address: "123 Main St"
age: 30
country: "country_id"
city: "city_id"
specialization: "Yoga"
experience: "5 years"
experienceYear: 5
password: "password123"
serviceProvider: "[service_id1, service_id2]"
```

### 5.2 Update Trainer
**PUT** `/trainer/update-trainer/:id`
**Content-Type:** `multipart/form-data`
```
profile_image: <file>
first_name: "John"
last_name: "Doe Updated"
specialization: "Advanced Yoga"
```

### 5.3 Update Trainer Status
**PATCH** `/trainer/update-trainer-status/:trainerId`
```json
{
  "status": "active"
}
```

### 5.4 Update Trainer Profile (By Trainer)
**PUT** `/trainer/update-trainer-profiles/:trainerId`
**Content-Type:** `multipart/form-data`
```
profile_image: <file>
first_name: "John"
last_name: "Doe"
specialization: "Yoga"
```

### 5.5 Get All Assigned Jobs
**POST** `/trainer/get-all-assigned-jobs`
```json
{
  "page": 1,
  "limit": 10,
  "status": "assigned"
}
```

### 5.6 Trainer Check-in
**POST** `/trainer/checkin/:orderDetailsId`
```json
{
  "checkinTime": "2024-01-01T10:00:00Z",
  "latitude": 25.0772,
  "longitude": 55.1398
}
```

### 5.7 Initiate Checkout
**POST** `/trainer/initiate-checkout/:orderDetailsId`
```json
{
  "notes": "Service completed successfully"
}
```

### 5.8 Complete Checkout
**POST** `/trainer/complete-checkout/:orderDetailsId`
```json
{
  "completionTime": "2024-01-01T11:00:00Z",
  "images": ["url1", "url2"]
}
```

---

## 6. Admin Endpoints (`/api/v1/admin`)

### 6.1 Create Promo Code
**POST** `/admin/create-promo-code`
**Content-Type:** `multipart/form-data`
```
image: <file> (optional)
code: "SAVE20" (required)
discountType: "percentage" (required)
discountValue: 20 (required)
description: "Promo code description" (optional)
isActive: true (optional)
is_validation_date: true (optional)
startDate: "2024-01-01" (optional, required if is_validation_date is true)
endDate: "2024-12-31" (optional, required if is_validation_date is true)
apply_offer_after_orders: 5 (optional)
minOrderAmount: 100 (optional)
maxDiscountAmount: 50 (optional)
maxUses: 100 (required)
termsAndConditions: "Terms and conditions text" (required)
```

### 6.2 Update Promo Code
**PUT** `/admin/update-promo-code/:id`
**Content-Type:** `multipart/form-data`
```
image: <file> (optional)
code: "SAVE25" (optional)
discountType: "percentage" (optional)
discountValue: 25 (optional)
description: "Updated description" (optional)
isActive: true (optional)
is_validation_date: true (optional)
startDate: "2024-01-01" (optional)
endDate: "2024-12-31" (optional)
apply_offer_after_orders: 5 (optional)
minOrderAmount: 100 (optional)
maxDiscountAmount: 50 (optional)
maxUses: 100 (optional)
termsAndConditions: "Updated terms" (optional)
```

### 6.3 Get Promo Code by ID
**GET** `/admin/get-promo-code-by-id/:id`
**Headers:** `Authorization: Bearer <access_token>`
**No request body required**

### 6.4 Get All Promo Codes
**POST** `/admin/get-all-promo-codes`
**Headers:** `Authorization: Bearer <access_token>`
**No request body required**
*Note: Returns all promo codes sorted by creation date (newest first)*

### 6.5 Delete Promo Code
**DELETE** `/admin/delete-promo-code/:id`
**Headers:** `Authorization: Bearer <access_token>`
**No request body required**

### 6.6 Get All Subservice Rating Reviews
**GET** `/admin/get-all-subservice-rating-review/:subServiceId`
**Headers:** `Authorization: Bearer <access_token>`
**No request body required**

### 6.7 Get All Orders
**GET** `/admin/get-all-orders`
**Headers:** `Authorization: Bearer <access_token>`
**No request body required**

### 6.8 Get Dashboard Details
**GET** `/admin/get-dashboard-details`
**Headers:** `Authorization: Bearer <access_token>`
**No request body required**

### 6.9 Get Month Wise Data
**GET** `/admin/get-month-wise-data?year=2024`
**Headers:** `Authorization: Bearer <access_token>`
**Query Parameters:**
- `year` (optional): Year for which to get data. Defaults to current year if not provided.
**No request body required**

### 6.10 Get Planner Dashboard
**POST** `/admin/get-planner-dashboard`
```json
{
  "bookingDate": "2024-01-01",
  "subServiceId": "subservice_id" (optional)
}
```

### 6.11 Get Available Groomers
**POST** `/admin/get-all-available-groomers`
```json
{
  "groomerId": "groomer_id",
  "timeSlotId": "timeslot_id",
  "date": "2024-01-01"
}
```

### 6.12 Get Available Groomers for Booking
**POST** `/admin/get-all-available-groomers-booking`
```json
{
  "date": "2024-01-01",
  "timeslot": "timeslot_id",
  "subServiceId": "subservice_id"
}
```

### 6.13 Create Article
**POST** `/admin/create-artical`
**Content-Type:** `multipart/form-data`
```
image: <file> (required)
title: "Article Title" (required)
description: "Article description" (optional)
```

### 6.14 Get All Articles
**GET** `/admin/get-all-articals`
**Headers:** `Authorization: Bearer <access_token>`
**No request body required**

### 6.15 Get Article by ID
**GET** `/admin/get-artical/:id`
**Headers:** `Authorization: Bearer <access_token>`
**No request body required**

### 6.16 Update Article
**PUT** `/admin/update-artical/:id`
**Content-Type:** `multipart/form-data`
```
image: <file> (optional)
title: "Updated Title" (optional)
description: "Updated description" (optional)
```

### 6.17 Delete Article
**DELETE** `/admin/delete-artical/:id`
**Headers:** `Authorization: Bearer <access_token>`
**No request body required**

---

**Note:** Refer to the main README.md for complete endpoint documentation including responses and authentication requirements.

