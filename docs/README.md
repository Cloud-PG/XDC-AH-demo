# XDC HA Meeting: XCache Demo

## Deploy K8s on any cloud with DODAS-TS

Although is not the only way, I put here the references and contacts for whoever is interested in deploy K8s on any cloud provider with a unique configuration file. The procedure uses PaaS orchestration from DODAS thematic service (EOSC-Hub)

- User Guide
- K8s template

## XCache local deployment for cloud resources

### What is going to be deployed?

### Deploy K8d XCache service

### Deploy XCache redirector

### Deploy XCache servers

### Deploy a clien node

### Testing functionalities

For time reason of the demo a pre-installed origin server will be used as remote data source. On that server has been put a file called `test.txt`

We are going to do the following:

- look briefly at redirector logs, to see XCache servers registering themselves
- from the client node request a copy of the `test.txt` to the XCache redirector
  - `xrdcp -f -d2 root://xcache-service.default.svc.cluster.local//test.txt .`
  - in few words at this point the redirector is going to check in any cache server has it on disk
    - if any, will make client contact that server directly
    - otherwise it will choose via round robin a cache server that will work as a proxy for the current client request, but caching data meanwhile
- check that the file is actually stored on the cache server that was contacted
- retry to make the same request from the client node and check that indeed it come from the same server that has the file on disk now
  - the transfer speed should look a bit better indeed
- scale up and down the cluster dynamically

- put another file on the origin and see where it land when requested