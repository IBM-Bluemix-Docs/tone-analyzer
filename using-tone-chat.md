---

copyright:
  years: 2015, 2020
lastupdated: "2020-01-31"

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

# Using the customer-engagement endpoint
{: #utco}

The {{site.data.keyword.toneanalyzershort}} customer-engagement endpoint analyzes the tone of customer service and support conversations. It can help you better understand your interactions with customers and improve your communications in general or for specific customers. For more information about the interface, including the Node.js, Java, and Python SDKs that are available for calling the service, see the [API reference](https://{DomainName}/apidocs/tone-analyzer){: external}.
{: shortdesc}

Request logging is disabled for the {{site.data.keyword.toneanalyzershort}} service. Regardless of whether you set the `X-Watson-Learning-Opt-Out` request header, the service does not log or retain data from requests and responses.
{: note}

## Requesting a tone analysis
{: #request-tone-chat}

To analyze tone with the customer-engagement endpoint, you call the `POST /v3/tone_chat` method with the following parameters.

<table>
  <caption>Table 1. Parameters of the <code>POST /v3/tone_chat</code>
    method</caption>
  <tr>
    <th style="text-align:left; width:20%">Parameter</th>
    <th style="text-align:center; width:12%">Type</th>
    <th style="text-align:center; width:20%">Data type</th>
    <th style="text-align:left">Description</th>
  </tr>
  <tr>
    <td><code>Body</code><br/><em>Required</em></td>
    <td style="text-align:center">Body</td>
    <td style="text-align:center">JSON object</td>
    <td>
      A JSON <code>ToneChatInput</code> object that contains the
      content that is to be analyzed. For more information, see
      [Specifying JSON input](#JSONrequest).
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
</table>

If you submit more than 50 utterances, the service returns a `warning` field for the overall content at the `utterances_tone` level of its response; it analyzes only the first 50 utterances. If you submit a single utterance that contains more than 500 characters, the service returns an `error` field for that utterance and does not analyze the utterance. In both cases, the request still succeeds with HTTP response code 200.

The service returns response code 400 if all utterances of the input have more than 500 characters.
{: note}

### Example request
{: #exampleRequest}

The following example `curl` command calls the customer-engagement endpoint with the input file <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/tone-analyzer/tone-chat.json" download="tone-chat.json">tone-chat.json <img src="../../icons/launch-glyph.svg" alt="External link icon" title="External link icon"></a> and a version of `2017-09-21`:

```bash
curl -X POST -u "apikey:{apikey}"
--header "Content-Type: application/json"
--data-binary @./tone-chat.json
"{url}/v3/tone_chat?version=2017-09-21"
```
{: pre}

## Specifying JSON input
{: #JSONrequest}

You pass the method a JSON `ToneChatInput` object with the following format. The `utterances` field provides an array of `utterance` objects. The `text` field is a required string that provides an utterance that was contributed by a user to the conversation that is to be analyzed. The `user` field is an optional string that identifies the user who contributed the utterance.

```javascript
{
  "utterances": [
    {
      "text": "",
      "user": ""
    },
    . . .
  ]
}
```
{: codeblock}

The following example shows the contents of the <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/tone-analyzer/tone-chat.json" download="tone-chat.json">tone-chat.json <img src="../../icons/launch-glyph.svg" alt="External link icon" title="External link icon"></a> file. The file includes a brief exchange between a <code>customer</code> and an <code>agent</code>.

```javascript
{
  "utterances": [
    {
      "text": "Hello, I'm having a problem with your product.",
      "user": "customer"
    },
    {
      "text": "OK, let me know what's going on, please.",
      "user": "agent"
    },
    {
      "text": "Well, nothing is working :(",
      "user": "customer"
    },
    {
      "text": "Sorry to hear that.",
      "user": "agent"
    }
  ]
}
```
{: codeblock}

## JSON response content
{: #JSONresponse-tone-chat}

The service returns a JSON `UtteranceAnalyses` object that contains a single field, `utterances_tone`. This field contains an array of `UtteranceAnalysis` objects, each of which provides the following information about an utterance of the input content:

-   `utterance_id` (integer) provides the unique identifier of the utterance. The first utterance has ID 0, and the ID of each subsequent utterance is incremented by one.
-   `utterance_text` (string) provides the text of the utterance.
-   `tones` is an array of `ToneChatScore` objects that provides results for the dominant tones. Such tones have scores of at least 0.5. The array is empty if the utterance has no tone with a score that meets this threshold.

Each `ToneChatScore` object provides the following information about a qualifying tone:

-   `score` (double) is the score for the tone in the range of 0.5 to 1. A score greater than 0.75 indicates a high likelihood that the tone is perceived in the utterance.
-   `tone_id` (string) is the unique, non-localized identifier of the tone; for descriptions of the tones, see [Customer-engagement tones](#tones-tone-chat).
-   `tone_name` (string) is the user-visible, localized name of the tone.

The following example shows the structure of the `UtteranceAnalyses` object:

```javascript
{
  "utterances_tone": [
    {
      "utterance_id": {integer},
      "utterance_text": "{string}",
      "tones": [
        {
          "score": {double},
          "tone_id": "{string",
          "tone_name": "{string}"
        }
      ]
    },
    . . .
  ]
}
```
{: codeblock}

### Example response
{: #exampleResponse-tone-chat}

The following output is returned for the [Example request](#exampleRequest). (The same output is returned for the example in the [Getting started tutorial](/docs/tone-analyzer?topic=tone-analyzer-gettingStarted#customerEngagement).) All reported tones have a score of at least 0.5. Tones with a score of at least 0.75 are likely to be perceived by participants in the conversation.

```javascript
{
  "utterances_tone": [
    {
      "utterance_id": 0,
      "utterance_text": "Hello, I'm having a problem with your product.",
      "tones": [
        {
          "score": 0.686361,
          "tone_id": "polite",
          "tone_name": "Polite"
        }
      ]
    },
    {
      "utterance_id": 1,
      "utterance_text": "OK, let me know what's going on, please.",
      "tones": [
        {
          "score": 0.92724,
          "tone_id": "polite",
          "tone_name": "Polite"
        }
      ]
    },
    {
      "utterance_id": 2,
      "utterance_text": "Well, nothing is working :(",
      "tones": [
        {
          "score": 0.997795,
          "tone_id": "sad",
          "tone_name": "sad"
        }
      ]
    },
    {
      "utterance_id": 3,
      "utterance_text": "Sorry to hear that.",
      "tones": [
        {
          "score": 0.730982,
          "tone_id": "polite",
          "tone_name": "Polite"
        },
        {
          "score": 0.672499,
          "tone_id": "sympathetic",
          "tone_name": "Sympathetic"
        }
      ]
    }
  ]
}
```
{: codeblock}

## Customer-engagement tones
{: #tones-tone-chat}

The service can return scores for the following seven tones.

<table style="width:90%">
  <caption>Table 2. Customer-engagement tones</caption>
  <tr>
    <th style="text-align:left; width:20%">Tone / ID</th>
    <th style="text-align:left">Description</th>
  </tr>
  <tr>
    <td>Excited<br/><code>excited</code></td>
    <td>
      Showing personal enthusiasm and interest
    </td>
  </tr>
  <tr>
    <td>Frustrated<br/><code>frustrated</code></td>
    <td>
      Defined as feeling annoyed and irritable
    </td>
  </tr>
  <tr>
    <td>Impolite<br/><code>impolite</code></td>
    <td>
      Being disrespectful and rude
    </td>
  </tr>
  <tr>
    <td>Polite<br/><code>polite</code></td>
    <td>
      Defined as rational, goal-oriented behavior
    </td>
  </tr>
  <tr>
    <td>Sad<br/><code>sad</code></td>
    <td>
      Regarded as an unpleasant passive emotion
    </td>
  </tr>
  <tr>
    <td>Satisfied<br/><code>satisfied</code></td>
    <td>
      An affective response to perceived service quality
    </td>
  </tr>
  <tr>
    <td>Sympathetic<br/><code>sympathetic</code></td>
    <td>
      An affective mode of understanding that involves emotional resonance
    </td>
  </tr>
</table>
