# Overview of SPIRE - Kubehuddle 2023

- [Slides](./Kubehuddle_Overview%20of%20SPIRE.pdf)

## Demo

1. Start SPIRE server:

```shell
./spire-server  run -config local-server.conf
```

2. Generate a join token for the agent:


```shell
./spire-server token generate -spiffeID spiffe://example.org/local-agent
```

3. Launch the agent with the join token:


```shell
./spire-agent run -config local-agent.conf -joinToken <INSERT_JOIN_TOKEN>
```

4. List the registered agent:

```shell
./spire-server agent list
```

5. Register a workload:


```
 ./spire-server entry create \
     -spiffeID spiffe://example.org/wl/my-workload \
     -parentID spiffe://example.org/spire/agent/join_token/<INSERT_JOIN_TOKEN> \
     -selector unix:user:<USERNAME> \
     -selector unix:uid:<UID>
```

You can use the [SPIFFE helper](https://github.com/spiffe/spiffe-helper) to retrieve an SVID.

1. Clone the repo.
2. Update the `certDir` in `helper.conf` to point to the folder for the workloads SVID:

3. Run the helper:

```shell
go run cmd/spiffe-helper/main.go
```

The SVID will be dropped in the specified folder. You can use `openssl` to check that SPIFFE ID in the cert:

```shell
openssl x509 -in certs/svid.pem -text
```