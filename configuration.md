# Configuration

Advanced configuration options for Cirrus Sync.

## Configuration Files

Cirrus Sync stores configuration in the following locations:

**Windows:**
```
%APPDATA%\CirrusSync\config.json
```

**macOS:**
```
~/Library/Application Support/CirrusSync/config.json
```

**Linux:**
```
~/.config/cirrussync/config.json
```

## General Settings

### Application Behavior

```json
{
  "general": {
    "autoStart": true,
    "minimizeToTray": true,
    "showNotifications": true,
    "checkUpdatesAutomatically": true,
    "updateChannel": "stable"
  }
}
```

**Options:**
- `autoStart` - Launch Cirrus Sync on system startup
- `minimizeToTray` - Minimize to system tray instead of taskbar
- `showNotifications` - Display desktop notifications for sync events
- `checkUpdatesAutomatically` - Check for application updates automatically
- `updateChannel` - Update channel: `stable`, `beta`, or `dev`

### User Interface

```json
{
  "ui": {
    "theme": "auto",
    "language": "en",
    "showAdvancedOptions": false,
    "compactMode": false
  }
}
```

**Theme Options:**
- `auto` - Follow system theme
- `light` - Light theme
- `dark` - Dark theme

**Language Options:**
- `en` - English
- `es` - Spanish
- `fr` - French
- `de` - German
- `ja` - Japanese
- `zh` - Chinese

## Sync Configuration

### Default Sync Settings

```json
{
  "sync": {
    "defaultSyncType": "bidirectional",
    "conflictResolution": "manual",
    "preserveTimestamps": true,
    "followSymlinks": false,
    "checksumValidation": true,
    "retryAttempts": 3,
    "retryDelay": 5000
  }
}
```

**Sync Types:**
- `bidirectional` - Two-way synchronization
- `upload` - Local to cloud only
- `download` - Cloud to local only

**Conflict Resolution:**
- `manual` - Prompt user for each conflict
- `newestWins` - Newest file overwrites older
- `largestWins` - Largest file overwrites smaller
- `localWins` - Local file always wins
- `remoteWins` - Remote file always wins

### Performance Tuning

```json
{
  "performance": {
    "maxConcurrentTransfers": 5,
    "chunkSize": 8388608,
    "connectionTimeout": 30000,
    "readTimeout": 60000,
    "maxRetries": 3,
    "useCompression": true
  }
}
```

**Parameters:**
- `maxConcurrentTransfers` - Maximum simultaneous file transfers
- `chunkSize` - Transfer chunk size in bytes (8MB default)
- `connectionTimeout` - Connection timeout in milliseconds
- `readTimeout` - Read timeout in milliseconds
- `maxRetries` - Maximum retry attempts for failed transfers
- `useCompression` - Enable data compression during transfer

## Network Configuration

### Bandwidth Controls

```json
{
  "network": {
    "uploadLimit": 0,
    "downloadLimit": 0,
    "throttleOnCellular": true,
    "pauseOnMeteredConnection": false,
    "useProxy": false,
    "proxySettings": {
      "type": "http",
      "host": "",
      "port": 8080,
      "username": "",
      "password": "",
      "authentication": false
    }
  }
}
```

**Bandwidth Limits:**
- `0` - Unlimited
- `1048576` - 1 MB/s
- `5242880` - 5 MB/s

**Proxy Types:**
- `http` - HTTP proxy
- `https` - HTTPS proxy
- `socks4` - SOCKS4 proxy
- `socks5` - SOCKS5 proxy

### SSL/TLS Configuration

```json
{
  "ssl": {
    "verifySSLCertificates": true,
    "allowSelfSignedCertificates": false,
    "customCertificatePath": "",
    "tlsVersion": "1.3",
    "cipherSuites": "default"
  }
}
```

## Security Settings

### Encryption Configuration

```json
{
  "security": {
    "enableClientSideEncryption": false,
    "encryptionAlgorithm": "AES-256-GCM",
    "keyDerivationIterations": 100000,
    "encryptFilenames": false,
    "localCacheEncryption": true
  }
}
```

