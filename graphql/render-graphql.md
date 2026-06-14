---
title: Render GraphQL Schema
description: >-
  Conceptual GraphQL schema for the Render cloud platform, covering services,
  deployments, environments, networking, autoscaling, git integration, teams,
  usage, and webhooks.
type: GraphQL
provider: Render
providerUrl: https://render.com
apiReferenceUrl: https://api-docs.render.com/reference/
schemaFile: render-schema.graphql
created: '2026-06-14'
---

# Render GraphQL Schema

Render is a cloud platform that lets teams deploy web services, static sites,
background workers, cron jobs, and private services from a Git repository or a
Docker image. Its public REST API (https://api.render.com/v1) exposes the full
surface of the platform. This conceptual GraphQL schema maps that surface to
strongly-typed GraphQL constructs, grouping related concerns into cohesive
object types.

## Schema source

The schema was derived from the Render Public API reference at
https://api-docs.render.com/reference/ and the official llms.txt index at
https://api-docs.render.com/llms.txt. No GraphQL endpoint is currently offered
by Render; this schema is a conceptual translation intended for tooling,
mocking, federation, and documentation purposes.

## Type groups

### Services

The core abstraction on Render is the **Service**. Each service has a
`ServiceType` (`WEB_SERVICE`, `STATIC_SITE`, `CRON_JOB`, `BACKGROUND_WORKER`,
`PRIVATE_SERVICE`). Specialised types (`WebService`, `StaticSite`, `CronJob`,
`BackgroundWorker`, `PrivateService`) add type-specific fields such as
health-check paths, cron schedules, and port declarations.

`ServiceDetails` carries build and runtime configuration that does not change on
every deploy (build command, start command, pre-deploy command, root directory,
auto-deploy flag, Docker settings).

### Deployments

A **Deploy** tracks a single deployment of a service. It holds a `DeployStatus`
enum that progresses through creation, build, live, or failure states. Every
deploy links to zero or more `DeployLog` lines and an optional `Build` record
that captures timing and status for the build phase.

### Environments and configuration

**Environment** groups related services under a shared namespace. **EnvGroup**
is a reusable set of environment variables and secret files that can be linked
to multiple services. **EnvVar** and **Secret** represent individual key-value
pairs and file-path secrets respectively.

### Networking

**CustomDomain** and **DomainVerification** track custom hostnames attached to
services. **TLSCert** records the status of automatically provisioned TLS
certificates. **NetworkPort** describes port/protocol pairs exposed by private
services. **Header**, **Redirect**, and **Rewrite** implement routing rules that
Render applies at the CDN edge.

### Autoscaling

**ScalingPolicy** describes an autoscaling configuration with a minimum and
maximum instance count. One or more **AutoscaleCriteria** each target a
`ScalingMetric` (`CPU`, `MEMORY`, `REQUESTS_PER_SECOND`) with a percentage
threshold. **MinInstances** and **MaxInstances** are scalar wrappers kept as
distinct types to allow future extension (e.g., scheduled scaling windows).

### Storage

**Disk** represents a persistent disk volume attached to a service. **DiskMount**
records the relationship between a disk and its mount path inside a container.

### Plans

**Plan** wraps the Render pricing tier (`FREE` through `PRO_ULTRA`) together with
the CPU shares, memory, price, and included bandwidth for that tier.

### Git integration

**Repo**, **Branch**, and **GitAccount** model the connection between a Render
service and its upstream source code. `GitProvider` distinguishes GitHub,
GitLab, and Bitbucket. Auto-deploy behaviour is driven by branch pushes detected
through these linked accounts.

### Teams and access control

**Owner** is either an individual user or an organisation. **Team** groups
members under a shared owner. **Member** assigns a **Role**
(`OWNER`, `ADMIN`, `MEMBER`, `BILLING_ADMIN`) to a **User**. **APIKey** records
bearer tokens scoped to an owner that authenticate REST and (conceptually)
GraphQL calls.

### Webhooks

**Webhook** allows an owner or service to push deployment events to an external
HTTP endpoint. The `events` list on each webhook mirrors the event types
available through the Render notification system.

### Usage and billing

**BandwidthUsage** and **BuildMinutes** capture consumption within a billing
period. **Usage** rolls both together with a period range under the owning
account, matching the data surfaced in the Render dashboard.

### Alerts and log streams

**Alert** fires when notable platform events occur (deploy failures, suspension,
credit limits). **LogStream** and **LogLine** expose the live and historical log
data available through the Render log streaming API.

### Pull request previews

**PullRequestPreview** represents a short-lived environment spun up automatically
when a pull request is opened against a service's repository. Each preview has
its own URL and deploy status lifecycle.

### Pipeline

**Pipeline** and **PipelineStep** model multi-service deployment workflows where
services are deployed in a defined order, optionally gating on the success of
earlier steps.

## Named types (57 total)

| # | Type | Kind |
|---|------|------|
| 1 | Service | Object |
| 2 | ServiceDetails | Object |
| 3 | ServiceType | Enum |
| 4 | WebService | Object |
| 5 | StaticSite | Object |
| 6 | CronJob | Object |
| 7 | BackgroundWorker | Object |
| 8 | PrivateService | Object |
| 9 | Environment | Object |
| 10 | EnvGroup | Object |
| 11 | EnvVar | Object |
| 12 | Secret | Object |
| 13 | Deploy | Object |
| 14 | DeployStatus | Enum |
| 15 | DeployLog | Object |
| 16 | DeployConnection | Object |
| 17 | DeployEdge | Object |
| 18 | Pipeline | Object |
| 19 | PipelineStep | Object |
| 20 | Build | Object |
| 21 | BuildCommand | Object |
| 22 | Docker | Object |
| 23 | DockerBuild | Object |
| 24 | Region | Enum |
| 25 | Plan | Object |
| 26 | PlanType | Enum |
| 27 | Disk | Object |
| 28 | DiskMount | Object |
| 29 | DiskMountType | Enum |
| 30 | Network | Object |
| 31 | NetworkPort | Object |
| 32 | CustomDomain | Object |
| 33 | DomainVerification | Object |
| 34 | DomainVerificationStatus | Enum |
| 35 | TLSCert | Object |
| 36 | TLSCertStatus | Enum |
| 37 | AutoscaleCriteria | Object |
| 38 | ScalingPolicy | Object |
| 39 | ScalingMetric | Enum |
| 40 | MinInstances | Object |
| 41 | MaxInstances | Object |
| 42 | Header | Object |
| 43 | HeaderOp | Enum |
| 44 | Rule | Object |
| 45 | Redirect | Object |
| 46 | RedirectType | Enum |
| 47 | Rewrite | Object |
| 48 | PullRequestPreview | Object |
| 49 | Repo | Object |
| 50 | Branch | Object |
| 51 | GitProvider | Enum |
| 52 | GitAccount | Object |
| 53 | Owner | Object |
| 54 | Team | Object |
| 55 | Member | Object |
| 56 | Role | Enum |
| 57 | User | Object |
| 58 | APIKey | Object |
| 59 | Webhook | Object |
| 60 | BandwidthUsage | Object |
| 61 | BuildMinutes | Object |
| 62 | Usage | Object |
| 63 | Alert | Object |
| 64 | AlertType | Enum |
| 65 | LogStream | Object |
| 66 | LogStreamType | Enum |
| 67 | LogLine | Object |
| 68 | PageInfo | Object |
| 69 | ServiceConnection | Object |
| 70 | ServiceEdge | Object |
| 71 | Query | Object |
| 72 | Mutation | Object |
| 73 | Subscription | Object |
| 74 | CreateServiceInput | Input |
| 75 | UpdateServiceInput | Input |
| 76 | EnvVarInput | Input |
| 77 | CreateEnvGroupInput | Input |
| 78 | UpdateEnvGroupInput | Input |
| 79 | ScalingPolicyInput | Input |
| 80 | AutoscaleCriteriaInput | Input |
| 81 | CreateWebhookInput | Input |

## Root operations

### Query

- `service(id)` — fetch a single service by ID
- `services(type, region, first, after)` — paginated list of services with optional filters
- `deploy(id)` — fetch a single deploy record
- `environment(id)` / `environments(ownerId)` — environment lookup
- `envGroup(id)` / `envGroups(ownerId)` — env-group lookup
- `customDomain(id)` — domain details
- `owner(id)` / `team(id)` — account and team lookup
- `usage(ownerId, periodStart, periodEnd)` — billing usage summary
- `logs(serviceId, type, since)` — log stream query
- `pipeline(id)` — pipeline details
- `webhook(id)` / `webhooks(ownerId)` — webhook management
- `alerts(ownerId)` — active and historical alerts

### Mutation

- `createService` / `updateService` / `deleteService`
- `suspendService` / `resumeService`
- `triggerDeploy` / `cancelDeploy`
- `createEnvGroup` / `updateEnvGroup` / `deleteEnvGroup`
- `addCustomDomain` / `removeCustomDomain` / `verifyCustomDomain`
- `updateScalingPolicy`
- `createWebhook` / `deleteWebhook`
- `createAPIKey` / `revokeAPIKey`
- `inviteMember` / `updateMemberRole` / `removeMember`

### Subscription

- `deployUpdated(serviceId)` — real-time deploy state changes
- `serviceStatusChanged(serviceId)` — suspension, scale events
- `logStream(serviceId, type)` — live log line streaming

## References

- Render REST API: https://api-docs.render.com/reference/
- Render Docs: https://render.com/docs
- Render GitHub: https://github.com/renderinc
- Render OSS: https://github.com/render-oss
- Render LLMs.txt: https://api-docs.render.com/llms.txt
