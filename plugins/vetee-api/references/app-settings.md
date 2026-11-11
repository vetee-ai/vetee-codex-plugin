# Application settings

Based on the Vetee “Application settings” documentation.

Use the `getSettings` GraphQL query to read the application's contact and support
email addresses. Run it through the selected environment's `admin_query` tool.
See [GraphQL basics](graphql-basics.md) for endpoint and response conventions.

## Request

Pass this document as the MCP tool's `document` argument:

```graphql
query GetSettings {
  getSettings {
    status { success errorCode errorMessage }
    contactEmail
    supportEmail
  }
}
```

No variables are needed. Confirm the operation in the selected live schema if
it is unavailable or its response shape has changed.

## Response

Read `data.getSettings.status` first, then `contactEmail` and `supportEmail`.
For example, a successful response has this shape; the addresses below are
placeholders, not configured values:

```json
{
  "data": {
    "getSettings": {
      "status": {
        "success": true,
        "errorCode": null,
        "errorMessage": null
      },
      "contactEmail": "contact@example.com",
      "supportEmail": "support@example.com"
    }
  }
}
```

Also check top-level GraphQL `errors`. Return the values actually supplied by
the API; do not substitute the example addresses.