**Encryption Algorithms:**
- `AES-256-GCM` - Advanced Encryption Standard (recommended)
- `ChaCha20-Poly1305` - ChaCha20 stream cipher
- `AES-256-CBC` - AES in CBC mode (legacy)

### Authentication Settings

```json
{
  "auth": {
    "sessionTimeout": 3600,
    "requireReauthentication": false,
    "twoFactorAuthentication": {
      "enabled": false,
      "method": "totp",
      "backupCodes": []
    }
  }
}
```

## Logging Configuration

### Log Levels and Output

```json
{
  "logging": {
    "level": "info",
    "enableFileLogging": true,
    "logRotation": true,
    "maxLogSize": 10485760,
    "maxLogFiles": 5,
    "logPath": "default",
    "components": {
      "sync": "info",
      "network": "warn",
      "auth": "info",
      "api": "debug"
    }
  }
}
```

**Log Levels:**
- `debug` - Detailed debugging information
- `info` - General information messages
- `warn` - Warning messages
- `error` - Error messages only
- `off` - Disable logging

### Advanced Logging

```json
{
  "advancedLogging": {
    "enableNetworkTracing": false,
    "enableSQLTracing": false,
    "enablePerformanceMetrics": false,
    "logFormat": "json",
    "includeStackTrace": true
  }
}
```

## Provider-Specific Settings

### Google Drive Configuration

```json
{
  "providers": {
    "googleDrive": {
      "useServiceAccount": false,
      "serviceAccountKeyPath": "",
      "apiQuotaManagement": true,
      "maxRequestsPerSecond": 10,
      "enableTeamDriveSupport": true
    }
  }
}
```

### Dropbox Configuration

```json
{
  "providers": {
    "dropbox": {
      "useBusinessAccount": false,
      "enableDeltaSync": true,
      "maxFileSize": 157286400,
      "enableSmartSync": true
    }
  }
}
```

### OneDrive Configuration

```json
{
  "providers": {
    "oneDrive": {
      "usePersonalAccount": true,
      "enableBusinessFeatures": false,
      "maxChunkSize": 62914560,
      "enableVersioning": true
    }
  }
}
```

## Backup and Recovery

### Configuration Backup

```json
{
  "backup": {
    "autoBackupConfig": true,
    "backupLocation": "cloud",
    "backupFrequency": "daily",
    "keepBackupHistory": 30,
    "encryptBackups": true
  }
}
```

### Database Settings

```json
{
  "database": {
    "type": "sqlite",
    "connectionPoolSize": 10,
    "queryTimeout": 30000,
    "enableWALMode": true,
    "autoVacuum": "incremental"
  }
}
```

## Environment Variables

Cirrus Sync also supports configuration via environment variables:

```bash
# API Configuration
CIRRUS_API_KEY=your_api_key
CIRRUS_API_ENDPOINT=https://api.cirrus-sync.com

# Network Settings
CIRRUS_PROXY_URL=http://proxy.company.com:8080
CIRRUS_UPLOAD_LIMIT=5242880
CIRRUS_DOWNLOAD_LIMIT=10485760

# Security Settings
CIRRUS_ENCRYPTION_KEY=your_encryption_key
CIRRUS_SSL_VERIFY=true

# Logging
CIRRUS_LOG_LEVEL=info
CIRRUS_LOG_PATH=/var/log/cirrus
```

## Command Line Arguments

Override configuration options via command line:

```bash
cirrus-sync --config-file /path/to/config.json \
            --log-level debug \
            --no-auto-start \
            --proxy http://proxy:8080
```

**Available Arguments:**
- `--config-file` - Path to configuration file
- `--log-level` - Override log level
- `--no-auto-start` - Disable auto-start
- `--headless` - Run without GUI
- `--proxy` - Set proxy URL
- `--upload-limit` - Set upload bandwidth limit
- `--download-limit` - Set download bandwidth limit
