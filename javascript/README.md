# Baidu Qianfan Large Model Platform Javascript SDK

For Baidu Cloud's Qianfan Large Model Platform, we have launched a JavaScript SDK (referred to as Qianfan SDK below), which facilitates users to integrate and invoke the capabilities of the Qianfan Large Model Platform through code.

[![license][license-image]][license-url]
[![codecov][codecov-image]][codecov-url]
[![NPM version][npm-image]][npm-url]
[![NPM downloads][download-image]][download-url]
[![docs][docs-image]][docs-url]
[![Feedback Issue][issue-image]][issue-url]
[![Feedback Ticket][ticket-image]][ticket-url]

[license-image]: https://img.shields.io/github/license/baidubce/bce-qianfan-sdk.svg
[license-url]: https://github.com/baidubce/bce-qianfan-sdk/blob/main/LICENSE
[codecov-image]: https://img.shields.io/codecov/c/github/baidubce/bce-qianfan-sdk/main
[codecov-url]: https://codecov.io/gh/baidubce/bce-qianfan-sdk/branch/main
[npm-image]: http://img.shields.io/npm/v/@baiducloud/qianfan
[npm-url]: http://npmjs.org/package/@baiducloud/qianfan
[download-image]: https://img.shields.io/npm/dm/@baiducloud/qianfan
[download-url]: https://npmjs.org/package/@baiducloud/qianfan
[docs-image]: https://img.shields.io/badge/docs-qianfan%20sdk-blue?style=flat-square
[docs-url]: https://github.com/baidubce/bce-qianfan-sdk/blob/main/javascript/README.md
[issue-image]: https://img.shields.io/badge/%E8%81%94%E7%B3%BB%E6%88%91%E4%BB%AC-GitHub_Issue-brightgreen
[issue-url]: https://github.com/baidubce/bce-qianfan-sdk/issues
[ticket-image]: https://img.shields.io/badge/%E8%81%94%E7%B3%BB%E6%88%91%E4%BB%AC-%E7%99%BE%E5%BA%A6%E6%99%BA%E8%83%BD%E4%BA%91%E5%B7%A5%E5%8D%95-brightgreen
[ticket-url]: https://console.bce.baidu.com/ticket/#/ticket/create?productId=279
## Quick Start

## Step 1: Install Node.js SDK

```bash
npm install @baiducloud/qianfan
# or
yarn add @baiducloud/qianfan
```



## Step 2: Authentication

