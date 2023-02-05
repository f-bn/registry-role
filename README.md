<p><img src="https://github.com/distribution/distribution/raw/main/distribution-logo.svg" alt="registry-logo" title="registry" align="top" height=180 /></p>

*The toolkit to pack, ship, store, and deliver container content*

### General informations

This Ansible is designed to deploy and configure the Docker Distribution registry on target server(s) (using binary).

**Table of Contents**

  - [Roles variables](#role-variables)
  - [Examples](#examples)
  - [Install and use this role](#install-and-use-this-role)

**References**

  - Docker Registry : https://docs.docker.com/registry/
  - Distribution : https://github.com/distribution/distribution

### Role variables

| Name                              | Default                      | Description                                                      |
| :-------------------------------- | :--------------------------- | :--------------------------------------------------------------- |
| `registry_version`                | `2.8.1`                      | Defines the version of Registry to install                        |
| `registry_install_dir`            | `/usr/local/bin`             | Defines the Registry binary installation directory               |
| `registry_config_dir`             | `/etc/registry`              | Defines the Registry configuration directory                     |
| `registry_config_path`            | `{{ registry_config_dir }}/config.yaml`|  Defines the absolute path to the Registry configuration file |
| `registry_data_dir`               | `/var/lib/registry`          | Defines the data directory where all registry files are stored   |
| `registry_logs_dir`               | `/var/log/registry`          | Defines the logs directory of the Registry                       |
| `registry_binary_archive_url`     | see [vars](vars/main.yml)    | Defines the URL where to download the Registry binary archive    |
| `registry_binary_archive_checksum`| see [vars](vars/main.yml)    | Defines the Registry binary archive checksum (sha256 checksum)   |
| `registry_binary_update`          | `false`                      | If set to `true`, force the Registry binary update               |
| `registry_configuration`          | see [defaults](defaults/main.yml) | Defines a YAML dict containing the Registry configuration (see [examples](€examples) below |

### Examples

The configuration of the Registry is pretty simple, it's a simple YAML dictionnary :

```YAML
registry_configuration:
  version: 0.1  # Required
  log:
    level: info
  storage:      # Required
    filesystem:
      rootdirectory: /var/lib/registry
    maintenance:
      uploadpurging:
        enabled: true
        age: 168h
        interval: 24h
        dryrun: true
  http:
    addr: 0.0.0.0:5000
    host: https://my.registry.internal:5000

  # Configure the registry as pull-through cache
  proxy:
    remoteurl: https://registry-1.docker.io
    username: <username>
    password: <password>
```

### Install and use this role

* Install the role using the command-line :

  ```shell
  $ ansible-galaxy role install git+https://github.com/f-bn/registry-role.git registry
  ```

* You can also install the role in your projects using a `requirements.yml` file and `ansible-galaxy` command-line :

  ```YAML
  $ cat requirements.yml
  ---
  roles:
    - name: registry
      src: https://github.com/f-bn/registry-role.git
      scm: git
      version: '1.0.0'

  $ ansible-galaxy install-f -r requirements.yml
  ```

* Once the role is installed, you can use it in your playbooks :

  ```yaml
  - name: Deploy
    hosts: <hosts>
    roles:
      - role: registry
  ```
