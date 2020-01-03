# SoftEther VPN on Docker on Raspberry Pi

## How to use

```
docker build -t softether .
docker run --net=host --privileged softether
```

When using port 443, stop the port from manager tool or vpncmd
