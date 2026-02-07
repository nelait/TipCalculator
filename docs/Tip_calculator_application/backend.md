```markdown
# Tip Calculator Application Backend Implementation Guide

**Version:** 1.0  
**Date:** 2/6/2026  

## 1. API Design

### Key Endpoints

- **POST /calculate-tip**
  - **Description:** Calculate the tip based on the total bill and desired tip percentage.
  - **Method:** POST
  - **Payload:**
    ```json
    {
      "total_bill": 100.0,
      "tip_percentage": 15
    }
    ```
  - **Response:**
    ```json
    {
      "total_bill": 100.0,
      "tip_percentage": 15,
      "tip_amount": 15.0,
      "total_with_tip": 115.0
    }
    ```

- **GET /tip-percentages**
  - **Description:** Retrieve a list of common tip percentages.
  - **Method:** GET
  - **Response:**
    ```json
    {
      "tip_percentages": [10, 15, 18, 20]
    }
    ```

## 2. Data Models

### Database Tables/Collections

- **TipsCollection**
  - **Fields:**
    - `id` (Primary Key, UUID)
    - `total_bill` (Float)
    - `tip_percentage` (Integer)
    - `tip_amount` (Float)
    - `total_with_tip` (Float)
    - `timestamp` (Datetime)

## 3. Business Logic

1. **Calculate Tip:**
   - Retrieve the `total_bill` and `tip_percentage` from the request body.
   - Calculate `tip_amount` as `(total_bill * tip_percentage) / 100`.
   - Calculate `total_with_tip` as `total_bill + tip_amount`.
   - Store the calculation data in `TipsCollection` for future analytics.

2. **Fetch Tip Percentages:**
   - Provide a predefined list of common tip percentages for client use.

## 4. Security

- **Authentication:**
  - Use JWT (JSON Web Tokens) for user authentication. Each request must include a valid token in the Authorization header.

- **Authorization:**
  - Ensure that only authenticated users can perform tip calculations. Use middleware to verify token validity.

## 5. Performance

- **Caching:**
  - Use in-memory caching (e.g., Redis) for storing frequently accessed data, such as common tip percentages.

- **Database Indexing:**
  - Index `total_bill` and `timestamp` fields in `TipsCollection` to optimize query performance for analytics.

## 6. Code Examples

### Calculate Tip Function

```python
from datetime import datetime

def calculate_tip(total_bill, tip_percentage):
    tip_amount = (total_bill * tip_percentage) / 100
    total_with_tip = total_bill + tip_amount
    return {
        "total_bill": total_bill,
        "tip_percentage": tip_percentage,
        "tip_amount": tip_amount,
        "total_with_tip": total_with_tip
    }

def store_tip_data(db, data):
    data['timestamp'] = datetime.now()
    db.TipsCollection.insert_one(data)
```

### JWT Authentication Middleware

```python
from functools import wraps
from flask import request, jsonify
import jwt

SECRET_KEY = "your_secret_key"

def token_required(f):
    @wraps(f)
    def decorated(*args, **kwargs):
        token = request.headers.get('Authorization')
        if not token:
            return jsonify({'message': 'Token is missing!'}), 403
        try:
            jwt.decode(token, SECRET_KEY, algorithms=["HS256"])
        except jwt.ExpiredSignatureError:
            return jsonify({'message': 'Token has expired!'}), 403
        except jwt.InvalidTokenError:
            return jsonify({'message': 'Invalid token!'}), 403
        return f(*args, **kwargs)
    return decorated
```

This guide provides a comprehensive structure to implement the backend of a tip calculator application efficiently and securely.
```