S3 Bucket
=========

Create an S3 bucket in AWS

Currently only creates one bucket

Requirements
------------

Assumes AWS creds are configured in the environment already
boto for aws modules

Role Variables
--------------

``` yaml
s3_name: # name of the bucket
s3_encryption: # S3 encryption type, default to AES256

s3_state: # optional to delete a bucket, defaults to present

s3_lifecycle_rule_name: # Name of the lifecycle rule to apply (only used when s3_lifecycle set to true)
s3_lifecycle: # Boolean (True/False) to add lifecycle rules, if true rules will be created if not missing input below
s3_lifecycle_prefix: # define a prefix of folder to apply rule at, if not used it will cover the whole bucket
s3_version_days: # set the days it takes to remove old version
s3_expiration_days: # set the expiration of data in days
s3_lifecycle_status: # enable or disable the rule, defaults to enabled
```

Dependencies
------------

This can only make buckets that appear as "can be public", I havent tried the public access blocking buckets feature introduced here: [Public Access Blocking](https://github.com/ansible-collections/amazon.aws/pull/171)

**You need to go an change it to private**

Example Playbook
----------------

```yaml
---
- name: s3 Provisioning
  hosts: localhost
  gather_facts: false
  pre_tasks:
    - name: Setting vars for new bucket
      set_fact:
        s3_name: my-new-bucket

        s3_lifecycle: True
        s3_version_days: 1
        s3_expiration_days: 1
  roles:
    - s3-bucket
```

License
-------

MIT

Author Information
------------------

Adam Brassard: ABrass on IRC
