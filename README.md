# ansible-role-packetbeat

Tested on Ansible 2.4.2 and Ubuntu 16.04

This role has some configuration options and can send logs to logstash only (now).

So please refer packetbeat.yml.j2 template file for the details.

Referenced by a
[Configuring Packetbeat](https://www.elastic.co/guide/en/beats/packetbeat/current/configuring-howto-packetbeat.html) document.

## Playbook sample
This sample playbook installs Packetbeat.

* **packetbeat_protocols** : This list value should have two keys (type, ports) and appropriate values.
* **out_logstash.host** : The ip of logstash host to send collected data by packetbeat
* **out_logstash.port** : The port of logstash service
* **packetbeat_loglevel (optional)** : The logging level for packetbeat. Default value is info
* **packetbeat_name (optional)** : The name of packetbeat to be installed. Default is the host ip where packetbeat will be installed
* **packetbeat_version (optional)** : Default value is 6.x. If you'd like to install packetbeat 5.x, you should set this value to 5.x.

```yaml
- hosts: test_host
  become: yes
  roles:
    - role: packetbeat
      packetbeat_name: test_packetbeat
      packetbeat_protocols:
        - { type: tls, ports: [443] }
      packetbeat_loglevel: debug
      out_logstash:
        host: '{{ hostvars["elk_test"].ansible_host }}'
        port: 5044
```
