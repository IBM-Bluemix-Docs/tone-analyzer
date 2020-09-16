---

copyright:
  years: 2015, 2020
lastupdated: "2020-09-16"

subcollection: tone-analyzer

---

{:help: data-hd-content-type='help'}
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

# Using the customer-engagement endpoint
{: #utco}

The {{site.data.keyword.toneanalyzershort}} customer-engagement endpoint analyzes the tone of customer service and support conversations. It can help you better understand your interactions with customers and improve your communications in general or for specific customers. For more information about the interface, including the Node.js, Java, and Python SDKs that are available for calling the service, see the [API reference](https://{DomainName}/apidocs/tone-analyzer){: external}.
{: shortdesc}

Request logging is disabled for the {{site.data.keyword.toneanalyzershort}} service. Regardless of whether you set the `X-Watson-Learning-Opt-Out` request header, the service does not log or retain data from requests and responses.
{: note}

## Requesting a tone analysis
{: #request-tone-chat}

To analyze tone with the customer-engagement endpoint, you call the `POST /v3/tone_chat` method with the following parameters:

-   `Body` (request body, *required* JSON object) - A JSON `ToneChatInput` object that contains the content that is to be analyzed. For more information, see [Specifying JSON input](#JSONrequest).
-   `version` (query parameter, *required* string) - The version of the API that you want to use as a date in the format `YYYY-MM-DD`; for example, specify `2017-09-21` for September 21, 2017 (the latest version). For more information about all available versions, see the [Release notes](/docs/tone-analyzer?topic=tone-analyzer-rnrn).
-   `Content-Language` (request header, *optional string) - The language of the input content:
    -   `en` (English, the default)
    -   `fr` (French)

    Regional variants are treated as their parent language. For example, `en-US` is interpreted as `en`. The input content must match the specified language. Do not submit content that contains both languages. You can use different languages for the input and response.
-   `Accept-Language` (request header, *optional* string) - The requested language of the response:
    -   `ar` (Arabic)
    -   `de` (German)
    -   `en` (English, the default)
    -   `es` (Spanish)
    -   `fr` (French)
    -   `it` (Italian)
    -   `ja` (Japanese)
    -   `ko` (Korean)
    -   `pt-br` (Brazilian Portuguese)
    -   `zh-cn` (Simplified Chinese)
    -   `zh-tw` (Traditional Chinese)

    For two-character arguments, regional variants are treated as their parent language. For example, `en-US` is interpreted as `en`. You can use different languages for the input and response.

If you submit more than 50 utterances, the service returns a `warning` field for the overall content at the `utterances_tone` level of its response; it analyzes only the first 50 utterances. If you submit a single utterance that contains more than 500 characters, the service returns an `error` field for that utterance and does not analyze the utterance. In both cases, the request still succeeds with HTTP response code 200.

The service returns response code 400 if all utterances of the input have more than 500 characters.
{: note}

### Example request
{: #exampleRequest}
{: help}
{: support}

The following example `curl` command calls the customer-engagement endpoint with the input file [tone-chat.json](https://watson-developer-cloud.github.io/doc-tutorial-downloads/tone-analyzer/tone-chat.json){: external} and a version of `2017-09-21`:

```bash
curl -X POST -u "apikey:{apikey}" \
--header "Content-Type: application/json" \
--data-binary @./tone-chat.json \
"{url}/v3/tone_chat?version=2017-09-21"
```
{: pre}

## Specifying JSON input
{: #JSONrequest}
{: help}
{: support}

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

The following example shows the contents of the [tone-chat.json](https://watson-developer-cloud.github.io/doc-tutorial-downloads/tone-analyzer/tone-chat.json){: external} file. The file includes a brief exchange between a `customer` and an `agent`.

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
{: help}
{: support}

The service can return scores for the following seven tones.

| Tone / ID | Description |
|-----------|-------------|
| Excited<br/>`excited` | Showing personal enthusiasm and interest |
| Frustrated<br/>`frustrated` | Defined as feeling annoyed and irritable |
| Impolite<br/>`impolite` | Being disrespectful and rude |
| Polite<br/>`polite` | Defined as rational, goal-oriented behavior |
| Sad<br/>`sad` | Regarded as an unpleasant passive emotion |
| Satisfied<br/>`satisfied` | An affective response to perceived service quality |
| Sympathetic<br/>`sympathetic` | An affective mode of understanding that involves emotional resonance |
{: caption="Table 1. Customer-engagement tones"}
