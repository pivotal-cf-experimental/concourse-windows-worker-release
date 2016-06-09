# concourse-windows-release

```
---
name: concourse_windows
director_uuid: $UUID

releases:
- name: concourse_windows
  version: latest

resource_pools:
- name: default
  network: default
  stemcell:
    name: bosh-aws-xen-hvm-windows-stemcell-go_agent
    version: latest
  cloud_properties:
    instance_type: c3.xlarge
    availability_zone: us-east-1a

compilation:
  workers: 1
  network: default
  cloud_properties:
    availability_zone: us-east-1a
    instance_type: c3.large

update:
  canaries: 0
  canary_watch_time: 60000
  update_watch_time: 60000
  max_in_flight: 2

jobs:
- name: concourse_windows
  templates:
  - name: concourse_windows
  instances: 1
  resource_pool: default
  networks:
  - name: default
  properties:
    concourse_windows:
      tsa_host: concourse.ci
      tsa_public_key: "ssh-rsa key"
      tsa_worker_private_key: |
        -----BEGIN RSA PRIVATE KEY-----
        cool
        -----END RSA PRIVATE KEY-----
```
