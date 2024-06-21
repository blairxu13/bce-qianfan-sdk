# 百度千帆大模型平台 JavaScript SDK

针对百度智能云千帆大模型平台，我们推出了一套 JavaScript SDK（下称千帆 SDK），方便用户通过代码接入并调用千帆大模型平台的能力。

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

## 第一步：安装node.js sdk

```bash
#如果使用npm：
npm install @baiducloud/qianfan
#如果使用yarn：
yarn add @baiducloud/qianfan
```

## 第二步：获得鉴权

### 选择一：使用安全认证AK/SK鉴权   【推荐】
1）登录百度智能云千帆控制台
登录百度智能云千帆控制台，点击“用户账号->安全认证”进入Access Key管理界面。
（2）查看安全认证页面的Access Key/Secret Key
注意：
初始化鉴权时，使用“安全认证/Access Key”中的Access Key和 Secret Key进行鉴权，更多鉴权认证机制请参考鉴权认证机制。
安全认证Access Key(AK)/Secret Key(SK)，和使用的获取AcessToken的应用API Key(AK) 和 Secret Key(SK)不同

### 使用应用AK/SK鉴权调用 【不推荐，后续可能出现新功能不兼容的情况】
（1）登录百度智能云千帆控制台。
注意：为保障服务稳定运行，账户最好不处于欠费状态。
（2）创建千帆应用。
如果已有应用，此步骤可跳过。如果无应用，进入控制台创建应用 ，如何创建应用也可以参考应用接入使用。
（3）在应用接入页，获取应用的API Key、Secret Key。

## 第三步：初始化AK和SK
### 选择一：通过配置文件初始化
在项目的根目录中创建一个名为 .env 的文件，并添加以下内容，SDK从当前目录的 .env 中读取配置。
```bash
QIANFAN_AK=your_api_key
QIANFAN_SK=your_secret_key
```
### 选择二：通过环境变量初始化 【推荐】
```bash
import{setEnvVariable}from"@baiducloud/qianfan";
setEnvVariable('QIANFAN_AK','your_api_key');
setEnvVariable('QIANFAN_SK','your_secret_key');
```
### 选择三：通过参数初始化
```bash
import {ChatCompletion} from "@baiducloud/qianfan";

// 通过参数初始化，应用API Key替换your_api_key，应用Secret Key替换your_secret_key，以对话Chat为例，调用如下
const client = new ChatCompletion({ QIANFAN_AK: 'your_api_key', QIANFAN_SK: 'your_secret_key' });
```

## 第四步：使用SDK
功能如下：
### Chat 单轮对话
```bash
// 使用安全认证AK/SK鉴权，通过环境变量初始化；替换下列示例中参数，安全认证Access Key替换your_iam_ak，Secret Key替换your_iam_sk
setEnvVariable('QIANFAN_ACCESS_KEY','your_iam_ak');
setEnvVariable('QIANFAN_SECRET_KEY','your_iam_sk');

const client = new  ChatCompletion();
async function main() {
    const resp = await client.chat({
        messages: [
            {
                role: 'user',
                content: '你好！',
            },
        ],
    });
    console.log(resp);
}

main();
```

