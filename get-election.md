# ChainBallot API - Get Elections Endpoint Documentation

This documentation provides frontend developers with the necessary information to interact with the `GET /election` endpoint of the ChainBallot API.

## Base URL

The base URL for the API is:

```
https://chainballot-backend.onrender.com/gateway/v1/
```

## Endpoint

### GET `/election`

This endpoint is used to retrieve elections based on certain query parameters, or to list all elections if no parameters are provided.

---

### Request

- **Method**: `GET`
- **URL**: `/election`
- **Full URL**: `https://chainballot-backend.onrender.com/gateway/v1/election`
- **Headers**:
    - `Content-Type`: `application/json`
    - `X-Custom-Header`: `YOUR_CUSTOM_VALUE_HERE`

### Query Parameters (Optional)

The request can include a `requestBody` parameter in the query, which filters the elections based on the criteria provided. If no query parameters are provided, the API will return a list of up to 8 elections.

---

### Example Requests

#### 1. Get Elections Filtered by `election_presiding_officer`

This request will retrieve elections that have the specified presiding officer.

```json
{
    "requestBody": {
        "election_presiding_officer": "0x1234567890abcdef1234567890abcdef12345678"
    }
}
```

#### 2. Get Elections Filtered by `election_address`

```json
{
    "requestBody": {
        "election_address": "0xabcdefabcdefabcdefabcdefabcdefabcdef"
    }
}
```

#### 3. Get Elections by ID

```json
{
    "requestBody": {
        "id": "64c12345abc678def9012345"
    }
}
```

#### 4. Get All Elections (No Filtering)

You can either pass an empty `requestBody` or omit the `requestBody` completely. The server will return the first 8 elections in the database.

```json
{
    "requestBody": {}
}
```

Or no query parameter:

```
GET /election
```

---

### Example Request Using Axios

#### 1. Request with Query Parameters

Here is an example of how to make a request using Axios to get elections filtered by `election_presiding_officer`:

```javascript
import axios from 'axios';

const getElections = async () => {
    const url = 'https://chainballot-backend.onrender.com/gateway/v1/election';
    const params = {
        requestBody: {
            election_presiding_officer: "0x1234567890abcdef1234567890abcdef12345678"
        }
    };

    try {
        const response = await axios.get(url, {
            headers: {
                'Content-Type': 'application/json',
                'X-Custom-Header': 'YOUR_CUSTOM_VALUE_HERE'
            },
            params: params
        });
        console.log('Elections:', response.data);
    } catch (error) {
        console.error('Error fetching elections:', error.response ? error.response.data : error.message);
    }
};

getElections();
```

#### 2. Request Without Query Parameters (All Elections)

To retrieve all elections, you can omit the `params` object from the Axios request:

```javascript
import axios from 'axios';

const getAllElections = async () => {
    const url = 'https://chainballot-backend.onrender.com/gateway/v1/election';

    try {
        const response = await axios.get(url, {
            headers: {
                'Content-Type': 'application/json',
                'X-Custom-Header': 'YOUR_CUSTOM_VALUE_HERE'
            }
        });
        console.log('All Elections:', response.data);
    } catch (error) {
        console.error('Error fetching elections:', error.response ? error.response.data : error.message);
    }
};

getAllElections();
```

---

### Response

The API will return a JSON object containing a list of elections, filtered according to the query parameters or all available elections if no parameters were provided.

#### Example Successful Response

```json
{
    "success": true,
    "elections": [
        {
            "_id": "64c12345abc678def9012345",
            "election_title": "The first presidential election",
            "election_description": "This is the first ever presidential election that will be held on Chainballot",
            "election_presiding_officer": "0x1234567890abcdef1234567890abcdef12345678",
            "election_start_date": "2024-10-20T09:00:00.000Z",
            "election_end_date": "2024-10-25T09:00:00.000Z",
            "createdAt": "2024-10-15T10:30:00.000Z",
            "__v": 0
        }
        // Other election objects...
    ]
}
```

#### Example Error Response

```json
{
    "success": false,
    "message": "requestBody must be a non-empty object."
}
```
