
# ChainBallot API - Modify Election Endpoint Documentation

This documentation provides frontend developers with the necessary information to interact with the `PATCH /election` endpoint of the ChainBallot API.

## Base URL

The base URL for the API is:

```
https://chainballot-backend.onrender.com/gateway/v1/
```

## Endpoint

### PATCH `/election`

This endpoint allows you to modify an election’s details by updating the `election_address`. You must provide the election’s `id` to identify which election to modify.

---

### Request

- **Method**: `PATCH`
- **URL**: `/election`
- **Full URL**: `https://chainballot-backend.onrender.com/gateway/v1/election`
- **Headers**:
    - `Content-Type`: `application/json`
    - `X-Custom-Header`: `YOUR_CUSTOM_VALUE_HERE`

### Request Body

The request body must include the following fields:

- **`election_address`**: The new election address that will replace the old one.
- **`id`**: The ID of the election you want to modify.

#### Example Request Body

```json
{
    "requestBody": {
        "election_address": "0xabcdef1234567890abcdef123456781234567890",
        "id": "6712508abfe61148ea8b471b"
    }
}
```

---

### Example Request Using Axios

Here’s an example of how to make a `PATCH` request using Axios to modify an election:

```javascript
import axios from 'axios';

const modifyElection = async () => {
    const url = 'https://chainballot-backend.onrender.com/gateway/v1/election';
    const requestBody = {
        election_address: "0xabcdef1234567890abcdef123456781234567890",
        id: "6712508abfe61148ea8b471b"
    };

    try {
        const response = await axios.patch(url, {
            requestBody: requestBody
        }, {
            headers: {
                'Content-Type': 'application/json',
                'X-Custom-Header': 'YOUR_CUSTOM_VALUE_HERE'
            }
        });
        if (response.status === 204) {
            console.log('Election modified successfully (No Content).');
        }
    } catch (error) {
        console.error('Error modifying election:', error.response ? error.response.data : error.message);
    }
};

modifyElection();
```

---

### Response

#### Success Response

- **Status Code**: `204 No Content`
- **Description**: The election was successfully updated. No content is returned in the response body.

---

#### Error Responses

- **Status Code**: `400 Bad Request`
- **Description**: If the `requestBody` is invalid or the election could not be updated.

#### Example Error Response

```json
{
    "success": false,
    "message": "requestBody must be a non-empty object."
}
```

```json
{
    "success": false,
    "message": "Election could not be updated"
}
```

---

## Summary

This documentation provides frontend developers with an overview of how to make a `PATCH` request to modify election data using the ChainBallot API. Be sure to include the correct headers and provide the required fields (`election_address` and `id`) in the request body.

When the request is successful, a `204 No Content` status will be returned, indicating that the election was modified successfully but without any response body.
