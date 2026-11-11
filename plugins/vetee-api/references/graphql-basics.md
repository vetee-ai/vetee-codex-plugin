# GraphQL basics

Based on the Vetee “GraphQL” documentation. Use the live schema of the selected
environment to confirm exact operations, fields, inputs and role availability.
For MCP tool selection, environment defaults and permissions, see
[GraphQL workflow](graphql.md).

## Endpoint and authentication

The API accepts GraphQL documents at `/graphql` on the selected API host:

| Environment | API base URL | GraphQL endpoint |
| --- | --- | --- |
| master | `https://api.vetee.pet` | `https://api.vetee.pet/graphql` |
| beta | `https://api.beta.vetee.pet` | `https://api.beta.vetee.pet/graphql` |
| stage | `https://api.stage.vetee.pet` | `https://api.stage.vetee.pet/graphql` |

Authenticated requests use `Authorization: Bearer <access_token>`. When using
this plugin, the Codex MCP connection supplies authentication; pass GraphQL to
`admin_query` or, only for an explicitly requested change, `admin_mutation`.
Some operations are public; check the operation's contract rather than assuming.
The GraphQL endpoint also provides a schema viewer.

## Queries

| Operation pattern | Purpose | Common arguments |
| --- | --- | --- |
| `getList{ModelName}` | Read a filtered page of records | `filter`, `order`, `pagination` |
| `getOne{ModelName}` | Read one record using a unique filter | `filter` |

List wrappers commonly expose:

```graphql
status { success errorCode errorMessage }
meta { limit offset total }
nodes { id }
```

Detail wrappers commonly expose:

```graphql
status { success errorCode errorMessage }
node { id }
```

These are selection-set excerpts, not complete requests. Add them to a confirmed
operation. Nested relations may accept their own filters, order and pagination.
Custom queries can return a scalar or direct object instead of a wrapper.

## Mutations

| Operation pattern | Purpose | Common arguments |
| --- | --- | --- |
| `createOne{ModelName}` | Create a record | `data` |
| `updateOne{ModelName}` | Update a record | `filter`, `data` |
| `deleteOne{ModelName}` | Delete a record | `filter` |

Availability depends on the authenticated role. Custom business mutations do not
necessarily use these names or inputs. Inspect the schema before constructing
the request. Describing an operation here does not grant permission to run it;
the skill's read-only default still applies.

## Errors and results

Check GraphQL's top-level `errors` separately from application-level
`status {success errorCode errorMessage}`. A response can have HTTP 200 and still
contain either kind of failure. Treat `success: false` as failure, and do not
assume that nullable data exists when a status indicates an error.

Use actual IDs and values from the selected environment. Documentation examples
are illustrative; they are not records to query or update.

## Related operations

- [Application settings](app-settings.md): the `getSettings` query.
- [Upload a file](upload-file.md): multipart upload and use of `fileId` in GraphQL.
- [Open a file](open-file.md): file retrieval and image view parameters.
