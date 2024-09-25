### Documentation for the `/api/v3/reverse` Endpoint

The `/api/v3/reverse` endpoint is designed to facilitate reverse lookups of user information based on Roblox or Discord identifiers. This endpoint aims to bridge the information gap between Roblox and Discord communities by leveraging both direct and API-mediated data retrieval methods.

#### URL Structure
```
GET /api/v3/reverse
```

#### Query Parameters
- **query** (required): The ID of the user (either Roblox ID or Discord ID) you wish to lookup.
- **type** (required): Specifies the type of ID provided in the query. Can be either `roblox` for Roblox IDs or `discord` for Discord IDs.
- **method** (required): Determines the source of the data. Can be either `scripts` for local data files or `breaches` for accessing broader external data sources.

#### Functionality
This endpoint operates by accessing locally stored data or by querying external APIs to fetch corresponding user information. Depending on the `method` specified, it will either search in local JSON files or make HTTP requests to external APIs such as RoPro or Bloxlink to gather data.

#### Response Structure
The response will be a JSON object containing the following fields:
- **success**: Boolean indicator of the request's success.
- **message**: Descriptive message about the result.
- **source**: The source from where the data was retrieved, which could be local files or external APIs.
- **roblox**: An object containing Roblox-specific information (id and possibly a username).
- **discord**: An object containing Discord-specific information (id and possibly a username).
- **additional_info** (optional): Additional information fetched from APIs, such as user reputation, tier status, and account creation date.
- **results**: An array of objects detailing the retrieved user information.

#### Error Handling
In case of errors (e.g., missing parameters, failed external API calls), the API will respond with an appropriate HTTP status code and a JSON object describing the error.

#### Example Request
```http
GET /api/v3/reverse?query=123456789&type=roblox&method=scripts
```

#### Example Response
```json
{
  "success": true,
  "message": "Successfully retrieved information about the user",
  "source": "Shhh Orders (scripts)",
  "roblox": {
    "id": "123456789",
    "name": "RobloxUser123"
  },
  "discord": {
    "id": "987654321",
    "name": "DiscordUser123"
  },
  "results": [
    {
      "roblox_id": "123456789",
      "discord_id": "987654321",
      "additional_info": {
        "reputation": "High",
        "tier": "Gold",
        "user_since": "2018"
      }
    }
  ]
}
```

#### Security
- All requests must include a valid API key in the `Authorization` header to be processed. This ensures that only authorized users can access the endpoint.
