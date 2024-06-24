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

## 第二步：连接proxy
浏览器使用不需要鉴权，连接proxy使用，方法如下：

1. 需要先安装python>=3.8
2. pip install qianfan
3. qianfan proxy 在执行qianfan proxy的同级目录下，新建 .env文件，设置 QIANFAN_ACCESS_KEY 和 QIANFAN_SECRET_KEY 即可
注意：在Vue或react项目中集成使用时，需确保webpack为4以下，如果5以上版本需要根据提示配置polyfills，在后续的迭代中会逐步优化。

注意访问地址，需要修改为proxy的ip地址，否则会跨域


## 第三步：初始化AK和SK
### 选择一：通过配置文件初始化
在项目的根目录中创建一个名为 .env 的文件，并添加以下内容，SDK从当前目录的 .env 中读取配置。
```bash
QIANFAN_AK=your_api_key
QIANFAN_SK=your_secret_key
```

## 第四步：使用SDK
功能如下：
### Chat 单轮对话
```bash
// 浏览器环境，必须传入QIANFAN_BASE_URL，（proxy启动后地址）， //QIANFAN_CONSOLE_API_BASE_URL不传时，只能使用预置模型，传入后可以使用动态模型
import {ChatCompletion} from "@baiducloud/qianfan";
const client = new ChatCompletion({QIANFAN_BASE_URL: 'http://172.18.184.85:8002', QIANFAN_CONSOLE_API_BASE_URL: 'http://172.18.184.85:8003'});

async function main() {
    const resp = await client.chat({
        messages: [
            {
                role: "user",
                content: "今天深圳天气",
            },
        ],
    }, "ERNIE-Bot-turbo");
}

main();


```




### 多轮对话
```bash
// 浏览器环境，必须传入QIANFAN_BASE_URL，（proxy启动后地址）， // //QIANFAN_CONSOLE_API_BASE_URL不传时，只能使用预置模型，传入后可以使用动态模型

const client = new ChatCompletion({QIANFAN_BASE_URL: 'http://172.18.184.85:8002', QIANFAN_CONSOLE_API_BASE_URL: 'http://172.18.184.85:8003'});

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
// 浏览器环境，必须传入QIANFAN_BASE_URL，（proxy启动后地址）， // //QIANFAN_CONSOLE_API_BASE_URL不传时，只能使用预置模型，传入后可以使用动态模型

const client = new ChatCompletion({QIANFAN_BASE_URL: 'http://172.18.184.85:8002', QIANFAN_CONSOLE_API_BASE_URL: 'http://172.18.184.85:8003'});
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
// 浏览器环境，必须传入QIANFAN_BASE_URL，（proxy启动后地址）， // //QIANFAN_CONSOLE_API_BASE_URL不传时，只能使用预置模型，传入后可以使用动态模型

import {Completions} from "@baiducloud/qianfan";
const client = Completions({QIANFAN_BASE_URL: 'http://172.18.184.85:8002', QIANFAN_CONSOLE_API_BASE_URL: 'http://172.18.184.85:8003'});

async function main() {
    const resp = await client.completions({
        prompt: 'Introduce the city Beijing',
    }, "SQLCoder-7B");
}


main();
```
参数传入 stream 为 true 时，返回流式结果


```bash

// 流式 
async function main() {
    const stream =  await client.completions({
        prompt: 'Introduce the city Beijing',
        stream: true,
      }, "SQLCoder-7B");
      for await (const chunk of stream as AsyncIterableIterator<any>) {
          // 返回结果
        }
}
main();

```


### 向量Embeddings


```bash
// 浏览器环境，必须传入QIANFAN_BASE_URL，（proxy启动后地址）， //QIANFAN_CONSOLE_API_BASE_URL不传时，只能使用预置模型，传入后可以使用动态模型
import {Eembedding} from "@baiducloud/qianfan";
const client = Eembedding({QIANFAN_BASE_URL: 'http://172.18.184.85:8002', QIANFAN_CONSOLE_API_BASE_URL: 'http://172.18.184.85:8003'});

async function main() {
    const resp = await client.embedding({
        input: [ 'Introduce the city Beijing'],
    }, "Embedding-V1");
}

main();
```