Before using the Qianfan SDK, users need to obtain Access Key and Secret Key from the Baidu Intelligent Cloud Console - Security Authentication page from [Qianfan Console](https://console.bce.baidu.com/iam/#/iam/accesslist), additionally, in the [Qianfan Console] (https://console.bce.baidu.com/qianfan/ais/console/applicationConsole/application), create an application, select the services to enable. For more specific procedures, refer to the platform documentation.

### Option 1: Authenticate Using Access Key/Secret Key (AK/SK) [Recommended]

(1) Log in to the Baidu Intelligent Cloud Qianfan Console, click on "User Account -> Security Authentication" to access the Access Key management interface.

(2) View the Access Key/Secret Key on the Security Authentication page.

Note:
When initializing authentication, use the Access Key and Secret Key from "Security Authentication/Access Key" for authentication. For more authentication mechanisms, please refer to the authentication mechanism documentation.
The Security Authentication Access Key (AK)/Secret Key (SK) is different from the API Key (AK) and Secret Key (SK) used to obtain Access Tokens for applications.

### Option 2: Authenticate Using Application AK/SK for API Calls [Not Recommended, May Lead to Compatibility Issues with New Features]

(1) Log in to the Baidu Cloud Qianfan Console.
   Note: To ensure stable service operation, it is advisable to keep the account in a non-overdue payment status.

(2) Create a Qianfan application.
If you already have an application, you can skip this step. If there is no existing application, create one in the console. You can also refer to the application integration guide for instructions on how to create an application.

(3) On the application access page, obtain the API Key and Secret Key for your application.

## Step 3：Initializing AK (Access Key) and SK (Secret Key)

### Option 1: Initialization via Configuration File [Recommended]

Create a file named .env in the root directory of your project and add the following content. The SDK reads configuration from the .env file in the current directory:

```bash
QIANFAN_AK=your_access_key
QIANFAN_SK=your_secret_key
QIANFAN_ACCESS_KEY=another_access_key
QIANFAN_SECRET_KEY=another_secret_key
```

### Option 2: Initialization via Environment Variables

```bash
setEnvVariable('QIANFAN_AK','your_api_key');
setEnvVariable('QIANFAN_SK','your_secret_key');
```

### Option 3: Initialization via Parameters (Using ChatCompletion as an Example)

```js
import { ChatCompletion } from "@baiducloud/qianfan";

// Initialize using parameters, replace 'your_api_key' with your application's API Key and 'your_secret_key' with your application's Secret Key. Example for ChatCompletion:
const client = new ChatCompletion({ QIANFAN_AK: 'your_api_key', QIANFAN_SK: 'your_secret_key' });

// Alternatively, initialize using parameters for ACCESS_KEY / SECRET_KEY:
const client = new ChatCompletion({ QIANFAN_ACCESS_KEY: 'your_api_key', QIANFAN_SECRET_KEY: 'your_secret_key' });
```
## Step 4: Using SDK
The functionality is as follows:
### Chat Single-turn Dialogue
#### Default Model

```ts
import {ChatCompletion, setEnvVariable} from "@baiducloud/qianfan";

setEnvVariable('QIANFAN_ACCESS_KEY','***');
setEnvVariable('QIANFAN_SECRET_KEY','***');

const client = new  ChatCompletion();
async function main() {
    const resp = await client.chat({
        messages: [
            {
                role: 'user',
                content: 'how are you? please answer in English！',
            },

        ],
    });
    console.log(resp);
}

main();
```

```bash
{
 id: 'as-x0m7bajy10',
  object: 'chat.completion',
  created: 1719824474,
  result: 'Hello, I am an artificial intelligence language model. I do not have a physical form or ability to interact with humans. However, I can answer your questions or provide information in English. What can I do for you?',
  is_truncated: false,
  need_clear_history: false,
  usage: { prompt_tokens: 8, completion_tokens: 44, total_tokens: 52 }
}
```

#### Specify Pre-trained Model

```ts
import {ChatCompletion, setEnvVariable} from "@baiducloud/qianfan";

const client = new  ChatCompletion();
async function main() {
    const resp = await client.chat({
        messages: [
            {
                role: 'user',
                content: 'what is weather like today in shenzhen please answer in english',
            },
        ],
     }, "ERNIE-Bot-turbo");
    console.log(resp);
}

main();
```
```bash
{
 id: 'as-axv9agwvds',
  object: 'chat.completion',
  created: 1719824681,
  result: "Hello, Shenzhen has a subtropical monsoon climate, with hot and humid summers and mild winters. The weather in Shenzhen today is expected to be sunny and hot, with temperatures around 30 degrees Celsius. It is recommended that you wear light clothing and sunscreen if you plan to go outdoors. If you have any other questions about Shenzhen's weather, please feel free to ask me.",
  is_truncated: false,
  need_clear_history: false,
  usage: { prompt_tokens: 13, completion_tokens: 85, total_tokens: 98 }
}
```
#### User-Deployed Custom Model Service
```ts
import {ChatCompletion, setEnvVariable} from "@baiducloud/qianfan";

const client = new  ChatCompletion({Endpoint: '***'});
async function main() {
    const resp = await client.chat({
        messages: [
            {
                role: 'user',
                content: 'hello！',
            },
        ],
    });
    console.log(resp);
}

main
```
### Multi-turn Dialogue

```ts
import {ChatCompletion, setEnvVariable} from "@baiducloud/qianfan";

const client = new  ChatCompletion();  
async function main() {    // 调用默认模型，即 ERNIE-Bot-turbo
    const resp = await client.chat({
        messages: [
            {
                role: 'user',
                content: 'hello！',
            },
            {
                 role: "assistant",
                 content: "hello, is there anything I could help you with？"
             },
             {
                 role: "user",
                 "content": "In Beijing, where can I go for fun on the weekend?"
             },
        ],
    });
    console.log(resp);
}

main();
```

```bash
{
 id: 'as-3wynwqj5bc',
  object: 'chat.completion',
  created: 1719824849,
  result: 'Sure! Here are my suggestions for your weekend plans in Beijing:\n' +
    '\n' +
    'Saturday:\n' +
    '\n' +
    "1. Visit the Forbidden City (故宫): It's one of the most famous landmarks in Beijing and a must-see for tourists.\n" +
    '\n' +
    "2. Take a stroll in the hutong (胡同): Beijing's hutong are traditional alleys that are full of local life. You can try some local food and chat with the locals.\n" +
    '\n' +
    "3. Visit the Temple of Heaven: It's a beautiful place with a lot of historical buildings and gardens.\n" +
    '\n' +
    "4. Try some local food: Beijing's cuisine is famous throughout China, and you can try some delicious dishes like roast duck and potstickers.\n" +
    '\n' +
    'Sunday:\n' +
    '\n' +
    "1. Visit the Great Wall: It's one of the Seven Wonders of the World and a must-see for any traveler. You can take a hiking or bike ride to see the beautiful scenery.\n" +
    '\n' +
    "2. Visit the Bird's Nest and Water Cube: These are two iconic buildings from the 2008 Beijing Olympics. You can take a tour or just take some photos.\n" +
    '\n' +
    '3. Explore the city center: Beijing has a lot of shopping centers and markets where you can find local goods and souvenirs.\n' +
    '\n' +
    'Remember to pack comfortable shoes and wear a jacket or sweater during the cooler months. Enjoy your weekend in Beijing!',
  is_truncated: false,
  need_clear_history: false,
  usage: { prompt_tokens: 21, completion_tokens: 305, total_tokens: 326 }
}
```
### Streaming Output

By passing `stream: true`

```ts
import {ChatCompletion, setEnvVariable} from "@baiducloud/qianfan";

const client = new  ChatCompletion();
async function main() {
    const stream = await client.chat({
        messages: [
            {
                role: 'user',
                content: 'hello',
            },
        ],
        stream: true,   //streaming mode
    });
      for await (const chunk of stream as AsyncIterableIterator<any>) {
        console.log(chunk);
    }
}

main();
```

```bash
{
  id: 'as-f7mrqpanb3',
  object: 'chat.completion',
  created: 1709724132,
  sentence_id: 0,
  is_end: false,
  is_truncated: false,
  result: 'hello',
  need_clear_history: false,
  usage: { prompt_tokens: 2, completion_tokens: 0, total_tokens: 2 }
}
{
  id: 'as-f7mrqpanb3',
  object: 'chat.completion',
  created: 1709724132,
  sentence_id: 1,
  is_end: false,
  is_truncated: false,
  result: 'may I help you with anything?',
  need_clear_history: false,
  usage: { prompt_tokens: 2, completion_tokens: 0, total_tokens: 2 }
}
{
  id: 'as-f7mrqpanb3',
  object: 'chat.completion',
  created: 1709724132,
  sentence_id: 2,
  is_end: true,
  is_truncated: false,
  result: '',
  need_clear_history: false,
  usage: { prompt_tokens: 2, completion_tokens: 8, total_tokens: 10 }
}
```
### Continuation 

The Qianfan SDK supports calling the Continuation Completions API, offering both non-streaming and streaming invocation methods.

#### Default Model

```ts
import {Completions, setEnvVariable} from "@baiducloud/qianfan";

const client = new Completions({ QIANFAN_ACCESS_KEY: 'your_iam_ak', QIANFAN_SECRET_KEY: 'your_iam_sk' });
async function main() {
    const resp = await client.completions({
        prompt: 'In Bash, how do I list all text files in the current directory (excluding subdirectories) that have been modified in the last month',
    });
    console.log(resp);
}

main();
```
#### Specify Pre-trained Model

```ts
import {Completions, setEnvVariable} from "@baiducloud/qianfan";

const client = new Completions();
async function main() {
    const resp = await client.completions({
        prompt: 'hello',
    }, 'ERNIE-Bot');
    console.log(resp);
}

main();
```
#### User-Deployed Custom Model Service

Passing the service address through Endpoint

```ts
import {Completions, setEnvVariable} from "@baiducloud/qianfan";

const client = new Completions({QIANFAN_ACCESS_KEY: '***', QIANFAN_SECRET_KEY: '***', Endpoint: '***'});
async function main() {
    const resp = await client.completions({
        prompt: 'hello，who are you',
    });
    console.log(resp);
}

main();
```

```bash
{
  id: 'as-hfmv5mvdim',
  object: 'chat.completion',
  created: 1709779789,
  result: 'Hello! How can I help you today? Whether you have any questions or need assistance, I'll do my best to provide answers and support. Please feel free to let me know your needs, and I'll respond as quickly as possible.',
  is_truncated: false,
  need_clear_history: false,
  finish_reason: 'normal',
  usage: { prompt_tokens: 1, completion_tokens: 34, total_tokens: 35 }
}
```
#### streaming 

```ts
import {Completions, setEnvVariable} from "@baiducloud/qianfan";

const client = new Completions({ QIANFAN_ACCESS_KEY: '***', QIANFAN_SECRET_KEY: '***' });
async function main() {
    const stream = await client.completions({
        prompt: 'hello, who are you?',
        stream: true,   //streaming response
    });
     for await (const chunk of stream as AsyncIterableIterator<any>) {
        console.log(chunk);
    }
}

main();
```

```bash
{
  id: 'as-cck51r1rfw',
  object: 'chat.completion',
  created: 1709779938,
  sentence_id: 0,
  is_end: false,
  is_truncated: false,
  result: 'hello！',
  need_clear_history: false,
  finish_reason: 'normal',
  usage: { prompt_tokens: 1, completion_tokens: 2, total_tokens: 3 }
}
{
  id: 'as-cck51r1rfw',
  object: 'chat.completion',
  created: 1709779938,
  sentence_id: 1,
  is_end: false,
  is_truncated: false,
  result: 'Is there anything I can help you with?',
  need_clear_history: false,
  finish_reason: 'normal',
  usage: { prompt_tokens: 1, completion_tokens: 2, total_tokens: 3 }
}
{
  id: 'as-cck51r1rfw',
  object: 'chat.completion',
  created: 1709779938,
  sentence_id: 2,
  is_end: true,
  is_truncated: false,
  result: '',
  need_clear_history: false,
  finish_reason: 'normal',
  usage: { prompt_tokens: 1, completion_tokens: 8, total_tokens: 9 }
}
```
### Embeddings

The Qianfan SDK also supports calling models within the Qianfan Large Model Platform to convert input text into vector representations represented by floating-point numbers. These semantic vectors can be used in scenarios such as text retrieval, information recommendation, and knowledge mining.

#### Default Model

```ts
import {Embedding} from "@baiducloud/qianfan";

const client = new Embedding();
async function main() {
    const resp = await client.embedding({
        input: ['Can you introduce yourself?', 'Do you have any hobbies?'],
    });
    const data = resp.data[0] as any;
    console.log(data.embedding);
}

main();
```

```bash
[0.06814255565404892,  0.007878394797444344,  0.060368239879608154, ...]
[0.13463851809501648,  -0.010635783895850182,   0.024348173290491104, ...]
```
#### Specify Pre-trained Model
Embedding-V1


Embedding-V1

```ts

import {Eembedding} from "@baiducloud/qianfan";

const client = new Eembedding({ QIANFAN_ACCESS_KEY: '***', QIANFAN_SECRET_KEY: '***' });
async function main() {
    const resp = await client.embedding({
        input: ['Can you introduce yourself?', 'Do you have any hobbies?'],
    }, 'Embedding-V1');
    const data = resp.data[0] as any;
    console.log(data.embedding);
}

main();
```

```bash
[0.13463850319385529,  -0.010635782964527607,   0.024348171427845955...]
```
### Images

#### image generating from text


```ts
import * as http from 'http';
import {Text2Image, setEnvVariable} from "@baiducloud/qianfan";
const client = new Text2Image({Endpoint：'***'});

async function main() {
    const resp = await client.text2Image({
        prompt: 'A Ragdoll cat with a bowtie.',
    });

    const base64Image = resp.data[0].b64_image;
    // create a simple server:
    const server = http.createServer((req, res) => {
        res.writeHead(200, {'Content-Type': 'text/html'});
        let html = `<html><body><img src="data:image/jpeg;base64,${base64Image}" /><br/></body></html>`;
        res.end(html);
    });

    const port = 3002;
    server.listen(port, () => {
        console.log(`server is running on http://localhost:${port}`);
    });
}

