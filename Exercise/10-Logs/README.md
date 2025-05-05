# 10-Logs

## Question

A pod called dev-pod-dind-878516 has been deployed in the default namespace.
Inspect the logs for the container called log-x and redirect the warnings to /opt/dind-878516_logs.txt on the controlplane node

## Answer

```bash
k logs dev-pod-dind-878516 -c log-x | grep WARNING > /opt/dind-878516_logs.txt
```
