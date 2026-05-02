# Render

Render is a cloud platform for building and running applications and websites with automatic Git-based deployments. It provides managed infrastructure for web services, static sites, background workers, cron jobs, private services, PostgreSQL databases, Redis/Key-Value stores, and persistent disks. The Render API enables programmatic control of all platform resources including service deployments, scaling, environment configuration, custom domains, blueprints, logging, metrics, and workflow automation.

**Human URL:** [https://render.com](https://render.com)

**API Reference:** [https://api-docs.render.com](https://api-docs.render.com)

---

## APIs

### Render API

The Render Public API (v1.0.0) provides full programmatic management of all Render cloud resources at `https://api.render.com/v1`. Authentication uses a Bearer API key. The spec covers 122 endpoint paths across 26 feature areas including services, deployments, databases, blueprints, logs, metrics, workflows, and more.

- **Documentation:** [https://render.com/docs/api](https://render.com/docs/api)
- **OpenAPI Spec:** [openapi/render-openapi.json](openapi/render-openapi.json)
- **Rules:** [rules/render-rules.yml](rules/render-rules.yml)
- **Capabilities:** [capabilities/service-deployment.yaml](capabilities/service-deployment.yaml)

---

## Artifacts

### OpenAPI

| File | Description |
|---|---|
| [openapi/render-openapi.json](openapi/render-openapi.json) | Render Public API v1.0.0 — 122 paths, 26 tag groups |

### Rules

| File | Description |
|---|---|
| [rules/render-rules.yml](rules/render-rules.yml) | Spectral ruleset enforcing Render API naming and authentication conventions |

### Capabilities

| File | Description |
|---|---|
| [capabilities/service-deployment.yaml](capabilities/service-deployment.yaml) | Service deployment and infrastructure management workflow — 24 MCP tools |
| [capabilities/shared/render-api.yaml](capabilities/shared/render-api.yaml) | Shared Render API consumed definition |

### JSON Schema

| File | Description |
|---|---|
| [json-schema/render-service-schema.json](json-schema/render-service-schema.json) | JSON Schema for Render Service resource |
| [json-schema/render-deploy-schema.json](json-schema/render-deploy-schema.json) | JSON Schema for Render Deploy resource |

### JSON Structure

| File | Description |
|---|---|
| [json-structure/render-service-structure.json](json-structure/render-service-structure.json) | Structural documentation for Render Service |

### JSON-LD

| File | Description |
|---|---|
| [json-ld/render-context.jsonld](json-ld/render-context.jsonld) | JSON-LD context mapping Render resources to schema.org |

### Examples

| File | Description |
|---|---|
| [examples/render-create-service-example.json](examples/render-create-service-example.json) | Create a new Node.js web service |
| [examples/render-trigger-deploy-example.json](examples/render-trigger-deploy-example.json) | Trigger a deployment for a service |

### Vocabulary

| File | Description |
|---|---|
| [vocabulary/render-vocabulary.yml](vocabulary/render-vocabulary.yml) | Domain vocabulary for Render cloud platform concepts |

---

## Common Properties

| Property | URL |
|---|---|
| Website | [https://render.com](https://render.com) |
| Documentation | [https://render.com/docs](https://render.com/docs) |
| API Documentation | [https://render.com/docs/api](https://render.com/docs/api) |
| Dashboard | [https://dashboard.render.com](https://dashboard.render.com) |
| Community | [https://community.render.com](https://community.render.com) |
| GitHub | [https://github.com/renderinc](https://github.com/renderinc) |
| Status | [https://status.render.com](https://status.render.com) |
| Blog | [https://render.com/blog](https://render.com/blog) |

## Maintainers

**FN:** Kin Lane

**Email:** kin@apievangelist.com