### 指定支持预置服务的模型
```bash
setEnvVariable('QIANFAN_ACCESS_KEY','your_iam_ak');
setEnvVariable('QIANFAN_SECRET_KEY','your_iam_sk');

const client = new  ChatCompletion();
async function main() {
    const resp = await client.chat({
        messages: [
            {
                role: 'user',
                content: '你好！',
            },
        ],
    }, 'ERNIE-Bot-turbo');
    console.log(resp);
}

main();
```
### 用户自行发布的模型服务
```bash
import {ChatCompletion, setEnvVariable} from "@baiducloud/qianfan";

// 使用安全认证AK/SK鉴权，通过环境变量初始化；替换下列示例中参数，安全认证Access Key替换your_iam_ak，Secret Key替换your_iam_sk
setEnvVariable('QIANFAN_ACCESS_KEY','your_iam_ak');
setEnvVariable('QIANFAN_SECRET_KEY','your_iam_sk');

const client = new  ChatCompletion({Endpoint: '***'});
async function main() {
    const resp = await client.chat({
        messages: [
            {
                role: 'user',
                content: '你好',
            },
        ],
    });
    console.log(resp);
}

main();
```
### 多轮对话
```bash

import {ChatCompletion, setEnvVariable} from "@baiducloud/qianfan";

// 使用安全认证AK/SK鉴权，通过环境变量初始化；替换下列示例中参数，安全认证Access Key替换your_iam_ak，Secret Key替换your_iam_sk
setEnvVariable('QIANFAN_ACCESS_KEY','your_iam_ak');
setEnvVariable('QIANFAN_SECRET_KEY','your_iam_sk');

const client = new  ChatCompletion();  
async function main() {    // 调用默认模型，即 ERNIE-Bot-turbo
    const resp = await client.chat({
        messages: [
            {
                role: 'user',
                content: '你好！',
            },
            {
                 role: "assistant",
                 content: "你好，请问有什么我可以帮助你的吗？"
             },
             {
                 role: "user",
                 "content": "我在北京，周末可以去哪里玩？"
             },
        ],
    });
    console.log(resp);
}

main();
```
### 返回事例
```bash

{
  id: 'as-8vcq0n4u0e',
  object: 'chat.completion',
  created: 1709887877,
  result: '北京是一个拥有许多有趣和独特景点的大城市，周末你可以去很多地方玩。例如：
' +
    '
' +
    '1. **故宫博物院**：这是中国最大的古代建筑群，有着丰富的历史和文化遗产，是个很好的适合全家人游玩的地方。
' +
    '2. **天安门广场**：这里是北京的心脏，周围有许多历史和现代建筑。你可以在广场上漫步，欣赏升旗仪式和观看周围的繁华景象。
' +
    '3. **颐和园**：这是一个美丽的皇家园林，有着优美的湖泊和精美的古建筑。你可以在这里漫步，欣赏美丽的景色，同时也可以了解中国的传统文化。
' +
    '4. **北京动物园**：这是中国最大的动物园之一，有许多稀有动物，包括熊猫、老虎、长颈鹿等。对于孩子们来说是个很好的去处。
' +
    '5. **798艺术区**：这是一个充满艺术气息的地方，有许多画廊、艺术工作室和艺术展览。这里有许多新的现代艺术作品，可以欣赏到一些艺术家的创作。
' +
    '6. **三里屯酒吧街**：如果你对夜生活感兴趣，可以去三里屯酒吧街。这里有许多酒吧和餐馆，是一个热闹的夜生活场所。
' +
    '7. **北京环球度假区**：如果你们喜欢主题公园，那么可以去环球度假区，虽然这是在建的，但是等它建好之后肯定是一个很好的去处。
' +
    '
' +
    '当然，你也可以考虑一些其他的地方，比如购物街、博物馆、公园等等。希望这些建议对你有所帮助！',
  is_truncated: false,
  need_clear_history: false,
  usage: { prompt_tokens: 19, completion_tokens: 307, total_tokens: 326 }
}
```

### 流式输出：调用事例

```bash
import {ChatCompletion, setEnvVariable} from "@baiducloud/qianfan";

// 使用安全认证AK/SK鉴权，通过环境变量初始化；替换下列示例中参数，安全认证Access Key替换your_iam_ak，Secret Key替换your_iam_sk
setEnvVariable('QIANFAN_ACCESS_KEY','your_iam_ak');
setEnvVariable('QIANFAN_SECRET_KEY','your_iam_sk');

const client = new  ChatCompletion();
async function main() {
    const stream = await client.chat({
        messages: [
            {
                role: 'user',
                content: '你好！',
            },
        ],
        stream: true,   //启用流式返回
    });
      for await (const chunk of stream as AsyncIterableIterator<any>) {
        console.log(chunk);
    }
}

main();

```

### 流式输出：返回示例

```bash

{
  id: 'as-f7mrqpanb3',
  object: 'chat.completion',
  created: 1709724132,
  sentence_id: 0,
  is_end: false,
  is_truncated: false,
  result: '你好！',
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
  result: '有什么我可以帮助你的吗？',
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
### 续写Completions
千帆 SDK 支持调用续写Completions相关API，支持非流式、流式调用。

#### 非流式

```bash
import {Completions, setEnvVariable} from "@baiducloud/qianfan";

const client = new Completions({ QIANFAN_ACCESS_KEY: 'your_iam_ak', QIANFAN_SECRET_KEY: 'your_iam_sk' });
async function main() {
    const resp = await client.completions({
        prompt: 'In Bash, how do I list all text files in the current directory (excluding subdirectories) that have been modified in the last month',
    }, 'CodeLlama-7b-Instruct');
    console.log(resp);
}

main();
```
#### 非流式-返回示例
```bash

