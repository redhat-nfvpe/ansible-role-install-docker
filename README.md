# ansible-role-install-docker

Install Docker using operating system repository. Allows for installation of
latest Docker version, or (optionally) a pinned Docker version.
Primarily used in
[kube-ansible](https://github.com/redhat-nfvpe/kube-ansible).

> **WARNING**
>
> This role will setup the `ansible_user` in the `docker` group, allowing for
> Docker to be run as a non-root user. Unfortunately, that effectively makes
> the non-root user a root user, which could potentially have security
> implications in your environment.

## Selecting Docker versions

This is optimized primarily for CentOS, and likely works with Fedora. However,
you have two options generally for installed Docker.

* RPMs installed from official CentOS repositories.
* Installation from Docker-CE RPM repos.

You may specify the variable `docker_repo_type` as either `ce` or `os`. The 
value of `os` is default, and stands for "operating system default", `ce` is
for "community edition" referring to Docker's nomenclature of their product.

For example, to override the default `os` value, reference the role as:

```
- { role: ansible-role-install-docker, docker_repo_type: "ce" }
```

## Role Variables

Available variables listed below along with their default values (see
`defaults/main.yml`):

Select the repository from which to install Docker.

```
docker_repo_type: "os"
```

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

An option to disable allowing docker for a non-root user:

```
docker_non_root_user: false
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
