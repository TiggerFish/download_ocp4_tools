download_ocp4_tools
=========

This role downloads multiple versions of the openshift installer and command line tools for multiple platforms.  
Additionally it will download the opm, helm and odo command line tools.  
The goal was to demonstrate that the files were downloaded from a known, secure source, produce logs of the download and that the checksums.... check.  

Requirements
------------

Written and tested with Ansible 2.9 on RHEL8 but will probably work with earlier versions and similar distros.

Role Variables
--------------

`vars/main.yml`  
```yaml
---
base_url: # The base url for the openshift tools.  
helm_base_url: # The base url for the helm clients.  
odo_base_url: # The base url for the odo clients.  
```
`defaults/main.yml`
```yaml
---
ocp_version: # A list of openshift versions to download the tools for.
ocp_tools: # A list of the tools to download.
ocp_platform: # A list of the platforms you wish to download the tools for.
get_helm: # Boolean to control if helm clients are downloaded.
helm_platform: # A list of the platforms you wish to download helm for.
get_odo: # Boolean to control if odo clients are downloaded.
odo_platform: # A list of the platforms you wish to download odo for.
download_location: # Where on the filesystem to download the components to.
```

Dependencies
------------

None

Example Playbook
----------------

Suggested `ansible.cfg`
```ini
[defaults]
inventory      = ./inventory
stdout_callback = skippy
log_path = ./download-ocp4-tools.log
[privilege_escalation]
become=false
```
Suggested `inventory`
```ini
[local]
localhost
```
Example `download-ocp4-tools.yml` playbook
```yaml
---
- name: "Download OCP4 Tools"
  hosts: local
  become: false
  gather_facts: false
  vars:
    ocp_version:
      - 4.7.39
      - 4.8.23
      - 4.9.10
    ocp_tools:
      - openshift-install
      - openshift-client
      - opm
    ocp_platform:
      - windows
      - linux
    get_helm: true
    helm_platform:
      - windows-amd64
      - linux-amd64
    get_odo: true
    odo_platform:
      - linux-amd64
      - windows-amd64
    download_location: /openshift/tools/
  roles:
    - download_ocp4_tools
```

License
-------

BSD

Author Information
------------------

An optional section for the role authors to include contact information, or a website (HTML is not allowed).
