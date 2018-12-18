Logstash
=========

Logstash installation and configuration role for Elasticsearch cluster.

Requirements
------------

None

Role Variables
--------------

    pipeline_configuration: <list of pipeline configurations>
      - name: <pipeline name - retains only alphanumeric chars and underscore>
        input:
          type: <list of inputs (dictionaries)>
        filter:
          __if: <an 'if' clause - uses a string predicate (at toplevel or element level)>
          type: <list filters (dictionaries)>
        output:
          type:
            - __if: <an 'if' clause - block level predicate string>
              <output>:
                <setting>

Dependencies
------------

common/elk/base

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
