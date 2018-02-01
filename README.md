# Ansible Role: Docker

An Ansible Role that installs [Docker](https://www.docker.com) on Linux.

## Requirements

None.

## Role Variables

Available variables are listed below, along with default values (see `defaults/main.yml`):

    # Edition can be one of: 'ce' (Community Edition) or 'ee' (Enterprise Edition).
    docker_edition: 'ce'
    docker_package: "docker-{{ docker_edition }}"
    docker_package_state: present

The `docker_edition` should be either `ce` (Community Edition) or `ee` (Enterprise Edition). You can also specify a specific version of Docker to install using a format like `docker-{{ docker_edition }}-<VERSION>`. And you can control whether the package is installed, uninstalled, or at the latest version by setting `docker_package_state` to `present`, `absent`, or `latest`, respectively.

    docker_install_compose: true
    docker_compose_version: "1.18.0"
    docker_compose_path: /usr/local/bin/docker-compose

Docker Compose installation options.

    docker_apt_release_channel: stable
    docker_apt_repository: "deb https://download.docker.com/linux/{{ ansible_distribution|lower }} {{ ansible_distribution_release }} {{ docker_apt_release_channel }}"

(Used only for Debian/Ubuntu.) You can switch the channel to `edge` if you want to use the Edge release.

    docker_yum_repo_url: https://download.docker.com/linux/centos/docker-{{ docker_edition }}.repo
    docker_yum_repo_enable_edge: 0
    docker_yum_repo_enable_test: 0

(Used only for RedHat/CentOS.) You can enable the Edge or Test repo by setting the respective vars to `1`.

### Daemon Configuration

You can customize daemon configuration by creating a YAML structure of options under `docker_daemon_config`. For a list of available options, check the [dockerd docs](https://docs.docker.com/engine/reference/commandline/dockerd/#daemon-configuration-file). By default, it is set to configure devicemapper storage with direct-lvm for CentOS.

    docker_configure_daemon_deb: false
    docker_configure_daemon_rh: true

Set to true if the configuration should be used for Debian/Ubuntu or RHEL/CentOS hosts, respectively.


## Dependencies

None.

## Example Playbook

```yaml
- hosts: all
  roles:
    - cavemandaveman.docker
```

## License

GPLv3

## Author Information

This role was created in 2018 by cavemandaveman.
