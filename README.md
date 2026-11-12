# Charles Stephen Thompson

Infrastructure and automation engineer in Brooklyn, NY. I run DNS, identity and databases, and I script anything I have to do twice.

[cst.nyc](https://cst.nyc) · [blog.cst.nyc](https://blog.cst.nyc)

Open to infrastructure, platform and automation engineering roles. The best way to reach me is through [cst.nyc](https://cst.nyc).

## What I work on

**DNS that stays up.** A [Technitium](https://technitium.com/dns/) DNS cluster: DNSSEC-signed zones and a validating resolver, encrypted DNS (DoT, DoH and DoQ), a dnsdist and keepalived front end with a floating address, zones replicated between nodes with catalog zones, and a blocklist of well over a million entries that the gateway enforces by blocking or redirecting DNS to any other resolver. Certificates come from a flow built on ACME DNS-01 over RFC 2136 with scoped TSIG keys, so no client can write to the cluster directly. Both nodes are up, with an offline root.

**Databases for log-scale data.** PostgreSQL and TimescaleDB for high-volume syslog and DNS query logs: hypertables with chunk-drop retention instead of batch deletes, connection pooling with PgBouncer, and a PostgreSQL 18 image with TimescaleDB, pgvector and pgvectorscale that rebuilds daily. I have also run Patroni with etcd, synchronous replication and automatic failover, and have since simplified that setup.

**Identity.** A decade of enterprise IAM and SSO (Active Directory, Okta, Google, SAML) before this, and I still build on it: OIDC and PKCE single sign-on across my own services.

**Automation.** Hosts are configured with Ansible (roles that are tested by converging them twice in a container), services run as Podman Quadlet units, and secrets stay out of git. CI rebuilds images when an upstream project releases.

## Selected projects

| Project | What it is |
|---|---|
| [technitium-dns-multi](https://github.com/charlestephen/technitium-dns-multi) | One container that bundles Technitium, dnsdist (DoT, DoH and DoQ, with the PROXY protocol so Technitium sees real client addresses), keepalived, acme.sh and PgBouncer, each switched on by an environment variable. Multi-arch images on GHCR and Docker Hub, released automatically. |
| [old-homelab](https://github.com/charlestephen/old-homelab) | One-shot installers that rebuild a home lab from a single zip on a clean Debian install: a high-availability DNS pair, a core services host, a public edge host with Traefik, CrowdSec and geoblocking, and an application host. Services are Podman Quadlet units that `podlet` generates from `podman run` lines, secrets are Podman secrets, and the Traefik API always requires a login. Checked with dry runs, generated-unit validation and live containers. |
| [dns-ip-list-chunker](https://github.com/charlestephen/dns-ip-list-chunker) | A Go service that merges and deduplicates DNS and IP blocklists and serves them in sizes routers accept. After profiling, a full refresh of 26 real lists (1.8 million entries) dropped from about 14 s to about 2 s, and a refresh with nothing changed does no work. Output was verified identical. |
| [hassio-apps](https://github.com/charlestephen/hassio-apps) | 37 Home Assistant add-ons for infrastructure tools, including Traefik, Forgejo, PostgreSQL, PgBouncer and Technitium. Built for arm64 and amd64, with upstream version tracking, CodeQL, Trivy, hadolint and commit-pinned actions. |
| [pgVectorScaleDB](https://github.com/charlestephen/pgVectorScaleDB) | A PostgreSQL 18 image with TimescaleDB, pgvector, pgvectorscale and system_stats. A daily workflow refreshes the pinned versions and publishes. |
| [unifi-geoip-blocklist-updater](https://github.com/charlestephen/unifi-geoip-blocklist-updater) | A Go container that keeps GeoIP blocklists in UniFi firewall rules current. |

I also maintain Homebridge plugins: [homebridge-frigidaire-connected-ac](https://github.com/charlestephen/homebridge-frigidaire-connected-ac) (with a dependency-free TypeScript client for the Frigidaire cloud API) and [homebridge-git-backup](https://github.com/charlestephen/homebridge-git-backup).

## How I work

- **Measure, then change.** I profile before I rewrite, and I compare output before and after so a faster version is not a different one.
- **Test the real thing.** Where I can, I test against the actual servers and containers rather than mocks of them.
- **Keep secrets out of git.** Code, values and secrets are separate layers, with secret scanning on commit.
- **Pin and verify.** Actions are pinned to commit SHAs, dependencies are updated by Renovate, and my commits are signed with a hardware key.
- **Write down the limits.** My READMEs say what a project does not do.

## Stack

Go · Python · Bash · TypeScript · PostgreSQL · TimescaleDB · Technitium · dnsdist · keepalived · Traefik · CrowdSec · Podman · Ansible · Home Assistant · n8n · UniFi · Forgejo and GitHub Actions
