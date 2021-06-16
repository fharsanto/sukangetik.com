---
title: "Choosing the right Central Log Management (CLM)"
date: 2021-02-15T22:10:45+07:00
# draft: true
categories: monitoring
tags: ["operational", "monitoring", "opensource", "cloud"]
Description: Concern before choosing tools for monitoring your stack / product

---

## Purpose
A type of logging solution system that consolidates all of your log data and pushes to one central, accessible and easy-to-use interface. Centralize logging is designed to make your life easier. Not only does CLM provide multiple features that allow you to easily collect log information, but it also helps you consolidate, analyze, and view that information quickly and clearly. CLM gives you tons of capabilities including:
* Storing log data from multiple sources in a central location
* Enforcing retention policies on your logs so they are available for a specific time period
* Easily searching inside the logs for important information
* Generating alerts based on metrics you define on the logs
* Sharing your dashboard and log information with others simply and quickly
* Low costs and increased storage and backup for historical data
* Setting up security alerts and granting login access to particular users without granting server root access

## The Options
For this things, we scoring based on

### [Graylog](https://www.graylog.org)
Graylog is a leading centralized log management solution built to open standards for capturing, storing, and enabling real-time analysis of terabytes of machine data. We deliver a better user experience by making analysis ridiculously fast and efficient using a more cost-effective and flexible architecture.

![Minimum Setup](https://docs.graylog.org/en/4.0/_images/architec_small_setup.png)
*Minimum Setup*

![Bigger Production Setup](https://docs.graylog.org/en/4.0/_images/architec_bigger_setup.png)
*Bigger Production Setup*

|                  | Details                     |
|------------------|-----------------------------|
| Licence Type     | Open Source with [Enterprise](https://www.graylog.org/products/open-source-vs-enterprise) |
| Language         | Java ( >= 8 )               |
| Components       | Elasticsearch (6.x or 7.x)<br />MongoDB (4.0 or 4.2) |
| OS Packages      | Ubuntu, Debian, RHEL/CentOS, SLES |
| Containers       | [Docker](https://docs.graylog.org/en/4.0/pages/installation/docker.html#here) |
| Data Formats     | Syslog (TCP, UDP, AMQP, Kafka)<br />GELF(TCP, UDP, AMQP, Kafka, HTTP)<br />AWS - AWS Logs, FlowLogs, CloudTrail<br />[Beats/Logstash](https://www.elastic.co/guide/en/beats/libbeat/current/community-beats.html)<br />CEF (TCP, UDP, AMQP, Kafka)<br />JSON Path from HTTP API<br />Netflow (UDP)<br />Plain/Raw Text (TCP, UDP, AMQP, Kafka) |
| Data Transport   | Apache Kafka, RabbitMQ, REST API |

**Advantages**
* Quick Setup
* Authentication / Authorization included
* Parsing, Alerting, Archiving

**Challenges**
* Graph / Dashboard is basic
* Fewer plugins available

### [Elastic Stack](https://www.elastic.co/what-is/elk-stack)
`ELK` is the acronym for three open source projects: Elasticsearch, Logstash, and Kibana. Elasticsearch is a search and analytics engine. Logstash is a server‑side data processing pipeline that ingests data from multiple sources simultaneously, transforms it, and then sends it to a `stash` like Elasticsearch. Kibana lets users visualize data with charts and graphs in Elasticsearch.

The Elastic Stack is the next evolution of the ELK Stack.

![Standard Setup](https://www.elastic.co/guide/en/logstash/current/static/images/deploy2.png)
*Standard Setup*

![Additional Popular Setup](https://www.elastic.co/guide/en/logstash/current/static/images/deploy3.png)
*Additional Popular Setup*

|                  | Details                     |
|------------------|-----------------------------|
| Licence Type     | Open Source with [Subscription](https://www.elastic.co/subscriptions) option or using [Elastic Cloud](https://www.elastic.co/pricing/) |
| Language         | Java ( >= 8 )               |
| Components       | Elasticsearch<br />Kibana<br />Logstash<br />Security |
| OS Packages      | Ubuntu, Debian, RHEL/CentOS, SLES, Windows, MacOS |
| Containers       | [Docker](https://www.elastic.co/guide/en/elasticsearch/reference/7.11/docker.html) |
| Data Formats     | [Dozen of input Supported](https://www.elastic.co/guide/en/logstash/current/input-plugins.html) |
| Data Transport   | REST API |

**Advantages**
* Starting version 7.11 Security (Authentication / Authorization) is free
* Parsing, Alerting, Archiving
* Graph / Dashboard is amazing
* Many plugins available

**Challenges**
* Medium Complex to setup
* Elastic Stack need big resource, like Elasticsearch it's must have min 3 nodes.
* Logstash resource usage is heavy

### [Splunk](https://www.splunk.com/)
A scalable and reliable data platform for investigating, monitoring, analyzing and acting on your data.

|                  | Details                     |
|------------------|-----------------------------|
| Licence Type     | Free for 500MB data per day<br />[Splunk Cloud](https://www.splunk.com/en_us/software/pricing/enterprise-and-cloud.html)<br />Splunk Enterprise start $2700/year<br />Splunk Data Stream Processor |
| Language         | Java, C++, Python           |
| Components       | Splunk Server<br />Splunk Forwarder|
| OS Packages      | All Linux, FreeBSD 11, Solaris 11, AIX, MacOS |
| Containers       | [Docker](https://docs.splunk.com/Documentation/Splunk/8.1.2/Installation/Beforeyouinstall) |
| Data Formats     | [Dozen of input Supported](https://docs.splunk.com/Documentation/Splunk/8.1.2/Data/WhatSplunkcanmonitor) |
| Data Transport   | [Multiple](https://docs.splunk.com/Documentation/Splunk/latest/Data/Monitornetworkports) |

**Advantages**
* Fantastic querying data feature
* Can ingest and chart ANYTHING thrown at it. It’s magical
* Machine learning plugins available
* Thousand plugins available

**Challenges**
* Expensive
* Searching billion data can be [slow](https://community.splunk.com/t5/Monitoring-Splunk/Splunk-searches-are-becoming-very-slow/m-p/171690), must have some tunning
