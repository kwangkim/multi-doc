# Centralized Log Management
## Logstash
* gather log data from the network and store it in ElasticSearch
* Apache v2 License
* now part of ElasticSearch
* internally use Kibana in general
* input, output, filter (CSV filter)
* works: puts the events log data into one ElasticSearch index per day

## Kibana
* powerful GUI **dashboard** to visualize logs and time-stamped data in realtime
* a user friendly way to view, search and visualize the log data
* works: retrieves relevant log datas from ElasticSearch using a set of configured queries and facets and show them

## ElasticSearch
* a powerful open source search and analytics engine that makes data easy to explore

# vs
## Graylog2
* gather log data from the network and store it in ElasticSearch

## Fluentd
* vs. Logstash

## splunk
* indexes and makes searchable data from any app, server or network device in real time including logs, config files, messages, alerts, scripts and metrics.