### 图像-Images

文生图

```bash
// 浏览器环境，必须传入QIANFAN_BASE_URL，（proxy启动后地址）， //QIANFAN_CONSOLE_API_BASE_URL不传时，只能使用预置模型，传入后可以使用动态模型

import {Text2Image} from "@baiducloud/qianfan";
const client = Text2Image({QIANFAN_BASE_URL: '***', QIANFAN_CONSOLE_API_BASE_URL: '***'});

async function main() {
    const resp = await client.text2Image({
        prompt: '生成爱莎公主的图片',
        size: '768x768',
        n: 1,
        steps: 20,
        sampler_index: 'Euler a',
    }, 'Stable-Diffusion-XL');

    const base64Image = resp.data[0].b64_image;
    // 注意 base64Image没有带ata:image/jpeg;base64 前缀，要直接使用的话，需要加上
    // 创建一个简单的服务器
    const server = http.createServer((req, res) => {
        res.writeHead(200, {'Content-Type': 'text/html'});
        let html = `<html><body><img src="data:image/jpeg;base64,${base64Image}" /><br/></body></html>`;
        res.end(html);
    });
    const port = 3001;
    server.listen(port, () => {
        console.log(`服务器运行在 http://localhost:${port}`);
    });
}

main();
```
图生文
```bash

import {Image2Text} from "@baiducloud/qianfan";
// 浏览器环境，必须传入QIANFAN_BASE_URL，（proxy启动后地址）， //QIANFAN_CONSOLE_API_BASE_URL不传时，只能使用预置模型，传入后可以使用动态模型

const client = Image2Text({QIANFAN_BASE_URL: 'http://172.18.184.85:8002', QIANFAN_CONSOLE_API_BASE_URL: 'http://172.18.184.85:8003'});

async function main() {
    const resp = await client.image2Text({
        prompt: '分析一下图片画了什么',
        image: '图片的base64编码',
    });
}

main();

```
### Plugin 插件
千帆插件
```bash
// 浏览器环境，必须传入QIANFAN_BASE_URL，（proxy启动后地址），  //QIANFAN_CONSOLE_API_BASE_URL不传时，只能使用预置模型，传入后可以使用动态模型

import {Plugin} from "@baiducloud/qianfan";
const client = Image2Text({QIANFAN_BASE_URL: 'http://172.18.184.85:8002', QIANFAN_CONSOLE_API_BASE_URL: 'http://172.18.184.85:8003'});

// 天气插件
async function main() {
    const resp = await client.plugins({
        query: '深圳今天天气如何',
        /** 
         *  插件名称
         * 知识库插件固定值为["uuid-zhishiku"] 
         * 智慧图问插件固定值为["uuid-chatocr"]
         * 天气插件固定值为["uuid-weatherforecast"]
         */ 
        plugins: [
            'uuid-weatherforecast',
        ],
    });
}

// 智慧图问
async function chatocrMain() {
    const resp = await client.plugins({
        query: '请解析这张图片, 告诉我怎么画这张图的简笔画',
        plugins: [
            'uuid-chatocr',
        ],
        fileurl: 'https://xxx.bcebos.com/xxx/xxx.jpeg',
    });
}

// 知识库
async function zhishikuMain() {
    const reps = await client.plugins({
        query: '你好什么时候飞行员需要负法律责任？',
        plugins: [
            'uuid-zhishiku',
        ],
    });
}

main();

// chatocrMain();

// zhishikuMain();
```
.

### Reranker 重排序

```bash
// 浏览器环境，必须传入QIANFAN_BASE_URL，（proxy启动后地址）， //QIANFAN_CONSOLE_API_BASE_URL不传时，只能使用预置模型，传入后可以使用动态模型

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
