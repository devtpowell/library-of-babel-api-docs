# Authentication

The Library of Babel API requires authentication for all endpoints except basic browsing. Authentication ensures that only authorized clients can access advanced features such as search, page retrieval, and metadata queries.

This guide covers how to authenticate using an API key, how to include it in your requests, and what to expect if something goes wrong.

---

## API Key Authentication

All requests to authenticated endpoints must include an API key provided in the request header.

### Header Format

Include the following header in each request:

X-API-Key: your-api-key-here

### Example Request

```http
GET /search?q=mirror+labyrinth HTTP/1.1
Host: api.babel-library.org
X-API-Key: abc123xyz789```

Or with curl:

```curl -H "X-API-Key: abc123xyz789" "https://api.babel-library.org/search?q=mirror+labyrinth"```

## Obtaining an API Key

To register for an API key:

1. Visit https://babel-api.dev/register
2. Log in using your GitHub or email.
3. You’ll receive a development API key via email.

Development keys include:

- 1,000 requests per day
- Read-only access to all public endpoints

To request elevated access or commercial licensing, contact `support@babel-api.dev`.

## Error Handling

| Status Code | Error             | Description                                 |
| ----------- | ----------------- | ------------------------------------------- |
| 401         | Unauthorized      | Missing or invalid API key                  |
| 403         | Forbidden         | API key does not have access to this action |
| 429         | Too Many Requests | Rate limit exceeded                         |

If you receive a 429 Too Many Requests error, check the Retry-After response header to determine when you can resume.

## Rate Limits

All keys are subject to rate limiting.

| Tier        | Limit                     |
| ----------- | ------------------------- |
| Development | 60 requests per minute    |
| Pro         | 1,000 requests per minute |

If you exceed the limit, further requests may be temporarily rejected.

## Security Best Practices

- Keep your API key secret. Never commit it to a public repo.
- Store it securely in environment variables or a secure secrets manager.
- Only use your API key over HTTPS.
- Rotate your key if it may have been exposed.

## Example Error Response

```json
{
  "error": "Unauthorized",
  "message": "Missing or invalid API key.",
  "status": 401
}
```

Still need help? Contact support@babel-api.dev.
