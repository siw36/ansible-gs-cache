ansible_gs_cache
=========

This role deploys a lancachenet gaming cache based on docker containers.

Requirements
------------

This role expects docker to be installed on the target host.  
I recommend to use the `geerlingguy.pip` and `geerlingguy.docker` ansible roles for that.  

Role Variables
--------------

| Name | Description | Default value |
|---|---|---|
| cacheNewDisk | Set this to a raw block device attached to the machine to use this disk as storage for the cache. __The given disk will be formatted.__ | <none - optional> |
| cacheBaseDir | The data dir for the proxy. If you use the new disk variable, the new disk will be mounted there. | /var/cache |
| cacheDNS | Upstream DNS server | 1.1.1.1 1.0.0.1 |
| cacheMemSize | Amount of RAM to use for caching | 2000m |
| cacheDiskSize | Amount of disk space to use for cache | 20000m |
| cacheMaxAge | Retention time of cached data | 60d |
| cacheNewDiskFS | File system for the new disk (only used if `cacheNewDisk` is defined) | xfs |
| cacheDNSImage | Docker image for cache DNS | lancachenet/lancache-dns:latest |
| cacheImage | Docker image for the cache | lancachenet/monolithic:latest |
| cacheSSLImage | Docker image for the cache SSL proxy | lancachenet/sniproxy:latest |

Dependencies
------------

- `geerlingguy.pip` + the python package `docker-compose`
- `geerlingguy.docker`

Get this role (and dependencies)
------------
```bash
ansible-galaxy install --roles-path ./roles/ geerlingguy.pip geerlingguy.docker siw36.ansible_gs_cache
```

Example Playbook
----------------

Install docker with the dependent pip package, followed by the lancache itself.  
```yaml
- hosts: gs-cache
  become: true
  vars:
    pip_install_packages:
      - docker-compose
  roles:
    - geerlingguy.pip
    - geerlingguy.docker
    - ansible-gs-cache
```
License
-------

GNU General Public License v3.0

Author Information
------------------

Created by Robin 'siw36' Klussmann (08/2019)
