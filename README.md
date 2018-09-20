# graylog2-zabbix
Basic Zabbix monitoring for Graylog2 Server

### Master branch - Graylog 2.4 and up

Tested on Zabbix 3.4.11 and Graylog 2.4.6.

For specific Elasticsearch monitoring, please head over to Elastizabbix (https://github.com/mkhpalm/elastizabbix)

## Requirements
  * jq (https://github.com/stedolan/jq) 1.3+
  * curl

The script has been tested on Ubuntu 14.04 & Debian 9. Graylog should be running behind a reverse proxy like nginx with HTTPS support.

This doesn't require anything on the agent. It is an external script curl'ing to the Graylog2 API.

Please note, if running by hand, that the `poll_data` item has to be run first.

## How to install
  * Create a Graylog2 user with the "reader" role
  * Copy the script to your Zabbix's _externalscripts_ directory.
  * Make sure the file's permissions are adequate.
  * Import the XML template into Zabbix.
  * Assign the template to the corresponding Graylog server and update macros with the right values.

## Usage

Note: in order to use `api/system/deflector` (_Current deflector_ item) a user must have _Admin_ right. It is disabled in the template by default.

```
check_graylog_node -H <HOSTNAME> -U <USERNAME> -P <PASSWORD> -a <ATTRIBUTE> [-p <GRAYLOG_API_PORT>] [-s <PROTOCOL>] [-h] [-d]

Args:
    -H : Hostname or IP address of graylog server
    -U : Username
    -P : Password
    -a : Attribute to monitor. See list below.
    -p : Graylog API port (default: 9000)
    -s : Protocol: HTTP or HTTPS (default: HTTPS)
    -d : Debug message to log file (default: false)
    -h : Displays help

List of attributes:
    - node_id : returns graylog node_id
    - node_transport
    - node_is_master
    - node_cluster
    - node_type
    - node_throughput
    - lb_status
    - total_message_count
    - es_cluster_health
    - journal_size
    - journal_num_segments
    - journal_uncommitted_entries
    - journal_events_read
    - journal_events_append
    - buffer_input_utilization
    - buffer_output_utilization
    - buffer_input_utilization_percent
    - buffer_output_utilization_percent
    - poll_data
    - current_deflector (not yet supported, because not accessible via regular user)
    - system_lifecycle
    - system_isprocessing
    - system_tz
    - system_version
    - system_startedat
    - cluster_stream_count
    - cluster_stream_rule_count
    - cluster_user_count
    - cluster_output_count
    - cluster_dashboard_count
    - cluster_input_count
    - cluster_global_input_count
    - cluster_extractor_count
    - cluster_contentpack_count
    - cluster_alerts_count
    - warning_five_minute
    - error_five_minute
    - fatal_five_minute
```
