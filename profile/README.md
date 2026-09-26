<p align="center">
  <img src="https://raw.githubusercontent.com/fleetpermit/fleetpermit/main/docs/assets/logo.svg" alt="FleetPermit" width="320">
</p>

<h3 align="center">Least privilege for agents, across every cluster.</h3>
<p align="center">Define who can call which tool, on which clusters, and for how long.</p>

---

**FleetPermit** is portable, time-bound authorization for AI agents across Kubernetes fleets.

A platform team writes one `FleetAccessPolicy`: which workload identities (SPIFFE IDs) may call which
MCP tools, on which clusters, for at most how long. Access is activated with a short-lived
`ToolAccessLease`, delivered only to the clusters an Open Cluster Management placement selects, and
enforced by each cluster's Kubernetes agentic-networking gateway. The expiry is part of the rule the
gateway evaluates, so a lease stops working on time even when the fleet hub is unreachable.

FleetPermit builds on neutral upstream open-source projects and replaces none of them:
[Open Cluster Management](https://open-cluster-management.io/),
[Kubernetes SIG Network's kube-agentic-networking](https://github.com/kubernetes-sigs/kube-agentic-networking),
[Gateway API](https://gateway-api.sigs.k8s.io/), [Envoy](https://www.envoyproxy.io/),
[SPIFFE](https://spiffe.io/) and the [Model Context Protocol](https://modelcontextprotocol.io/).
It works with any agent implementation, because to FleetPermit an agent is a workload with an
identity that makes a tool call.

| | |
|---|---|
| **Main repository** | [fleetpermit/fleetpermit](https://github.com/fleetpermit/fleetpermit) |
| **Documentation** | [fleetpermit.github.io](https://fleetpermit.github.io/) |
| **Get started** | `make demo-up && make demo-run`: a 1 hub + 3 cluster lab on your laptop, no AI API keys needed |
| **Measured results** | [real multi-cluster scenarios and latencies](https://fleetpermit.github.io/results.html) |

### Security philosophy

Errors never add authority: a failure withdraws grants or leaves them to expire on time. A backend
with no grant is closed by the shipped default-deny anchor, which is part of the installation because
upstream enforces nothing on a backend without any policy. Leases can only narrow a policy, never
widen it. The time bound is enforced where the call happens. Every delivered rule is traceable to its
source by a SHA-256 content digest. These properties are backed by tests you can run. See the
[threat model](https://github.com/fleetpermit/fleetpermit/blob/main/docs/threat-model.md). Report
vulnerabilities privately through GitHub's **Report a vulnerability** button on the repository's Security tab.

### Contributing

Issues, reviews, docs and code are welcome. Start with
[CONTRIBUTING.md](https://github.com/fleetpermit/fleetpermit/blob/main/CONTRIBUTING.md).

<sub>FleetPermit is an independent open-source project, built on open technologies from the Kubernetes,
CNCF and Linux Foundation ecosystems. It is not affiliated with or endorsed by those organisations.
Apache-2.0.</sub>
