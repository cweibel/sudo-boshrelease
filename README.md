# `sudo` BOSH Release

BOSH Release to patch SUDO 1.9.5p2

## Example Usage

Add the `sudo` job to any instance_group you'd like it deployed to and add a reference to the `sudo` release in the releases section.

```
name: emptyvm

instance_groups:
- name: emptyvm
  azs: [z1]
  instances: 1
  jobs: 
  - name: sudo
    release: sudo
  vm_type: default
  stemcell: default
  persistent_disk: 10240
  networks:
  - name: default

releases: 
- name: sudo
  version: latest
  url: https://github.com/cweibel/sudo-boshrelease/releases/download/1/sudo-boshrelease.tar.gz

stemcells:
- alias: default
  os: ubuntu-trusty
  version: latest

update:
  canaries: 2
  max_in_flight: 1
  canary_watch_time: 5000-60000
  update_watch_time: 5000-60000

```

Consider leveraging the [BOSH Runtime Config](https://bosh.io/docs/runtime-config/) to deploy this to all deployments without having to modify each deployment yaml.


## Why does this exist?

Not everyone may be in a position to upgrade to stemcell 621.99 or newer, this BOSH release is a patch for [https://ubuntu.com/security/notices/USN-4705-1](https://ubuntu.com/security/notices/USN-4705-1).

Once deployed, this will replace the version of `sudo` which comes by default on the stemcell.
