Filebeat
=========

Install Elastic Stack Beat (filebeat).

Requirements
------------

None

Role Variables
--------------

filebeat_configuration: <the entire yaml configuration to be stored in the filebeat configuration file>

Dependencies
------------

None

Example Playbook
----------------

    - hosts: agents
      roles:
       - role: elk/beats/filebeat
         vars:
           filebeat_configuration:
             filebeat:
               inputs:
               - host: localhost:11999
                 type: tcp
             output:
               logstash:
                 hosts: logstash:5959

License
-------

MIT

Author Information
------------------

Tibor Csoka
