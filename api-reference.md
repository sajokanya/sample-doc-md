# API Reference

Cirrus Sync provides a comprehensive REST API for developers to integrate cloud synchronization capabilities into their applications.

## Authentication

### API Keys

All API requests require authentication using API keys:

```http
GET /api/v1/sync/status
Authorization: Bearer YOUR_API_KEY
```

### Obtaining API Keys

1. Log in to your Cirrus Sync account
2. Navigate to Settings > Developer
3. Click "Generate New API Key"
4. Copy and securely store your key

### Rate Limiting

API requests are limited to:
- 1000 requests per hour for free accounts
- 10000 requests per hour for premium accounts
- 100000 requests per hour for enterprise accounts

## Base URL

```
https://api.cirrus-sync.com/v1
```

## Endpoints

### Sync Management

#### List All Syncs

```http
GET /api/v1/syncs
```

**Response:**
```json
{
  "syncs": [
    {
      "id": "sync_123456",
      "name": "Documents Sync",
      "local_path": "/Users/john/Documents",
      "remote_path": "/Documents",
      "provider": "google_drive",
      "status": "active",
      "created_at": "2025-01-15T10:30:00Z",
      "last_sync": "2025-01-15T14:22:33Z"
    }
  ],
  "total": 1
}
```

#### Create New Sync

```http
POST /api/v1/syncs
```

**Request Body:**
```json
{
  "name": "My Documents",
  "local_path": "/Users/john/Documents",
  "remote_path": "/Documents",
  "provider": "google_drive",
  "sync_type": "bidirectional",
  "filters": {
    "include": ["*.pdf", "*.docx"],
    "exclude": ["*.tmp"]
  }
}
```

**Response:**
```json
{
  "id": "sync_789012",
  "status": "created",
  "message": "Sync created successfully"
}
```

#### Get Sync Details

```http
GET /api/v1/syncs/{sync_id}
```

**Response:**
```json
{
  "id": "sync_123456",
  "name": "Documents Sync",
  "local_path": "/Users/john/Documents",
  "remote_path": "/Documents",
  "provider": "google_drive",
  "status": "active",
  "sync_type": "bidirectional",
  "files_synced": 1247,
  "total_size": "2.4 GB",
  "last_sync": "2025-01-15T14:22:33Z",
  "next_sync": "2025-01-15T15:22:33Z"
}
```

#### Update Sync Configuration

```http
PUT /api/v1/syncs/{sync_id}
```

**Request Body:**
```json
{
  "name": "Updated Documents Sync",
  "sync_type": "upload_only",
  "filters": {
    "include": ["*.pdf", "*.docx", "*.xlsx"],
    "exclude": ["*.tmp", "*.log"]
  }
}
```

#### Delete Sync

```http
DELETE /api/v1/syncs/{sync_id}
```

**Response:**
```json
{
  "status": "deleted",
  "message": "Sync deleted successfully"
}
```

#### Start Manual Sync

```http
POST /api/v1/syncs/{sync_id}/start
```

#### Pause Sync

```http
POST /api/v1/syncs/{sync_id}/pause
```

#### Resume Sync

```http
POST /api/v1/syncs/{sync_id}/resume
```

### File Operations

#### List Files in Sync

```http
GET /api/v1/syncs/{sync_id}/files
```

**Query Parameters:**
- `path` (optional) - Filter by path
- `limit` (optional) - Number of results (default: 100)
- `offset` (optional) - Pagination offset

**Response:**
```json
{
  "files": [
    {
      "id": "file_345678",
      "name": "document.pdf",
      "path": "/Documents/document.pdf",
      "size": 1048576,
      "modified_at": "2025-01-15T12:30:00Z",
      "sync_status": "synced",
      "checksum": "sha256:abc123..."
    }
  ],
  "total": 247
}
```

#### Get File Details

```http
GET /api/v1/files/{file_id}
```

#### Force File Sync

```http
POST /api/v1/files/{file_id}/sync
```

### Provider Management

#### List Connected Providers

```http
GET /api/v1/providers
```

**Response:**
```json
{
  "providers": [
    {
      "id": "provider_456789",
      "type": "google_drive",
      "email": "user@gmail.com",
      "connected_at": "2025-01-10T09:15:00Z",
      "status": "active",
      "storage_used": "15.2 GB",
      "storage_total": "100 GB"
    }
  ]
}
```

#### Connect New Provider

```http
POST /api/v1/providers
```

**Request Body:**
```json
{
  "type": "dropbox",
  "auth_code": "authorization_code_from_oauth"
}
```

#### Disconnect Provider

```http
DELETE /api/v1/providers/{provider_id}
```

### Webhooks

#### List Webhooks

```http
GET /api/v1/webhooks
```

#### Create Webhook

```http
POST /api/v1/webhooks
```

**Request Body:**
```json
{
  "url": "https://yourapp.com/webhook",
  "events": ["sync.completed", "sync.failed", "file.changed"],
  "sync_id": "sync_123456"
}
```

#### Webhook Events

Cirrus Sync sends webhooks for the following events:

- `sync.started` - Sync operation started
- `sync.completed` - Sync operation completed successfully
- `sync.failed` - Sync operation failed
- `file.added` - New file added to sync
- `file.changed` - Existing file modified
- `file.deleted` - File removed from sync
- `provider.connected` - New cloud provider connected
- `provider.disconnected` - Cloud provider disconnected

**Webhook Payload Example:**
```json
{
  "event": "sync.completed",
  "sync_id": "sync_123456",
  "timestamp": "2025-01-15T14:22:33Z",
  "data": {
    "files_processed": 15,
    "files_added": 3,
    "files_updated": 7,
    "files_deleted": 1,
    "duration": 45.2
  }
}
```

## Error Codes

| Code | Description |
|------|-------------|
| 400 | Bad Request - Invalid parameters |
| 401 | Unauthorized - Invalid or missing API key |
| 403 | Forbidden - Insufficient permissions |
| 404 | Not Found - Resource does not exist |
| 409 | Conflict - Resource already exists |
| 429 | Too Many Requests - Rate limit exceeded |
| 500 | Internal Server Error - Server error |

## SDKs and Libraries

### JavaScript/Node.js

```bash
npm install cirrus-sync-sdk
```

```javascript
const CirrusSync = require('cirrus-sync-sdk');

const client = new CirrusSync({
  apiKey: 'your-api-key'
});

// List all syncs
const syncs = await client.syncs.list();

// Create new sync
const newSync = await client.syncs.create({
  name: 'My Sync',
  localPath: '/path/to/local',
  remotePath: '/path/to/remote',
  provider: 'google_drive'
});
```

### Python

```bash
pip install cirrus-sync
```

```python
from cirrus_sync import CirrusSyncClient

client = CirrusSyncClient(api_key='your-api-key')

# List all syncs
syncs = client.syncs.list()

# Create new sync
new_sync = client.syncs.create(
    name='My Sync',
    local_path='/path/to/local',
    remote_path='/path/to/remote',
    provider='google_drive'
)
```

### Go

```bash
go get github.com/cirrus-sync/go-sdk
```

```go
package main

import (
    "github.com/cirrus-sync/go-sdk"
)

func main() {
    client := cirrussync.NewClient("your-api-key")
    
    // List all syncs
    syncs, err := client.Syncs.List()
    if err != nil {
        panic(err)
    }
}
```
