# Ansible Role: drone

This role will install drone agents+server (using docker-compose)

# Requirements
This role requires:
  - docker installed on the server

# Role Variables

## Role Configuration variables

```
drone_server_image: "drone/drone"
drone_agent_image: "drone/agent"
drone_version: "latest"
```
With these parameters, you can change the base repository and the version to be used for the deployment

``` 
drone_start_server: true
drone_start_agent: true
```
With these two parameters, you can specify what parts of a drone setup will be deployed (defaults: to drone agent+server)

```
drone_agent_count: 1
```
With this parameter, you define the amount of drone-agents that will be deployed per instance (default: 1)

```
drone_debug: false
```
With this parameter, you define if drone will start in debug mode (default: false)

```
drone_open: true
```
With this parameter, you define if drone is open for everyone to register (default: true)

```
drone_agent_debug: false
```
With this parameter, you define if drone agent will start in debug mode (default: false)

## Drone specific parameters

The role exposes all parameters that can be used to configure drone via the ansible role

### Server
**Required**
- `drone_secret`
- `drone_admin`
- `drone_vcs`
- `drone_server_url`


**Optional**
- `drone_open`
- `drone_database_driver`
- `drone_database_config`
- `drone_orgs`
- `drone_debug`
- `drone_server_cert`
- `drone_server_key`
- `drone_yaml`
- `drone_cache_tty`


### Agent
**Required**
- `drone_secret`
- `drone_server_host`

**Optional**
- `drone_agent_server_url` 
- `drone_agent_https_proxy`
- `drone_agent_http_proxy`
- `drone_agent_docker_os`
- `drone_agent_docker_arch`
- `drone_agent_docker_max_procs`
- `drone_agent_docker_cert_path`
- `drone_agent_docker_tls_verify`
- `drone_agent_docker_host`
- `drone_agent_plugin_privileged`
- `drone_agent_plugin_pull`
- `drone_agent_max_logs`
- `drone_agent_timeout`
- `drone_agent_backoff`
- `drone_agent_debug`

### VCS
#### github
**Required**
- `drone_github_client`
- `drone_github_secret`

**Optional**
- `drone_github_url`
- `drone_github_scope`
- `drone_github_username`
- `drone_github_password`
- `drone_github_private_mode`
- `drone_github_merge_ref`
- `drone_github_context`
- `drone_github_skip_verify`

#### bitbucket
**Required**
- `drone_bitbucket_client`
- `drone_bitbucket_secret`

### additional parameters
The ansible role offers additional parameters - please check `defaults/main.yml`


# Example Playbook

```
- hosts: drone
  vars_files:
    - vars/main.yml
  roles:
    - { role: solutiondrive.drone }
```
Inside `vars/main.yml`
```
drone_admin: "admin"
drone_secret: "thisisnotasecuresecret"
drone_server_host: "drone.domain.tld"
drone_vcs: "github"
drone_github_client: "github_client_token"
drone_github_secret: "github_client_secret"
drone_agent_count: 3
```

# Maintainer
- Patrick Jahns <jahns@solutiondrive.de>
- Tobias Lückel <lueckel@solutiondrive.de>
