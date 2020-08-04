---

copyright:
  years: 2015, 2020
lastupdated: "2020-08-04"

subcollection: tone-analyzer

---

{:help: data-hd-content-type='help'}
{:troubleshoot: data-hd-content-type='troubleshoot'}
{:support: data-reuse='support'}
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

# Using the general-purpose endpoint
{: #utgpe}

The {{site.data.keyword.toneanalyzershort}} general-purpose endpoint analyzes the tone of written communications, from short email messages to longer documents. It can help you understand the emotional and language tones of your communications. For more information about the interface, including the Node.js, Java, and Python SDKs that are available for calling the service, see the [API reference](https://{DomainName}/apidocs/tone-analyzer){: external}.
{: shortdesc}

Request logging is disabled for the {{site.data.keyword.toneanalyzershort}} service. Regardless of whether you set the `X-Watson-Learning-Opt-Out` request header, the service does not log or retain data from requests and responses.
{: note}

## Requesting a tone analysis
{: #request-tone}

To analyze tone with the general-purpose endpoint, you call one of the two versions of the service's `tone` method:

-   The `POST /v3/tone` method accepts input content in JSON, plain text, or HTML format via the required body of the request. Use this version of the method for longer text or for text that you do not want to expose on the URL.
-   The `GET /v3/tone` method accepts input content via its required `text` query parameter. Use this version of the method for simple text that is easily accommodated on the URL.

The methods accept the following parameters.

<table>
  <caption>Table 1. Parameters of the <code>/v3/tone</code> methods</caption>
  <tr>
    <th style="text-align:left; width:20%">Parameter</th>
    <th style="text-align:center; width:12%">Type</th>
    <th style="text-align:center; width:20%">Data type</th>
    <th style="text-align:left">Description</th>
  </tr>
  <tr>
    <td><code>Body</code><br/><em>Required for <code>POST</code></em></td>
    <td style="text-align:center">Body</td>
    <td style="text-align:center">JSON object | String</td>
    <td>
      JSON, plain text, or HTML input that contains the content to
      be analyzed. For JSON input, provide an object of type
      <code>ToneInput</code>. For more information, see
      [Specifying JSON input](#JSONinput). <em>Not supported for
      <code>GET</code> requests.</em>
    </td>
  </tr>
  <tr>
    <td><code>text</code><br/><em>Required for <code>GET</code></em></td>
    <td style="text-align:center">Query</td>
    <td style="text-align:center">String</td>
    <td>
      Plain text input that contains the content to be analyzed. You must
      URL-encode the input. <em>Not supported for <code>POST</code>
        requests.</em>
    </td>
  </tr>
  <tr>
    <td><code>Content-Type</code><br/><em>Required for <code>POST</code></em></td>
    <td style="text-align:center">Header</td>
    <td style="text-align:center">String</td>
    <td>
      The content type of the request.
      <ul style="margin:0px 0px 0px 20px; padding:0px">
        <li style="margin:0px; padding:0px">
          <code>text/plain</code> for plain text
        </li>
        <li style="margin:0px; padding:0px">
            <code>text/html</code> for text in HTML (the service removes
            HTML tags and analyzes only the textual content)
        </li>
        <li style="margin:0px; padding:0px">
          <code>application/json</code> for text in JSON format
        </li>
      </ul>
    <em>Omit for <code>GET</code> requests.</em>
    </td>
  </tr>
  <tr>
    <td><code>version</code><br/><em>Required</em></td>
    <td style="text-align:center">Query</td>
    <td style="text-align:center">String</td>
    <td>
      The version of the API that you want to use as a date in the format
      <code>YYYY-MM-DD</code>; for example, specify <code>2017-09-21</code>
      for September 21, 2017 (the latest version). For more information about
      all available versions, see the
      [Release notes](/docs/tone-analyzer?topic=tone-analyzer-rnrn).
    </td>
  </tr>
  <tr>
    <td><code>Content-Language</code><br/><em>Optional</em></td>
    <td style="text-align:center">Header</td>
    <td style="text-align:center">String</td>
    <td>
      The language of the input content.
      <ul style="margin:0px 0px 0px 20px; padding:0px">
        <li style="margin:0px; padding:0px">
          <code>en</code> (English, the default)
        </li>
        <li style="margin:0px; padding:0px">
          <code>fr</code> (French)
        </li>
      </ul>
      Regional variants are treated as their parent language; for example,
      <code>en-US</code> is interpreted as <code>en</code>. The input
      content must match the specified language. Do not submit content
      that contains both languages. You can use different languages for
      the input and response.
    </td>
  </tr>
  <tr>
    <td><code>Accept-Language</code><br/><em>Optional</em></td>
    <td style="text-align:center">Header</td>
    <td style="text-align:center">String</td>
    <td>
      The requested language of the response.
      <ul style="margin:0px 0px 0px 20px; padding:0px">
        <li style="margin:0px; padding:0px">
          <code>ar</code> (Arabic)
        </li>
        <li style="margin:0px; padding:0px">
          <code>de</code> (German)
        </li>
        <li style="margin:0px; padding:0px">
          <code>en</code> (English, the default)
        </li>
        <li style="margin:0px; padding:0px">
          <code>es</code> (Spanish)
        </li>
        <li style="margin:0px; padding:0px">
          <code>fr</code> (French)
        </li>
        <li style="margin:0px; padding:0px">
          <code>it</code> (Italian)
        </li>
        <li style="margin:0px; padding:0px">
          <code>ja</code> (Japanese)
        </li>
        <li style="margin:0px; padding:0px">
          <code>ko</code> (Korean)
        </li>
        <li style="margin:0px; padding:0px">
          <code>pt-br</code> (Brazilian Portuguese)
        </li>
        <li style="margin:0px; padding:0px">
          <code>zh-cn</code> (Simplified Chinese)
        </li>
        <li style="margin:0px; padding:0px">
          <code>zh-tw</code> (Traditional Chinese)
        </li>
      </ul>
      For two-character arguments, regional variants are treated as their
      parent language; for example, <code>en-US</code> is interpreted as
      <code>en</code>. You can use different languages for the input and
      response.
    </td>
  </tr>
  <tr>
    <td><code>sentences</code><br/><em>Optional</em></td>
    <td style="text-align:center">Query</td>
    <td style="text-align:center">Boolean</td>
    <td>
      Indicates whether the service is to return an analysis of each
      individual sentence in addition to its analysis of the full document.
      If <code>true</code> (the default), the service returns results for
      each sentence.
    </td>
  </tr>
</table>

Submit no more than 128 KB of total input content and no more than 1000 individual sentences. The service analyzes the first 1000 sentences for document-level analysis and only the first 100 sentences for sentence-level analysis. It returns a `warning` field as part of its response if you exceed either limit; the request still succeeds with HTTP response code 200.

### Example requests
{: #exampleRequests}
{: help}
{: support}

The following example `curl` command uses the HTTP `POST` request method to call the general-purpose endpoint with the input file <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/tone-analyzer/tone.json" download="tone.json">tone.json <img src="../icons/launch-glyph.svg" alt="External link icon" title="External link icon"></a> and a version of `2017-09-21`. The example requests an analysis for both the full document and the individual sentences.

```bash
curl -X POST -u "apikey:{apikey}" \
--header "Content-Type: application/json" \
--data-binary @./tone.json \
"{url}/v3/tone?version=2017-09-21"
```
{: pre}

The following example command is equivalent to the previous example but uses the HTTP `GET` request method:

```bash
curl -X GET -u "apikey:{apikey}" \
"{url}/v3/tone?version=2017-09-21&text=Team%2C%20I%20know%20that%20times%20are%20tough%21%20Product%20sales%20have%20been%20disappointing%20for%20the%20past%20three%20quarters.%20We%20have%20a%20competitive%20product%2C%20but%20we%20need%20to%20do%20a%20better%20job%20of%20selling%20it%21"
```
{: pre}

For more examples, see the [Getting started tutorial](/docs/tone-analyzer?topic=tone-analyzer-gettingStarted).

### Specifying the character set
{: #charset}
{: troubleshoot}
{: support}

By default, the service uses the following character sets for input content:

-   *For plain text and HTML content,* the service uses the International Standards Organization (ISO)-8859-1 character set (effectively the ASCII character set) per the HTTP version 1.1 specification.
-   *For JSON content,* the service effectively always uses the Unicode Transformation Format (UTF)-8 character set per Section 8.1 of the International Engineering Task Force (IETF) [Request for Comment (RFC) 7159](https://tools.ietf.org/html/rfc7159#section-8.1){: external}.

When submitting plain text or HTML content, include the `charset` parameter with the `Content-Type` header to indicate the character encoding of the input text. The following example specifies UTF-8 character encoding for plain text input:

```
Content-Type: text/plain;charset=utf-8
```
{: codeblock}

By using the `charset` parameter, you can avoid potential problems that are associated with non-ASCII or non-printable characters. If you pass UTF-8 data without specifying the character set, special characters can result in incorrect results or in HTTP 400- or 500-level errors.

To prevent similar errors when using the `curl` command, always pass the content via the `--data-binary` option of the `curl` command to preserve any UTF-8 encoding for the content. If you use the `--data` option to pass the content as ASCII, the command can process the input, which can cause problems for data encoded in UTF-8.

## Specifying JSON input
{: #JSONinput}
{: help}
{: support}

To analyze JSON input with the `POST` request method, you pass the method a JSON `ToneInput` object with the following simple format:

```javascript
{
  "text": ""
}
```
{: codeblock}

The following example shows the contents of the <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/tone-analyzer/tone.json" download="tone.json">tone.json <img src="../icons/launch-glyph.svg" alt="External link icon" title="External link icon"></a> file that is used with the examples in the [Getting started tutorial](/docs/tone-analyzer?topic=tone-analyzer-gettingStarted). The file includes a single paragraph of text that is written by one person. (The following text includes line breaks for readability; do not include them in actual input.)

```javascript
{
  "text": "Team, I know that times are tough! Product sales have been
  disappointing for the past three quarters. We have a competitive
  product, but we need to do a better job of selling it!"
}
```
{: codeblock}

## JSON response content
{: #JSONresponse-tone}

The service returns a JSON `ToneAnalysis` object that always contains a `document_tone` field. This field contains a `DocumentAnalysis` object that provides the analysis of the full input document. It contains a single field, `tones`, that provides the results of the analysis for each qualifying tone of the document.

If the `sentences` parameter of the request is omitted or set to `true`, the response also includes a `sentences_tone` field. This field contains an array of `SentenceAnalysis` objects, each of which provides the following information for a different sentence from the input content:

-   `sentence_id` (integer) provides the unique identifier for the sentence. The first sentence has ID 0, and the ID of each subsequent sentence is incremented by one.
-   `text` (string) provides the text of the sentence.
-   `tones` provides the results of the analysis for each qualifying tone of the sentence.

The following example shows the high-level structure of the `ToneAnalysis` object:

```javascript
{
  "document_tone": {
    "tones": [
      . . .
    ]
  },
  "sentences_tone": [
    {
      "sentence_id": {integer},
      "text": "{string}",
      "tones": [
        . . .
      ]
    },
    . . .
  ]
}
```
{: codeblock}

### Tone and score results
{: #uttsr}

The `tones` fields that are returned for both document- and sentence-level analyses contain an array of `ToneScore` objects that provides results for the dominant tones. Such tones have scores of at least 0.5. The array is empty if no tone has a score that meets this threshold. Each `ToneScore` object provides the following information about a qualifying tone:

-   `score` (double) is the score for the tone in the range of 0.5 to 1. A score greater than 0.75 indicates a high likelihood that the tone is perceived in the content.
-   `tone_id` (string) is the unique, non-localized identifier of the tone; for descriptions of the tones, see [General-purpose tones](#tones-tone).
-   `tone_name` (string) is the user-visible, localized name of the tone.

The following example shows the structure of the `ToneScore` object:

```javascript
{
  "tones": [
    {
      "score": {double},
      "tone_id": "{string}",
      "tone_name": "{string}"
    },
    . . .
  ]
}
```
{: codeblock}

### Example response
{: #exampleResponse-tone}

The following output is returned for the [Example requests](#exampleRequests). (The same output is returned for the first example in the [Getting started tutorial](/docs/tone-analyzer?topic=tone-analyzer-gettingStarted).) The response includes results for the full document and for each individual sentence. All reported tones have a score of at least 0.5. Tones with a score of at least 0.75 are likely to be perceived in the content.

```javascript
{
  "document_tone": {
    "tones": [
      {
        "score": 0.6165,
        "tone_id": "sadness",
        "tone_name": "Sadness"
      },
      {
        "score": 0.829888,
        "tone_id": "analytical",
        "tone_name": "Analytical"
      }
    ]
  },
  "sentences_tone": [
    {
      "sentence_id": 0,
      "text": "Team, I know that times are tough!",
      "tones": [
        {
          "score": 0.801827,
          "tone_id": "analytical",
          "tone_name": "Analytical"
        }
      ]
    },
    {
      "sentence_id": 1,
      "text": "Product sales have been disappointing for the past three quarters.",
      "tones": [
        {
          "score": 0.771241,
          "tone_id": "sadness",
          "tone_name": "Sadness"
        },
        {
          "score": 0.687768,
          "tone_id": "analytical",
          "tone_name": "Analytical"
        }
      ]
    },
    {
      "sentence_id": 2,
      "text": "We have a competitive product, but we need to do a better job of selling it!",
      "tones": [
        {
          "score": 0.506763,
          "tone_id": "analytical",
          "tone_name": "Analytical"
        }
      ]
    }
  ]
}
```
{: codeblock}

## General-purpose tones
{: #tones-tone}
{: help}
{: support}

The following table describes the general-purpose tones that the service can return. A tone whose score is less than 0.5 is omitted, indicating that the emotion is unlikely to be perceived in the content. A score greater than 0.75 indicates a high likelihood that the tone is perceived.

<table>
  <caption>Table 2. General-purpose tones</caption>
  <tr>
    <th style="text-align:left; vertical-align:bottom; width:20%">Tone / ID</th>
    <th style="text-align:left">Description</th>
  </tr>
  <tr>
    <td>Anger<br/><code>anger</code></td>
    <td>
      Anger is evoked due to injustice, conflict, humiliation, negligence,
      or betrayal. If anger is active, the individual attacks the target,
      verbally or physically. If anger is passive, the person silently
      sulks and feels tension and hostility. (An emotional tone.)
    </td>
  </tr>
  <tr>
    <td>Fear<br/><code>fear</code></td>
    <td>
      Fear is a response to impending danger. It is a survival mechanism that
      is triggered as a reaction to some negative stimulus. Fear can be a mild
      caution or an extreme phobia. (An emotional tone.)
    </td>
  </tr>
  <tr>
    <td>Joy<br/><code>joy</code></td>
    <td>
      Joy (or happiness) has shades of enjoyment, satisfaction, and pleasure.
      Joy brings a sense of well-being, inner peace, love, safety, and
      contentment. (An emotional tone.)
    </td>
  </tr>
  <tr>
    <td>Sadness<br/><code>sadness</code></td>
    <td>
      Sadness indicates a feeling of loss and disadvantage. When a person is
      quiet, less energetic, and withdrawn, it can be inferred that they feel
      sadness. (An emotional tone.)
    </td>
  </tr>
  <tr>
    <td>Analytical<br/><code>analytical</code></td>
    <td>
      An analytical tone indicates a person's reasoning and analytical attitude
      about things. An analytical person might be perceived as intellectual,
      rational, systematic, emotionless, or impersonal. (A language tone.)
    </td>
  </tr>
  <tr>
    <td>Confident<br/><code>confident</code></td>
    <td>
      A confident tone indicates a person's degree of certainty. A confident
      person might be perceived as assured, collected, hopeful, or egotistical.
      (A language tone.)
    </td>
  </tr>
  <tr>
    <td>Tentative<br/><code>tentative</code></td>
    <td>
      A tentative tone indicates a person's degree of inhibition. A tentative
      person might be perceived as questionable, doubtful, or debatable. (A
      language tone.)
    </td>
  </tr>
</table>
