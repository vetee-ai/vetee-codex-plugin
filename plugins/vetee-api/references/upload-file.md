# Upload a file

Based on the Vetee “Upload a file” documentation.

Upload raw file bytes first. The returned `fileId` identifies the file for a
later GraphQL relationship or [file view URL](open-file.md). Image resizing is
requested when viewing a file, not during upload.

## HTTP request

```http
POST {API_BASE}/action/file/upload
Authorization: Bearer <access_token>
Content-Type: multipart/form-data; boundary=<generated_boundary>
```

Use the selected environment's API base URL from [GraphQL basics](graphql-basics.md).
This is a REST action outside `/graphql`.

## Multipart fields

| Field | Value |
| --- | --- |
| `type` | `image`, `audio`, `video` or `document` |
| `fileCategoryId` | ID of the relevant `FileCategory` from the selected environment |
| `file` | The raw file bytes with their filename |

Use a multipart-capable HTTP client or `FormData` and let it generate the
boundary and matching `Content-Type`. A GraphQL document or JSON body is not a
substitute for the multipart upload. Look up the category in the selected
environment rather than copying an ID from another environment.

## Response and next step

A successful response supplies `fileId` and `url`:

```json
{
  "fileId": "<returned-file-id>",
  "url": "https://storage.example.com/<returned-file-path>"
}
```

The values are placeholders. Use the actual returned URL; do not construct a
storage URL by guessing its hostname or path. If the task also requires attaching
the file to a record, use the returned `fileId` in that record's GraphQL relation
input, following the live schema. Uploading bytes and attaching a file to a
record are separate operations.

The plugin's current `admin_query` and `admin_mutation` tools accept GraphQL
only; they do not transport multipart file bytes. This reference documents the
HTTP operation for an authenticated upload-capable client. Upload and relation
changes remain subject to the skill's explicit-user-request requirement.
