# Ansible Docker/ee-install role

## Installation

* Using `ansible-galaxy`:

Not available yet.

* Using `requirements.yml`:

Not available yet.

Using `git`:

Not available yet.

## Dependencies

* Ansible >= 2.4

## Variables

Here is a list of all the default variables for this role, which are also available in `defaults/main.yml`, `vars/main.yml` and `vars/<distribution>.yml`.

| Name                         | Default value                                                                                                                                            | Location          |
|------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------|
| docker_ee_version            | "latest"                                                                                                                                                 | defaults/main.yml |
| docker_ee_package_version    | "{{ docker_ee_package_versions[ansible_distribution] &#124; default(docker_ee_package_versions[ansible_os_family]) &#124; default(docker_ee_version) }}" | defaults/main.yml |
| docker_ee_release_channel    | "stable"                                                                                                                                                 | defaults/main.yml |
| docker_ee_subscription       | "{{ docker_ee_subscriptions[ansible_distribution] &#124; default(docker_ee_subscriptions[ansible_os_family] &#124; default(omit)) }}"                    | defaults/main.yml |
| docker_ee_repository_url     | "https://storebits.docker.com/ee/{{ ansible_distribution &#124; lower }}/{{ docker_ee_subscription }}"                                                   | vars/main.yml     |
| docker_ee_repository_gpg_url | "{{ docker_ee_repository_url }}/{{ ansible_distribution &#124; lower}}/gpg"                                                                              | vars/main.yml     |

## Usage

This is an example playbook:

```yaml
- hosts: all
  become: true
  roles:
  - role: docker-ee-install
  vars:
    docker_ee_subscriptions:
      Ubuntu: "sub-www-xxx-yyy-zz1"
      RedHat: "sub-www-xxx-yyy-zz2"
      CentOS: "sub-www-xxx-yyy-zz3"
```


## Testing
```shell
$ echo -e "{\"Ubuntu\": \"<your_subscription_for_ubuntu>\", \"CentOS\": \"$<your_subscription_for_centos>\"}" > tests/subscriptions.json
$ make test # To run all tests.
$ make ubuntu16.04-test # To run a specific test (e.g. ubuntu16.04-test, ubuntu14.04-test, centos7-test).
```
