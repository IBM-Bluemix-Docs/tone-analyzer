---

copyright:
  years: 2015, 2020
lastupdated: "2020-10-16"

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

# Overview for developers
{: #overviewDevelopers}

You can access the capabilities of the {{site.data.keyword.toneanalyzershort}} service via an HTTP Representational State Transfer (REST) API. Several Software Development Kits (SDKs) are also available to simplify application development in various languages. The following sections provide an overview of application development with the service.
{: shortdesc}

## Programming with the service
{: #programming}

To analyze the tone of an individual's text, you pass the input text to the service via the `GET` or `POST /v3/tone` method. To analyze the exchanges in a conversation, you pass input to the service via the `POST /v3/tone_chat` method. In both cases, the service returns its analysis in JSON format. For more information, see

-   [Using the general-purpose endpoint](/docs/tone-analyzer?topic=tone-analyzer-utgpe)
-   [Using the customer-engagement endpoint](/docs/tone-analyzer?topic=tone-analyzer-utco)

## Using Software Development Kits
{: #sdks}

SDKs are available for the {{site.data.keyword.toneanalyzershort}} service to simplify application development. {{site.data.keyword.ibmwatson}} SDKs are available for many popular programming languages and platforms.

-   For a complete list of SDKs and links to the SDKs on GitHub, see [Using SDKs](/docs/tone-analyzer?topic=watson-using-sdks).
-   For detailed information about all methods of the Node, Java, Python, Ruby, and Go SDKs for the {{site.data.keyword.toneanalyzershort}} service, see the [API & SDK reference](https://{DomainName}/apidocs/tone-analyzer){: external}.

## Learning more about application development
{: #learn}

For more information about working with {{site.data.keyword.watson}} services and {{site.data.keyword.cloud}}, see the following pages:

-   For an introduction to working with {{site.data.keyword.watson}} services and {{site.data.keyword.cloud_notm}}, see [Getting started with {{site.data.keyword.watson}} and {{site.data.keyword.cloud_notm}}](/docs/watson?topic=watson-about).
-   All service instances use {{site.data.keyword.cloud_notm}} Identity and Access Management (IAM) for authentication. For more information, see [Authenticating to Watson services](/docs/watson?topic=watson-iam).
-   Request logging is disabled for the {{site.data.keyword.toneanalyzershort}} service. The service does not log or retain data from requests and responses, regardless of whether the `X-Watson-Learning-Opt-Out` request header is set.
