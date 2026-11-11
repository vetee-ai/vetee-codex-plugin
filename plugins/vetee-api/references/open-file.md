# Open a file

Based on the Vetee “View a file” documentation.

Read a file using its ID on the selected environment's API base URL:

```http
GET {API_BASE}/action/file/view/{fileId}
```

See [GraphQL basics](graphql-basics.md) for the API base URLs. This is a REST
file endpoint outside `/graphql`. Obtain `fileId` from the selected environment's
records or an [upload response](upload-file.md).

## Image query parameters

| Parameter | Meaning |
| --- | --- |
| `width` | Requested image width |
| `height` | Requested image height |
| `fit=cover` | Produce the requested dimensions, cropping as needed |
| `fit=outside` | Resize to fit outside the requested dimensions |
| `position=center` | Center the crop; the documented default position |

For example, an image view URL has this shape:

```text
{API_BASE}/action/file/view/{fileId}?width=640&height=480&fit=cover&position=center
```

These options apply to image files. Other file types use the normal view
endpoint without assuming that image transformations apply.

Check the selected environment's view-URL authentication configuration. The
source documentation does not guarantee that every file is anonymously readable.
Use an authenticated client when required; do not put bearer tokens into URLs.
The current MCP GraphQL tools can look up file metadata and IDs, while the HTTP
view endpoint serves the file itself.
