# Client/Server Messages

## Server
### RQ_ServerBanner

```java
// Request the server's banner.
//
// Source:       Client
// Destination:  Server
// Request:      RS_ServerBanner
```

### RS_ServerBanner

```java
// Response with the server's banner.
//
// Source:       Server
// Destination:  Client
// Request:      RQ_ServerBanner
```

#### Message Format
| Field            | Type       | Requirements              | Description                                              |
|------------------|------------|---------------------------|----------------------------------------------------------|
| maintenance      | bool       |                           | Indicates that only superusers will be allowed to login  |
| version          | string     | 5 - 32 characters         | The server's version string                              |
| message          | string     | 0 - 128 characters        | The banner text message                                  |
| image            | bytes      | 0 - 1 MiB PNG format      | The banner image                                         |