main();
```

#### text generating from image
##### Pre-trained Model Fuyu-8B
```ts
import {setEnvVariable} from '@baiducloud/qianfan'
import {Image2Text} from "@baiducloud/qianfan";

// using big model
const client = new Image2Text();
async function main() {
    const resp = await client.image2Text({
        prompt: 'Analyzing what a picture depicts',
        image: 'iVBORw0KGgoAAAANSUhEUgAAB4IAAxxxxxxxxxxxx=',  // replace the base64 encoding of an image
    });
    console.log(resp.result)
}

main();
```

### Plugin

#### qianfan pluggin

The SDK supports platform plugin capabilities to help users quickly build LLM applications or integrate LLM into their own programs. It supports plugins such as knowledge base, smart graph Q&A, weather, and more.
```ts
import {Plugin} from "@baiducloud/qianfan";
// Note: The qianfan plugin requires passing an Endpoint. The yiyan plugin does not require it.
const client = new Plugin({Endpoint: '***'});

// weatherchat pluggin
async function main() {
    const resp = await client.plugins({
        query: 'what's the weather like in shenzhen today?',
       Here is the translation of the text into English:

/** 
 * Plugin Name
 * Knowledge Base Plugin has a fixed value of ["uuid-zhishiku"]
 * Wisdom Image Q&A Plugin has a fixed value of ["uuid-chatocr"]
 * Weather Plugin has a fixed value of ["uuid-weatherforecast"]
 */

        plugins: [
            'uuid-weatherforecast',
        ],
    });
}