{
    id: 'as-4teyam0huy',
  object: 'chat.completion',
  created: 1718782862,
  result: 'To list all text files in the current directory (excluding subdirectories) that have been modified in the last month, you can use the following command:
' +
    '```
' +
    'find . -type f -name "*.txt" -mtime -1
' +
    '```
' +
    'Explanation:
' +
    '
' +
    '* `.` represents the current directory.
' +
    '* `-type f` specifies that we are looking for files.
' +
    '* `-name "*.txt"` specifies that we are looking for files with the ".txt" extension.
' +
    '* `-mtime -1` specifies that we are looking for files that have been modified in the last month.
' +
    '
' +
    'Note: The `-mtime` option is a GNU extension, and may not be available on all systems. If you are using a different operating system, you may need to use a different command to achieve the same result.',
  is_safe: 1,
  usage: { prompt_tokens: 29, completion_tokens: 158, total_tokens: 187 }
}
```
#### 流式

```bash
import {Completions, setEnvVariable} from "@baiducloud/qianfan";

const client = new Completions({ QIANFAN_ACCESS_KEY: 'your_iam_ak', QIANFAN_SECRET_KEY: 'your_iam_sk' });
async function main() {
    const stream = await client.completions({
        prompt: 'In Bash, how do I list all text files in the current directory (excluding subdirectories) that have been modified in the last month',
        stream: true,   //启用流式返回
    }, 'CodeLlama-7b-Instruct');
     for await (const chunk of stream as AsyncIterableIterator<any>) {
        console.log(chunk);
    }
}

main();
```
#### 流式-返回示例

```bash
{
	'id': 'as-wjs702ndui',
	'object': 'completion',
	'created': 1718782182,
	'sentence_id': 0,
	'is_end': False,
	'result': 'To list all text files in the current directory (excluding subdirectories) that have been modified in the last month in Bash, you can use the',
	'is_safe': 1,
	'usage': {
		'prompt_tokens': 29,
		'completion_tokens': 32,
		'total_tokens': 61
	}
} 
{
	'id': 'as-wjs702ndui',
	'object': 'completion',
	'created': 1718782183,
	'sentence_id': 1,
	'is_end': False,
	'result': ' following command:

find . -type f -name "*.txt" -mtime -1

Here's how the command works',
	'is_safe': 1,
	'usage': {
		'prompt_tokens': 29,
		'completion_tokens': 22,
		'total_tokens': 83
	}
} 
{
	'id': 'as-wjs702ndui',
	'object': 'completion',
	'created': 1718782184,
	'sentence_id': 2,
	'is_end': False,
	'result': ':

* `find`: The find command is used to search for files based on various criteria.
* `.`: The current directory is specified using the',
	'is_safe': 1,
	'usage': {
		'prompt_tokens': 29,
		'completion_tokens': 29,
		'total_tokens': 112
	}
} 
{
	'id': 'as-wjs702ndui',
	'object': 'completion',
	'created': 1718782185,
	'sentence_id': 3,
	'is_end': False,
	'result': ' `.` notation.
* `-type f`: This option tells find to search for files (not directories).
* `-name "*.txt"`: This',
	'is_safe': 1,
	'usage': {
		'prompt_tokens': 29,
		'completion_tokens': 27,
		'total_tokens': 139
	}
}
{
	'id': 'as-wjs702ndui',
	'object': 'completion',
	'created': 1718782186,
	'sentence_id': 4,
	'is_end': False,
	'result': ' option tells find to search for files with the .txt extension.
* `-mtime -1`: This option tells find to search for files that have been',
	'is_safe': 1,
	'usage': {
		'prompt_tokens': 29,
		'completion_tokens': 32,
		'total_tokens': 171
	}
}
{
	'id': 'as-wjs702ndui',
	'object': 'completion',
	'created': 1718782187,
	'sentence_id': 5,
	'is_end': False,
	'result': ' modified in the last month. The `-mtime` option is used to specify the modification time, and the `-1` option tells find to search for files',
	'is_safe': 1,
	'usage': {
		'prompt_tokens': 29,
		'completion_tokens': 35,
		'total_tokens': 206
	}
} 
{
	'id': 'as-wjs702ndui',
	'object': 'completion',
	'created': 1718782188,
	'sentence_id': 6,
	'is_end': False,
	'result': ' that have been modified in the last day.

You can also use the `-mtime +1` option to search for files that have been modified in',
	'is_safe': 1,
	'usage': {
		'prompt_tokens': 29,
		'completion_tokens': 33,
		'total_tokens': 239
	}
}
{
	'id': 'as-wjs702ndui',
	'object': 'completion',
	'created': 1718782189,
	'sentence_id': 7,
	'is_end': False,
	'result': ' the last 2 days, or the `-mtime +2` option to search for files that have been modified in the last 3 days, and so',
	'is_safe': 1,
	'usage': {
		'prompt_tokens': 29,
		'completion_tokens': 32,
		'total_tokens': 271
	}
} 
{
	'id': 'as-wjs702ndui',
	'object': 'completion',
	'created': 1718782190,
	'sentence_id': 8,
	'is_end': False,
	'result': ' on.

Note that the `-mtime` option only works for files that have a modification time that is less than or equal to the current time.',
	'is_safe': 1,
	'usage': {
		'prompt_tokens': 29,
		'completion_tokens': 33,
		'total_tokens': 304
	}
}
{
	'id': 'as-wjs702ndui',
	'object': 'completion',
	'created': 1718782191,
	'sentence_id': 9,
	'is_end': False,
	'result': ' If you want to search for files that have been modified in the last month, you can use the `-mtime -1` option. If you want to',
	'is_safe': 1,
	'usage': {
		'prompt_tokens': 29,
		'completion_tokens': 35,
		'total_tokens': 339
	}
} 
{
	'id': 'as-wjs702ndui',
	'object': 'completion',
	'created': 1718782192,
	'sentence_id': 10,
	'is_end': True,
	'result': ' search for files that have been modified in the last 2 months, you can use the `-mtime -2` option, and so on.',
	'is_safe': 1,
	'usage': {
		'prompt_tokens': 29,
		'completion_tokens': 29,
		'total_tokens': 368
	}
}
```

### 向量Embeddings

#### 默认模型调用
```bash
import {Embedding} from "@baiducloud/qianfan";

