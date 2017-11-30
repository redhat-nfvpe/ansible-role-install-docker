# ansible-role-install-docker

Install Docker using operating system repository. Allows for installation of
latest Docker version, or (optionally) a pinned Docker version.
Primarily used in
[kube-centos-ansible](https://github.com/redhat-nfvpe/kube-centos-ansible).

## Role Variables

Available variables listed below along with their default values (see
`defaults/main.yml`):

Set the package base name. If installing from another repository, may need to
change the base name to something like `docker-engine`.
```
docker_package_base_name: docker
```

Pin a version of the package to install. If set to `latest` (the default) then
install the latest version of the available Docker package. Does not
automatically upgrade on subsequent runs.
```
docker_package_version: latest
```

A list of Docker registries to configure for the daemon. These are trusted
repositories and must be coming from a trusted SSL certification.
```
docker_registries: []
```

A list of Docker registries to configure for the daemon. These are untrusted
repositories, and do not require proper certificates. Useful when running a
local registry.

```
docker_insecure_registries: []
```

A list of Docker registries to block.

```
docker_block_registries: []
```

## Dependencies

None.

## Example Playbook

```
- hosts: docker_host
  become: true
  become_user: root

  roles:
    - { role: install-docker, docker_package_version: '1.12.6' }
```

## Testing

You can locally test a deployment of this role using
[provision_docker](https://github.com/chrismeyersfsu/provision_docker).

```
cd tests/
ansible-playbook test.yml
```

## License

Apache v2.0

## Author Information

This role was created in 2017 by the
[Red Hat NFVPE Team](https://github.com/redhat-nfvpe).