async function chatocrMain() {
    const resp = await client.plugins({
        query: 'In English, please analyze this picture and tell me how to draw a simple sketch of it.',
        plugins: [
            'uuid-chatocr',
        ],
        fileurl: 'https://xxx.bcebos.com/xxx/xxx.jpeg',
    });
}

// 知识库
async function zhishikuMain() {
    const reps = await client.plugins({
        query: 'Hello, when do pilots need to assume legal responsibility?',
        plugins: [
            'uuid-zhishiku',
        ],
    });
}

main();

// chatocrMain();

// zhishikuMain();
```
#### yiyan pluggin API-V2

Sure, here's a brief overview of each component:

**ImageAI:**
ImageAI enables text creation and answering questions based on images. It assists in writing copy, generating stories, and creating visual content. It currently supports images up to 10MB in size.

**ChatFile:**
Formerly known as ChatFile, it allows tasks such as summarizing, Q&A, and content creation based on documents. It supports documents up to 10MB in size but does not support scanned documents.

**eChart:**
eChart uses Apache Echarts to provide data insights and create various types of charts, including bar charts, line charts, pie charts, radar charts, scatter plots, funnel charts, and mind maps (tree charts).



```ts
// eChart plugin
async function yiYaneChartMain() {
    const resp = await client.plugins({
        messages: [
            {
                "role": "user",
                "content": "Help me draw a pie chart: In August, there were 100 bug reports, 100 feature requests, and 100 usage consultations, totaling 300 feedback entries."
            }
        ],
        plugins: ["eChart"],
    });
}

