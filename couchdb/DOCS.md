# Configuration

Add-on configuration:

```yaml
port: 5984
username: "admin"
password: "your_secure_password_here"
```

### Option: `port` (required)

The port number CouchDB will listen on.

- Type: `int`
- Default: `5984`
- Range: `1-65535`

### Option: `username` (required)

The admin username for CouchDB.

- Type: `string`

### Option: `password` (required)

The admin password for CouchDB. **This must be set for security!**

- Type: `password`

**Note**: Make sure to use a strong, unique password for production use.

## Network

The add-on exposes CouchDB on port 5984 by default. You can change this in the configuration if needed.

## Storage

The add-on automatically creates persistent storage for CouchDB data in your Home Assistant configuration directory under `/config/couchdb/`. This includes:

- `/config/couchdb/data/` - Database files
- `/config/couchdb/config/` - Configuration files
- `/config/couchdb/log/` - Log files

## API Access

Once running, you can access the CouchDB API at:

- HTTP API: `http://YOUR_HA_IP:5984/`
- Web Interface (Fauxton): `http://YOUR_HA_IP:5984/_utils/`

Use the configured username and password to authenticate.