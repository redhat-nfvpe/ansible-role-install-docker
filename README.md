# ansible-role-install-docker

Install Docker from upstream Docker RPM repository. Allows for installation of
latest Docker version in repository, or (default) a pinned Docker version.
Primarily used in 
[kube-centos-ansible](https://github.com/redhat-nfvpe/kube-centos-ansible).

## Role Variables

Available variables listed below along with their default values (see
`defaults/main.yml`):

```
docker_engine_base_name: docker-engine
docker_engine_version: 17.03.1.ce
```

## Dependencies

None.

## Example Playbook

```
- hosts: docker_host
  become: true
  become_user: root

  roles:
    - { role: install-docker, docker_engine_version: latest }
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
