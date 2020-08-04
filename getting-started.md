---

copyright:
  years: 2015, 2020
lastupdated: "2020-08-04"

keywords: tone analyzer, getting started, tutorial

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
{:go: .ph data-hd-programlang='go'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}
{:download: .download}
{:apikey: data-credential-placeholder='apikey'}
{:url: data-credential-placeholder='url'}
{:hide-dashboard: .hide-dashboard}

# Getting started with {{site.data.keyword.toneanalyzershort}}
{: #gettingStarted}

The {{site.data.keyword.toneanalyzershort}} service analyzes the tone of input content. This tutorial shows commands that analyze different sample content. The examples demonstrate both the general-purpose and the customer-engagement endpoints.
{: shortdesc}

## Before you begin
{: #prerequisites}

- {: hide-dashboard}  Create an instance of the service:
    1.  {: hide-dashboard} Go to the [{{site.data.keyword.toneanalyzershort}}](https://{DomainName}/catalog/services/tone-analyzer){: external} page in the {{site.data.keyword.cloud_notm}} Catalog.
    1.  {: hide-dashboard} Sign up for a free {{site.data.keyword.cloud_notm}} account or log in.
    1.  {: hide-dashboard} Click **Create**.
-   Copy the credentials to authenticate to your service instance:
    1.  {: hide-dashboard} From the [{{site.data.keyword.cloud_notm}} dashboard](https://{DomainName}/resources){: external}, click on your {{site.data.keyword.toneanalyzershort}} service instance to go to the {{site.data.keyword.toneanalyzershort}} service dashboard page.
    1.  On the **Manage** page, click **Show Credentials** to view your credentials.
    1.  Copy the `API Key` and `URL` values.

### Using the curl examples
{: #getting-started-curl}

This tutorial uses the `curl` command to call methods of the service's HTTP interface. Make sure that you have the `curl` command installed on your system.

1.  To test whether `curl` is installed, run the following command on the command line. If the output lists the `curl` version that supports Secure Sockets Layer (SSL), you are set for the tutorial.

    ```bash
    curl -V
    ```
    {: pre}

1.  If necessary, install the version of `curl` with SSL enabled for your operating system from [curl.haxx.se](https://curl.haxx.se/){: external}.

Omit the braces from the examples. They indicate variable values.
{: tip}

## Step 1: Using the general-purpose endpoint via the POST request method
{: #generalPurposePost}

The following commands call the `POST /v3/tone` method to analyze the contents of the file `tone.json`. The file includes a single paragraph of plain text that is written by one person. The examples demonstrate the method's `sentences` query parameters.

1.  Download the sample file <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/tone-analyzer/tone.json" download="tone.json">tone.json <img src="../icons/launch-glyph.svg" alt="External link icon" title="External link icon"></a>.
1.  Issue the following command to analyze the tone of the overall content and of each individual sentence.
    -   {: hide-dashboard} Replace `{apikey}` and `{url}` with your information.
    -   Modify `{path_to_file}` to specify the location of the `tone.json` file.

    ```bash
    curl -X POST -u "apikey:{apikey}"{: apikey} \
    --header "Content-Type: application/json" \
    --data-binary @{path_to_file}tone.json \
    "{url}/v3/tone?version=2017-09-21"{: url}
    ```
    {: pre}

1.  Issue the following command to analyze the tone of the overall content only by setting the `sentences` parameter to `false`.

    ```bash
    curl -X POST -u "apikey:{apikey}"{: apikey} \
    --header "Content-Type: application/json" \
    --data-binary @{path_to_file}tone.json \
    "{url}/v3/tone?version=2017-09-21&sentences=false"{: url}
    ```
    {: pre}

For an example of the method's output, see [Example response](/docs/tone-analyzer?topic=tone-analyzer-utgpe#exampleResponse-tone).

## Step 2: Using the general-purpose endpoint via the GET request method
{: #generalPurposeGet}

The interface also offers a `GET /v3/tone` method. The `GET` method provides the same functionality and produces the same results as the `POST` method, but you use the method's `text` query parameter to specify the content to be analyzed. The method accepts only plain text input.

1.  The following example specifies the text of the file `tone.json` via the `text` parameter; as shown, you must URL-encode the text. The command omits the `sentences` parameter, so it returns the same output as the first `POST` example shown previously. (The example includes line breaks for readability; do not include them in an actual command.)

    ```bash
    curl -X GET -u "apikey:{apikey}"{: apikey} \
    "{url}/v3/tone?version=2017-09-21&text=Team%2C%20I%20know%20that%20times%20are%20tough%21%20Product%20sales%20have%20been%20disappointing%20for%20the%20past%20three%20quarters.%20We%20have%20a%20competitive%20product%2C%20but%20we%20need%20to%20do%20a%20better%20job%20of%20selling%20it%21"{: url}
    ```
    {: pre}

## Step 3: Using the customer-engagement endpoint
{: #customerEngagement}

The following command calls the `POST /v3/tone_chat` method to analyze the contents of the file `tone-chat.json`. The file includes a brief exchange of messages between two people, a <code>customer</code> and an <code>agent</code>.

1.  Download the sample file <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/tone-analyzer/tone-chat.json" download="tone-chat.json">tone-chat.json <img src="../icons/launch-glyph.svg" alt="External link icon" title="External link icon"></a>.
1.  Issue the following command to analyze the tone of the exchange in the sample file.

    ```bash
    curl -X POST -u "apikey:{apikey}"{: apikey} \
    --header "Content-Type: application/json" \
    --data-binary @{path_to_file}tone-chat.json \
    "{url}/v3/tone_chat?version=2017-09-21"{: url}
    ```
    {: pre}

The service's response indicates the most prevalent tones that are detected for each utterance of the input. To view the content of the response for this request, see [Example response](/docs/tone-analyzer?topic=tone-analyzer-utco#exampleResponse-tone-chat).

## Next steps
{: #gsns}

-   For more information about the `/v3/tone` method, see [Using the general-purpose endpoint](/docs/tone-analyzer?topic=tone-analyzer-utgpe).
-   For more information about the `/v3/tone_chat` method, see [Using the customer-engagement endpoint](/docs/tone-analyzer?topic=tone-analyzer-utco).
-   For more information about the methods of the service's interface, see the [API reference](https://{DomainName}/apidocs/tone-analyzer){: external}.
