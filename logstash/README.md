Logstash
=========

Logstash installation and configuration role for Elasticsearch cluster.

Requirements
------------

None

Role Variables
--------------

    elastic:
      host: "127.0.0.1"
      port: "9200"
      index: "%{[@metadata][beat]}-%{[@metadata][version]}-%{+YYYY.MM.dd}"

    logstash:
      port: "5044"
      config_path: "/etc/logstash/conf.d/"

    codec: "json"

Dependencies
------------

Example Playbook
----------------

    - hosts: servers
      roles:
        - role: elk/logstash
          vars:
            plugins:
              - logstash-filter-fingerprint
            pipelines:
              - name: Random index pipeline 1
                input: |
                  beats {
                    port => 32333
                  }

                filter: |
                  date {
                    match => '[ "timestamp", "yyyy-MM-dd HH:mm:ss,SSS" ]'
                  }

                output: |
                  elasticsearch {
                    hosts => ['localhost:9200']
                    index => '%{[@metadata][index_name]}-%{[@metadata][index_date]}'
                    action => 'update'
                    doc_as_upsert => true
                    document_id => '%{[@metadata][fingerprint]}'
                  }

License
-------

GPLv3

Author Information
------------------

Tibor Csoka
