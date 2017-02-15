Manage ES (Elasticsearch Service)
=========

## Usage
```
- role: reactiveops.manage-es
  es_domain_name: "{{ env }}"
  es_version:
  es_elasticsearch_cluster_config
  es_ebs_options
  es_access_policies
  es_snapshot_options
  es_advanced_options
  es_cli_input_json
  es_generate_cli_skeleton


  rds_environment: "{{ env }}"
  rds_context: "{{ context }}"
  rds_security_group_ids: "{{ hostvars[inventory_hostname][context + '_data'] }}"
  rds_master_username: "{{ lookup('env', 'RDS_USER') }}"
  rds_master_password: "{{ lookup('env', 'RDS_PASSWORD') }}"
  rds_db_engine: "postgres"
  rds_db_engine_version: "9.5.4"
```

It is also possible to use this role to modify an instance. To do so it is easiest to override settings from the command line:

```shell
ansible-playbook stack.yml  -e 'rds_command=modify' -e 'apply_immediately=yes'
```

For a list of valid `rds_db_engine` and `rds_db_engine_version` values, run `aws rds describe-db-engine-versions`.

The result of the `rds` resource will be stored in `manage_rds_{{ rds_name | replace('-', '_') }}": "{{result}}`. A `rds_name` of `foo-bar` would be set as `manage_rds_foo_bar`.

Custom parameter groups can be specified with `rds_db_parameter_group`. A default will be picked based on the engine and engine version if not specified.
