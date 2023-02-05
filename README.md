<p><img src="https://github.com/distribution/distribution/raw/main/distribution-logo.svg" alt="registry-logo" title="registry" align="top" height=180 /></p>

*The toolkit to pack, ship, store, and deliver container content*

### General informations

This Ansible is designed to deploy and configure the Docker Registry distribution on target server(s).

**Table of Contents**

  - [Roles variables](#role-variables)
  - [Examples](#examples)
  - [Install and use this role](#install-and-use-this-role)

**References**

  - Distribution : https://github.com/distribution/distribution

### Role variables

The role variables documentation are available here :

  - [General](docs/variables.md)

### Examples

You can find some configurations examples :

  - [Configure the Docker Registry](docs/examples.md)

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
