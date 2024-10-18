# ChainBallot API - Create Election Endpoint Documentation

This documentation provides frontend developers with the necessary information to interact with the `POST /election` endpoint of the ChainBallot API.

## Base URL

The base URL for the API is:

```
https://chainballot-backend.onrender.com/gateway/v1/
```

## Endpoint

### POST `/election`

This endpoint is used to create a new election by submitting a request with the necessary election details.

---

### Request

- **Method**: `POST`
- **URL**: `/election`
- **Full URL**: `https://chainballot-backend.onrender.com/gateway/v1/election`
- **Headers**:
    - `Content-Type`: `application/json`
    - `X-Custom-Header`: `YOUR_CUSTOM_VALUE_HERE`

### Request Body

The request body must include a JSON object with a `requestBody` field that contains the election details. Below is an example of a valid request body:

#### Example Valid Request Body

```json
{
    "requestBody": {
        "election_title": "The first presidential election",
        "election_description": "This is the first ever presidential election that will be held on Chainballot",
        "election_presiding_officer": "0x1234567890abcdef1234567890abcdef12345678",
        "election_start_date": "2024-10-20T09:00:00.000Z",
        "election_end_date": "2024-10-25T09:00:00.000Z"
    }
}
```

### Response

Upon successful creation of the election, the server will respond with a status code of `201 Created`, along with a JSON object containing the details of the newly created election.

#### Example Successful Response

```json
{
    "success": true,
    "data": {
        "_id": "64c12345abc678def9012345",
        "election_title": "The first presidential election",
        "election_description": "This is the first ever presidential election that will be held on Chainballot",
        "election_presiding_officer": "0x1234567890abcdef1234567890abcdef12345678",
        "election_start_date": "2024-10-20T09:00:00.000Z",
        "election_end_date": "2024-10-25T09:00:00.000Z",
        "createdAt": "2024-10-15T10:30:00.000Z",
        "__v": 0
    }
}
```

---

### Error Handling

In the case of an invalid request, the API will return an error response with a relevant status code and message.

#### Example Error Response

```json
{
    "success": false,
    "message": "requestBody must be a non-empty object."
}
```

---

### Example Request Using Axios

To make a request to this endpoint using Axios, you can use the following code snippet:

```javascript
import axios from 'axios';

const createElection = async () => {
    const url = 'https://chainballot-backend.onrender.com/gateway/v1/election';
    const requestBody = {
        requestBody: {
            election_title: "The first presidential election",
            election_description: "This is the first ever presidential election that will be held on Chainballot",
            election_presiding_officer: "0x1234567890abcdef1234567890abcdef12345678",
            election_start_date: "2024-10-20T09:00:00.000Z",
            election_end_date: "2024-10-25T09:00:00.000Z"
        }
    };

    try {
        const response = await axios.post(url, requestBody, {
            headers: {
                'Content-Type': 'application/json',
                'X-Custom-Header': 'YOUR_CUSTOM_VALUE_HERE' // Replace with actual custom value
            }
        });
        console.log('Election created successfully:', response.data);
    } catch (error) {
        console.error('Error creating election:', error.response ? error.response.data : error.message);
    }
};

createElection();
```

