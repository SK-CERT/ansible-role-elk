Role Name
=========

Install Elastic Beats - lightweight data shippers for Elasticsearch.

Requirements
------------

None

Role Variables
--------------

filebeat:
  port: "12000"
  config_path: "/etc/filebeat/"

logstash:
  host: "localhost"
  port: "5044"

Dependencies
------------

None

Example Playbook
----------------

Information about local filebeat TCP output port, destination logstash host and port are necessary.

    - hosts: clients
      roles:
       - role: elk/beats/filebeat
         vars:
           logstash:
             host: "192.168.1.5"
             port = "13568"

License
-------

MIT

Author Information
------------------

Tibor Csoka
