---

copyright:
  years: 2019
lastupdated: "2019-03-19"

subcollection: tone-analyzer

---

{:shortdesc: .shortdesc}
{:external: target="_blank" .external}
{:tip: .tip}
{:important: .important}
{:note: .note}
{:deprecated: .deprecated}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}

# High availability and disaster recovery
{: #ha-dr}

The {{site.data.keyword.toneanalyzerfull}} service is highly available within any {{site.data.keyword.cloud_notm}} location. It has no backup and restore requirements for disaster recovery.
{: shortdesc}

## High availability
{: #high-availability}

The {{site.data.keyword.toneanalyzershort}} service is highly available with no single point of failure within any {{site.data.keyword.cloud_notm}} location (for example, Dallas or Washington, DC). The service achieves high availability automatically and transparently by means of the multi-zone region (MZR) feature provided by {{site.data.keyword.cloud_notm}}.

{{site.data.keyword.cloud_notm}} enables multiple zones that do not share a single point of failure within a single location. It also provides automatic load balancing across the zones within a region.

## Disaster recovery
{: #disaster-recovery}

The {{site.data.keyword.toneanalyzershort}} service is stateless. It stores no user data on {{site.data.keyword.cloud_notm}}. In the event of a catastrophic failure in a region, complete the following steps:

1.  Create a new instance of the {{site.data.keyword.toneanalyzershort}} service in a different region.
1.  Modify your application to use the URL and credentials for the new service instance.