const client = new Embedding({ QIANFAN_ACCESS_KEY: 'your_iam_ak', QIANFAN_SECRET_KEY: 'your_iam_sk' });
async function main() {
    const resp = await client.embedding({
        input: ['介绍下你自己吧', '你有什么爱好吗？'],
    });
    const rs = resp.data;
    rs.forEach((data) => {
        console.log(data.embedding);
    })
}

main();
```
#### 默认模型调用-返回示例

```bash
[0.06814255565404892,  0.007878394797444344,  0.060368239879608154, ...]
[0.13463851809501648,  -0.010635783895850182,   0.024348173290491104, ...]
```

#### 指定支持预置服务的模型

```bash
import {Embedding} from "@baiducloud/qianfan";

const client = new Embedding({ QIANFAN_ACCESS_KEY: 'your_iam_ak', QIANFAN_SECRET_KEY: 'your_iam_sk' });
async function main() {
    const resp = await client.embedding({
        input: ['介绍下你自己吧', '你有什么爱好吗？'],
    }, 'Embedding-V1');
    const rs = resp.data;
    rs.forEach((data) => {
        console.log(data.embedding);
    })
}

main();
```

#### 指定支持预置服务的模型--返回示例

```bash


[0.06814255565404892,  0.007878394797444344,  0.060368239879608154, ...]
[0.13463851809501648,  -0.010635783895850182,   0.024348173290491104, ...]

main();
```

### 图像-Images

#### 指定支持预置服务的模型
```bash
import * as http from 'http';
import {Text2Image, setEnvVariable} from "@baiducloud/qianfan";
// 使用安全认证AK/SK鉴权，通过环境变量初始化；替换下列示例中参数，安全认证Access Key替换your_iam_ak，Secret Key替换your_iam_sk
setEnvVariable('QIANFAN_ACCESS_KEY','your_iam_ak');
setEnvVariable('QIANFAN_SECRET_KEY','your_iam_sk');

const client = new Text2Image();

async function main() {
    const resp = await client.text2Image({
        prompt: 'A Ragdoll cat with a bowtie.',
    });

    const base64Image = resp.data[0].b64_image;
    // 创建一个简单的服务器
    const server = http.createServer((req, res) => {
        res.writeHead(200, {'Content-Type': 'text/html'});
        let html = `<html><body><img src="data:image/jpeg;base64,${base64Image}" /><br/></body></html>`;
        res.end(html);
    });

    const port = 3002;
    server.listen(port, () => {
        console.log(`服务器运行在 http://localhost:${port}`);
    });
}

main();
```
#### 指定支持预置服务的模型

```bash
import * as http from 'http';
import {Text2Image, setEnvVariable} from "@baiducloud/qianfan";
// 使用安全认证AK/SK鉴权，通过环境变量初始化；替换下列示例中参数，安全认证Access Key替换your_iam_ak，Secret Key替换your_iam_sk
setEnvVariable('QIANFAN_ACCESS_KEY','your_iam_ak');
setEnvVariable('QIANFAN_SECRET_KEY','your_iam_sk');

const client = new Text2Image();

