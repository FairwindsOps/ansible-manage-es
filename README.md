Manage AWS ES (Elasticsearch Service) domains
=========

This Ansible role can be used to create and modify AWS Elasticsearch Service Domains.

## Usage

The only truly required variables are `es_domain_name` and `aws_region`, but without the `es_ip_whitelist` you will not be able to connect to the Elasticsearch Service endpoint. At this point only IP whitelisting is supported. The following will create a single instance Elasticsearch Service domain.

```yaml
- role: ansible-manage-es
  es_domain_name: 'my-search-thingy'
  aws_region: 'us-east-1'
  es_instance_type: 'm3.medium.elasticsearch'
  es_ip_whitelist:
    - "111.111.111.111"
    - "222.222.222.1/24"
```

By default the cluster is not aware of zones. This can be enabled via the following setting. You will also need an even number in the `es_instance_count` setting.

```yaml
  es_zone_awareness: yes
  es_instance_count: 2
```

To avoid issue with cluster coordination you can create dedicated masters. These do not need to large in size.

```yaml

  es_dedicated_master: yes
  es_dedicated_master_type: 't2.small.elasticsearch'
  es_dedicated_master_count: '3'
```

For clusters that need to store a lot of data it makes sense to use EBS volumes:

```yaml
  es_ebs_enabled: yes
  es_ebs_volume_type: gp2
  es_ebs_volume_size: 10
```

note: if the `es_ebs_volume_type` is `io1` then `es_ebs_iops` must also be set.

Please consult [defaults/main.yml](defaults/main.yml) for default settings.
