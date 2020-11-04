# Lightbend Kafka Lag Exporter

Ansible Role for installing and configuring the [Kafka Lag Exporter](https://github.com/lightbend/kafka-lag-exporter) from Lightbend.

![GitHub release (latest by date including pre-releases)](https://img.shields.io/github/v/release/nerdynick/kafka-lag-exporter-ansible?include_prereleases)
![Travis (.com)](https://img.shields.io/travis/com/nerdynick/kafka-lag-exporter-ansible)
![GitHub](https://img.shields.io/github/license/nerdynick/kafka-lag-exporter-ansible)
![GitHub All Releases](https://img.shields.io/github/downloads/nerdynick/kafka-lag-exporter-ansible/total)


## Requirements

* Java 8+ installed on host
* unzip installed on host

## Role Variables

### Controlling the Installation

| Variable | Default | Description |
| -------- | ------- | ----------- |
| kafka_lag_exporter_version | 0.6.5 | Which release to install from Github Release |
| kafka_lag_exporter_service_name | kafka-lag-exporter | Service Name for System.d |
| kafka_lag_exporter_user | kafkalag | User for all file permissions and system.d execution |
| kafka_lag_exporter_group | kafkalag | Group for all file permissions and system.d execution |
| kafka_lag_exporter_config_dir | /etc/kafka-lag-exporter | Directory where all Configuration should exist |
| kafka_lag_exporter_extraction_dir | /opt/kafka-lag-exporter | Directory where the archive should be extracted |
| kafka_lag_exporter_download | true | Bool on if the archive should be downloaded from the Github Releases Archive. Uses  `kafka_lag_exporter_download_url` to determin where to download from. | 
| kafka_lag_exporter_download_url | https://github.com/lightbend/kafka-lag-exporter/releases/download/v{{ kafka_lag_exporter_version }}/kafka-lag-exporter-{{ kafka_lag_exporter_version }}.zip | URL where to download the Archive |
| kafka_lag_exporter_upload | false | Bool to control if the archive should be uploaded from the local ansible controller rather then downloaded |
| kafka_lag_exporter_upload_path |  | Local path where to find the archive to upload |

### Configuraing Kafka Lag Exporter

| Variable | Default | Description |
| -------- | ------- | ----------- |
| kafka_lag_exporter_poll_interval | 30 seconds | How frequent to check Kafka Cluster for Offsets |
| kafka_lag_exporter_client_group_id | kafkalagexporter | Consumer Group ID for the embeded Kafka Consumer |
| kafka_lag_exporter_client_timeout | 10 seconds | TCP timeout for Kafka Clients |
| kafka_lag_exporter_lookup_table_size | 60 |  |
| kafka_lag_exporter_environment_overrides | {} | Map of ENV Vars to populate in System.d execution environment |
| kafka_lag_exporter_metric_whitelist | [".*"] | Whitelist of metrics to return |


## Dependencies

No other dependencies at this time.

## Example Playbook

```yaml
---
- name: Kafka Lag Exporter Install/Config
  hosts: kafka_lag_exporter
  gather_facts: true
  tasks:
  - name: Install Java
    import_role: 
      name: java
  - name: Install/Config
    import_role: 
      name: kafka-lag-exporter-ansible
```


## License

MIT

## Author Information

Nikoleta Verbeck | Github/@nerdynick