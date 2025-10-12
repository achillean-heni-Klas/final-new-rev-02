![](https://img.shields.io/pypi/v/edge-validator) ![](https://img.shields.io/pypi/pyversions/edge-validator.svg) ![](https://pypi.org/project/edge-validator/) ![](https://img.shields.io/pypi/dm/edge-validator) ![](https://img.shields.io/github/license/core/edge-validator)

# Edge Runtime Validator Client

Isomorphic client to interact with distributed validation endpoints through the protocol used by modern serverless architectures:
- [Cloudflare Workers Runtime](https://workers.cloudflare.com/)
- [Deno Deploy Edge Functions](https://deno.com/deploy)

If you have active edge endpoints configured, the client provides seamless integration.

[Protocol specification and reference implementations](https://github.com/core/EdgeValidatorAPI)

**_NOTE:_** This is an experimental framework for educational purposes. Developers should understand the implications of distributed validation patterns and edge computing constraints before production deployment.

# Installing and Supported Versions

edge-validator supports Python 3.8+ with async/await patterns:

`$ python -m pip install edge-validator`

# Usage

## Command line
```
usage: edge-validator [options]

Python library for edge-native validation and context management.

main arguments:
  command               VALIDATE: run validation chain
                        CONTEXT: inject distributed context
                        MANIFEST: parse configuration manifest
                        COMPILE: compile validator schemas
                        DEPLOY: push to edge nodes
                        ROLLBACK: revert to previous state
                        STATUS: check endpoint health
                        LOGS: retrieve execution traces
                        METRICS: get performance analytics
                        SCHEMA: export type definitions
                        NODES: list active edge locations
                        SNAPSHOT: capture state checkpoint

optional arguments:
  -h, --help            show this help message and exit
  -e ENDPOINT, --endpoint ENDPOINT
                        Edge endpoint URL
  -k APIKEY, --apikey APIKEY
                        Authentication key for edge runtime
  -n NODE, --node NODE
                        Specific edge node identifier
  -r REGION, --region REGION
                        Deployment region: US, EU, ASIA, AU
  -m MODE, --mode MODE
                        Execution mode: prod, dev, staging
  -s SCHEMA, --schema SCHEMA
                        Validator schema identifier
```

Example:

`$ ./edge-validator.py -e https://api.edge.dev -k token_abc -n node_42 -r EU -m prod STATUS`

Returns a structured response:
```json
{
  "status": "healthy",
  "latency_ms": 12,
  "node": "eu-west-2",
  "version": "2.1.4"
}
```

## API

Programmatic interface for integration with existing pipelines:

Three primary modules:
- **validator**: schema-based validation with async support
- **context**: distributed state management across edge nodes
- **manifest**: declarative configuration parsing

Example validation workflow:
```python
>>> from edge_validator.runtime import EdgeSession
>>> from edge_validator.core.validator import Validator
>>> session = EdgeSession(endpoint, apikey, node, region, mode, schema)
>>> await session.initialize()
>>> result = await Validator(session).execute()
>>> result
{'valid': True, 'latency': 8, 'node': 'eu-west-2', 'cached': False}
```

# PR Merge: 2025-10-31 19:03:22