yiYaneChartMain() 

// ImageAI plugin
async function yiYanImageAIMain() {
    const resp = await client.plugins({
        messages: [
            {
                "role": "user",
                "content": "<img>cow.jpeg</img><url>https://xxx/xxx/xxx.jpeg</url> what are in this photo"
            }
        ],
        plugins: ["ImageAI"],
    });
}

yiYanImageAIMain()

// ChatFiletesting
async function yiYanChatFileMain() {
    const resp = await client.plugins({
        messages: [
            {'role': 'user', 'content': '<file>Discussion on the Nutritional Value and Consumption Trends of Milk.docx</file><url>https://xxx/xxx/xxx.docx</url>'},
            // eslint-disable-next-line max-len
            {'role': 'assistant', 'content': 'Milk, as a natural food rich in nutrients and easy to digest and absorb, is widely popular. Its value is mainly manifested in two aspects: nutritional composition and medical value. In terms of nutritional composition, milk contains various essential nutrients such as fats, proteins, lactose, minerals, and water, in appropriate proportions that are easily digested and absorbed. In terms of medical value, milk promotes growth and development and helps maintain a healthy level, positively impacting children's growth. Furthermore, milk has a promising market outlook, with increasing consumer attention, evolving consumer psychology, and market demands. To better harness the nutritional value of milk, it is important to drink it in a healthy manner, in moderation, and choose suitable milk products according to individual needs. In conclusion, milk is an ideal natural food, not only rich in nutrients but also with significant medical and market value. We should fully recognize the value of milk, consume it scientifically, and allow milk to play a greater role in our health.'},
            {'role': 'user', 'content': 'What are the nutritional components of milk?'},
        ],
        plugins: ['ChatFile']
    });
}
yiYanChatFileMain();
```
### Reranker 

Cross-lingual semantic representation algorithm models specialize in optimizing semantic search results and precise semantic relevance ranking. They support four languages: Chinese, English, Japanese, and Korean.

```ts
import {Reranker} from "@baiducloud/qianfan";
// read env file
const client = new Reranker();

async function main() {
     const resp = await client.reranker({
        query: 'shanghai weather',
        documents: ['shanghai weather', 'beijing cuisine'],
    });
}

main();

```


