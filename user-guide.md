# User Guide

Complete guide to using Cirrus Sync effectively.

## Dashboard Overview

The Cirrus Sync dashboard provides a centralized view of all your sync operations:

- **Active Syncs** - Currently running synchronization tasks
- **Recent Activity** - Latest file changes and sync events
- **Storage Usage** - Cloud storage consumption across providers
- **Sync Status** - Health and performance metrics

## Managing Sync Folders

### Adding a New Sync

1. Click the "+" button in the main toolbar
2. Select "New Sync Folder"
3. Choose your local directory
4. Select cloud provider and remote path
5. Configure sync preferences
6. Click "Create Sync"

### Sync Types

**Real-time Sync**
- Instantly syncs changes as they occur
- Best for active working directories
- Higher battery usage on mobile devices

**Scheduled Sync**
- Syncs at specified intervals
- Efficient for large file collections
- Customizable timing options

**Manual Sync**
- Sync only when manually triggered
- Complete control over sync timing
- Ideal for sensitive data

### Sync Filters

Configure which files to include or exclude:

**File Type Filters**
```
Include: *.docx, *.pdf, *.jpg
Exclude: *.tmp, *.cache, *.log
```

**Size Filters**
- Minimum file size: 1 KB
- Maximum file size: 100 MB
- Skip empty files option

**Date Filters**
- Modified after: specific date
- Created before: specific date
- Age-based rules

## File Management

### File Versioning

Cirrus Sync maintains version history for all synced files:

- **Auto-versioning** - Keeps last 10 versions automatically
- **Manual snapshots** - Create named versions manually
- **Version comparison** - View differences between versions
- **Restore options** - Rollback to any previous version

### Conflict Resolution

When file conflicts occur, Cirrus Sync offers several resolution strategies:

**Automatic Resolution**
- Newest file wins
- Largest file wins
- Source priority (local vs. cloud)

**Manual Resolution**
- Review conflicts in dedicated interface
- Compare file contents side-by-side
- Choose resolution for each conflict
- Apply rules for future conflicts

### Offline Access

Configure offline availability for important files:

1. Right-click any file or folder
2. Select "Make Available Offline"
3. Choose sync priority (High/Normal/Low)
4. Files download automatically when connected

## Security Features

### Encryption

**In-Transit Encryption**
- TLS 1.3 for all data transfers
- End-to-end encryption support
- Certificate pinning for enhanced security

**At-Rest Encryption**
- AES-256 encryption for local cache
- Optional client-side encryption
- Key management integration

### Access Controls

**Two-Factor Authentication**
- TOTP support (Google Authenticator, Authy)
- SMS backup options
- Recovery codes generation

**Device Management**
- View all connected devices
- Remote device deauthorization
- Device-specific access controls

## Sharing and Collaboration

### Share Links

Create secure links to share files with others:

1. Right-click any synced file
2. Select "Create Share Link"
3. Configure permissions:
   - View only
   - Download allowed
   - Comment access
   - Edit permissions
4. Set expiration date
5. Copy and share the link

### Team Folders

Collaborate with team members using shared folders:

- **Team creation** - Invite members by email
- **Role management** - Admin, Editor, Viewer roles
- **Activity tracking** - See who changed what and when
- **Notification settings** - Email alerts for changes

## Performance Optimization

### Bandwidth Management

Control how Cirrus Sync uses your internet connection:

**Upload Limits**
- Maximum upload speed: 1 Mbps
- Upload schedule: Business hours only
- Pause uploads when on cellular

**Download Limits**
- Maximum download speed: 5 Mbps
- Priority downloads for recently accessed files
- Background download throttling

### Storage Optimization

**Smart Sync**
- Keep frequently accessed files local
- Move old files to cloud-only storage
- Automatic cleanup of temporary files

**Cache Management**
- Local cache size limit: 10 GB
- Cache cleanup policies
- Manual cache clearing options

## Mobile Apps

Cirrus Sync offers native mobile applications:

### iOS App Features
- Full file access and editing
- Camera upload automation
- Touch ID/Face ID authentication
- Offline file access

### Android App Features
- Intent integration with other apps
- Fingerprint authentication
- Background sync optimization
- SD card support

## Browser Extension

The Cirrus Sync browser extension provides:

- One-click file saving to cloud
- Screenshot capture and sync
- Web page archiving
- Password-protected downloads

## Keyboard Shortcuts

**Windows/Linux**
- `Ctrl + N` - New sync folder
- `Ctrl + R` - Refresh all syncs
- `Ctrl + P` - Pause all syncs
- `Ctrl + ,` - Open preferences

**macOS**
- `Cmd + N` - New sync folder
- `Cmd + R` - Refresh all syncs
- `Cmd + P` - Pause all syncs
- `Cmd + ,` - Open preferences