async function main() {
    const resp = await client.text2Image({
        prompt: 'A Ragdoll cat with a bowtie.',
     }, 'Stable-Diffusion-XL');

    const base64Image = resp.data[0].b64_image;
    // 创建一个简单的服务器
    const server = http.createServer((req, res) => {
        res.writeHead(200, {'Content-Type': 'text/html'});
        let html = `<html><body><img src="data:image/jpeg;base64,${base64Image}" /><br/></body></html>`;
        res.end(html);
    });

    const port = 3002;
    server.listen(port, () => {
        console.log(`服务器运行在 http://localhost:${port}`);
    });
}

main();
```

#### 用户自行发布的模型服务
```bash

import * as http from 'http';
import {Text2Image, setEnvVariable} from "@baiducloud/qianfan";
// 使用安全认证AK/SK鉴权，通过环境变量初始化；替换下列示例中参数，安全认证Access Key替换your_iam_ak，Secret Key替换your_iam_sk
setEnvVariable('QIANFAN_ACCESS_KEY','your_iam_ak');
setEnvVariable('QIANFAN_SECRET_KEY','your_iam_sk');

const client = new Text2Image();

async function main() {
    const resp = await client.text2Image({
        prompt: 'A Ragdoll cat with a bowtie.',
     }, 'Stable-Diffusion-XL');

    const base64Image = resp.data[0].b64_image;
    // 创建一个简单的服务器
    const server = http.createServer((req, res) => {
        res.writeHead(200, {'Content-Type': 'text/html'});
        let html = `<html><body><img src="data:image/jpeg;base64,${base64Image}" /><br/></body></html>`;
        res.end(html);
    });

    const port = 3002;
    server.listen(port, () => {
        console.log(`服务器运行在 http://localhost:${port}`);
    });
}

main();
```

### Fuyu-8B
#### 调用示例
```bash

import {setEnvVariable} from '@baiducloud/qianfan'
import {Image2Text} from "@baiducloud/qianfan";

// 使用安全认证AK/SK鉴权，通过环境变量方式初始化；替换下列示例中参数，安全认证Access Key替换your_iam_ak，Secret Key替换your_iam_sk
setEnvVariable('QIANFAN_AK','your_iam_ak');
setEnvVariable('QIANFAN_SK','your_iam_sk');

// 调用大模型
const client = new Image2Text();
async function main() {
    const resp = await client.image2Text({
        prompt: '分析一下图片画了什么',
        image: 'iVBORw0KGgoAAAANSUhEUgAAB4IAAxxxxxxxxxxxx=',  //  请替换图片的base64编码
    },'Fuyu-8B'
);
    console.log(resp.result)
}

main();
```

#### 返回示例


The image portray s a black and white portrait of a beautiful young woman . She is wearing a red hat, giving her  a hat -like appearance. The black and white nature of the photograph enhances the visual appeal and adds depth to the image .

### Reranker 重排序

```bash
// node环境
import {Reranker} from "@baiducloud/qianfan";
// 直接读取 env  
const client = new Reranker();

// 手动传 AK/SK
// const client = new Reranker({ QIANFAN_AK: '***', QIANFAN_SK: '***'});

// 浏览器环境，必须传入QIANFAN_BASE_URL，（proxy启动后地址）， QIANFAN_CONSOLE_API_BASE_URL不传时，只能使用预置模型，传入后可以使用动态模型
import {Reranker} from "@baiducloud/qianfan";
const client = Reranker({QIANFAN_BASE_URL: 'http://172.18.184.85:8002', QIANFAN_CONSOLE_API_BASE_URL: 'http://172.18.184.85:8003'});

async function main() {
     const resp = await client.reranker({
        query: '上海天气',
        documents: ['上海气候', '北京美食'],
    });
}

main();

```
### HTML 中使用, 引入 dist 文件中的 bundle.iife.js 即可使用，参考example/index.html
```bash
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <h1>Qianfan SDK</h1>
    <script src="../dist/bundle.iife.js"></script>
    <script>
        const {ChatCompletion} = QianfanSDK;
        const client =  new ChatCompletion({QIANFAN_BASE_URL: 'http://172.18.178.105:8002', QIANFAN_CONSOLE_API_BASE_URL: ' http://172.18.178.105:8003'})
     async function main() {
    const stream =  await client.chat({
        messages: [
            {
                role: 'user',
                content: '等额本金和等额本息有什么区别？',
            },
        ],
        stream: true,
    }, 'ERNIE-Bot-turbo');
    console.log('流式返回结果');
    for await (const chunk of stream) {
        console.log(chunk);
    }
}

main();
    </script>
</body>
</html>
```
