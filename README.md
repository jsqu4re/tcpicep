# tcpicep

## About

```mermaid
pie title Do we need serialization?
         "YES" : 6
         "NO" : 5
         "Maybe" : 45
```

## Idea

TCP-IP Communication for Iceoryx using a peer to peer architecture. Ignoring serialization in the first place and assuming a trusted network.

### Trusted Network

A trusted network in a un-trusted environment could be created using port forwarding via ssh.

### Serialization

Data serialization can be ignored as long as the ABI regarding memory layout is identical. This could be checked per service for every service could have had been compiled with different ABI flags. To ensure compatibility a identical docker container could be used to build the different applications.

## Structure

## Network Service Discovery

```mermaid
sequenceDiagram
    participant lshm as Local SHM
    participant lp as Local PC - Client
    participant rp as Remote PC - Server
    participant rshm as Remote SHM

    loop callback from roudi
        lshm->>lp: update available services
    end

    loop callback from roudi
        rshm->>rp: update available services
    end

    lp->>rp: Connect
    rp->>lp: Established

    lp->>rp: Send 'servers list'
    rp->>lp: Send 'servers list'

    lp->>rp: available services
    rp->>rshm: add remote services

    rp->>lp: available services
    lp->>lshm: add remote services
```

## Data Structure

### Servers List

Servers list with information about each server:

- Address
- Connectivity Status
- maybe known services
