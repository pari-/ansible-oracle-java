# oracle_java8

[![Build Status](https://travis-ci.org/pari-/ansible-oracle-java8.svg?branch=master)](https://travis-ci.org/pari-/ansible-oracle-java8)

An Ansible role which installs and configures Oracle's Java 8

<!-- toc -->

- [Requirements](#requirements)
- [Example](#example)
- [Variables](#variables)
  * [Role Variables](#role-variables)
  * [Role Internals](#role-internals)
- [Dependencies](#dependencies)
- [License](#license)
- [Author Information](#author-information)

<!-- tocstop -->

## Requirements

Currently this role is developed for and tested on Debian GNU/Linux (release: jessie). It is assumed to work on other Debian distributions as well.

Ansible version compatibility:

- __2.3.0.0__ (current version in use for development of this role) 
- 2.2.3.0
- 2.1.5.0
- 2.0.2.0

## Example

```yaml
- hosts: oracle_java8-hosts

  vars:
    oracle_java8_apt_key_id: "EEA14886"

  roles: 
    - "ansible-oracle_java8"
```

## Variables

Available variables are listed below, along with default values (see defaults/main.yml). They're generally prefixed with `oracle_java8_` (which I deliberately leave out here for better formatting).

### Role Variables

variable | default | notes
-------- | ------- | -----
`apt_key_id` | `EEA14886` | `The identifier for the key of the webupd8team/java repository. Including this allows check mode to correctly report the changed state`

### Role Internals

variable | default | notes
-------- | ------- | -----
`cache_valid_time` | `3600` | `Update the apt cache if its older than the set value (in seconds)` |
`default_release` | `{{ oracle_java8_repo_mapping[ansible_distribution|lower] }}` | `The default release to install packages from` |
`oracle_java8_keyserver` | `keyserver.ubuntu.com` | `The keyserver to retrieve key from` | 
`package_list` | `['oracle-java8-installer', 'oracle-java8-set-default']` | `The list of packages to be installed`
`repo_list` | `["deb http://ppa.launchpad.net/webupd8team/java/ubuntu {{ oracle_java8_repo_mapping[ansible_distribution|lower] }} main"]` | `Source strings for the repositories`
`repo_mapping['debian']` | `xenial` | `A variable used to do proper repository mapping for different debian-based distributions` |
`repo_mapping['ubuntu']` | `{{ ansible_distribution_release }}` | `A variable used to do proper repository mapping for different debian-based distributions` |
`supported_distro_list` | `['jessie', 'trusty']` | `A list of distribution releases this role supports`
`update_cache` | `yes` | `Run the equivalent of apt-get update before the operation`

## Dependencies

None

## License

MIT

## Author Information

* Patrick Ringl
