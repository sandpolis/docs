# Server/Agent Messages

## Agent Authentication
### RQ_NoAuth

```java
// Attempt to authenticate as an agent without providing anything.
//
// Source:       Agent
// Destination:  Server
// Response:     Outcome
```

### RQ_PasswordAuth

```java
// Attempt to authenticate as an agent using a simple password.
//
// Source:       Agent
// Destination:  Server
// Response:     Outcome
```

#### Message Format
| Field            | Type       | Requirements              | Description                                              |
|------------------|------------|---------------------------|----------------------------------------------------------|
| password         | string     | 8 - 64 characters         | The password text                                        |

### RQ_CertAuth

```java
// Attempt to authenticate as an agent using a "client" certificate.
//
// Source:       Agent
// Destination:  Server
// Response:     Outcome
```

## General
### RQ_AgentMetadata

```java
// Request agent metadata.
//
// Source:       Server
// Destination:  Agent
// Response:     RS_AgentMetadata
```

### RS_AgentMetadata

```java
// Response with agent metadata.
//
// Source:       Agent
// Destination:  Server
// Request:      RQ_AgentMetadata
```

#### Message Format
| Field            | Type       | Requirements              | Description                                              |
|------------------|------------|---------------------------|----------------------------------------------------------|
| hostname         | string     | 0 - 64 characters         | The agent's network hostname                             |
| os               | OsType     |                           | The agent's OS family                                    |
| arch             | string     |                           | The agent's CPU architecture                             |
