### 始めかた
<!-- 
### First steps
-->

<!--
In this set of articles, you'll learn the **core fundamentals** of Nest. To get familiar with the essential building blocks of Nest applications, we'll build a basic CRUD application with features that cover a lot of ground at an introductory level.
-->
この記事では、Nestの**基礎**について学びます。Nestアプリケーションの重要な構成要素に慣れるよう、入門レベルとしては多くの機能をカバーする基本的なCRUDアプリケーションを構築していきます。

<!--
#### Language
-->
#### 言語

<!--
We're in love with [TypeScript](http://www.typescriptlang.org/), but above all - we love [Node.js](https://nodejs.org/en/). That's why Nest is compatible with both TypeScript and **pure JavaScript**. Nest takes advantage of the latest language features, so to use it with vanilla JavaScript we need a [Babel](http://babeljs.io/) compiler.
-->
私たちは[TypeScript](http://www.typescriptlang.org/)が大好きですが、なにより[Node.js](https://nodejs.org/en/)が大好きです。なので、NestにはTypeScriptと**純粋なJavaScript**の両方に互換性を持たせています。Nestは最新の言語機能を利用しているため、純粋なJavaScriptで使用するには[Babel](http://babeljs.io/)コンパイラが必要です。

<!--
We'll mostly use TypeScript in the examples we provide, but you can always **switch the code snippets** to vanilla JavaScript syntax (simply click to toggle the language button in the upper right hand corner of each snippet).
-->
説明に使用するサンプルコードは主にTypeScriptになりますが、JavaScriptに**切り替える**こともできます（各サンプルコードの右上にある言語切り替えボタンをクリックするだけです）。

<!--
#### Prerequisites
-->
#### 要件

<!--
Please make sure that [Node.js](https://nodejs.org/) (>= 8.9.0) is installed on your operating system.
-->
ご使用のオペレーティングシステムに[Node.js](https://nodejs.org/)（>= 8.9.0）がインストールされていることを確認してください。

<!--
#### Setup
-->
#### セットアップ

<!--
Setting up a new project is quite simple with the [Nest CLI](/cli/overview). With [npm](https://www.npmjs.com/) installed, you can create a new Nest project with the following commands in your OS terminal:
-->
[Nest CLI](/cli/overview)を使うと、新しいプロジェクトを簡単にセットアップできます。[npm](https://www.npmjs.com/)がインストール済みなら、OSのターミナルで次のコマンドを実行するだけで、新しいNestプロジェクトを作成することができます。


```bash
$ npm i -g @nestjs/cli
$ nest new project-name
```

<!--
The `project` directory will be created, node modules and a few other boilerplate files will be installed, and a `src/` directory will be created and populated with several core files.
-->
`project`ディレクトリが作成され、Nodeモジュールとひな形ファイルがインストールされ、`src/`ディレクトリにはコアファイルの一式が入ります。

<div class="file-tree">
  <div class="item">src</div>
  <div class="children">
    <div class="item">app.controller.ts</div>
    <div class="item">app.module.ts</div>
    <div class="item">main.ts</div>
  </div>
</div>

<!--
Here's a brief overview of those core files:
-->
これらのコアファイルの概要は次のとおりです。

<!--
|                     |                                                                                                                     |
| ------------------- | ------------------------------------------------------------------------------------------------------------------- |
| `app.controller.ts` | Basic controller sample with a single route.                                                                        |
| `app.module.ts`     | The root module of the application.                                                                                 |
| `main.ts`           | The entry file of the application which uses the core function `NestFactory` to create a Nest application instance. |
-->

|                     |                                                                                                                     |
| ------------------- | ------------------------------------------------------------------------------------------------------------------- |
| `app.controller.ts` | 単一ルートのコントローラの基本的なサンプル。 |
| `app.module.ts`     | アプリケーションのルートモジュール。 |
| `main.ts`           | Nestアプリケーションのインスタンスを作成するために、コア機能である`NestFactory`を使用するアプリケーションのエントリファイル。 |

<!--
The `main.ts` includes an async function, which will **bootstrap** our application:
-->
この`main.ts`には、アプリケーションを**起動(bootstrap)**する非同期関数が含まれています:

```typescript
@@filename(main)

import { NestFactory } from '@nestjs/core';
import { ApplicationModule } from './app.module';

async function bootstrap() {
  const app = await NestFactory.create(ApplicationModule);
  await app.listen(3000);
}
bootstrap();
@@switch
import { NestFactory } from '@nestjs/core';
import { ApplicationModule } from './app.module';

async function bootstrap() {
  const app = await NestFactory.create(ApplicationModule);
  await app.listen(3000);
}
bootstrap();
```

<!--
To create a Nest application instance, we use the core `NestFactory` class. `NestFactory` exposes a few static methods that allow creating an application instance. The `create()` method returns an application object, which fulfills the `INestApplication` interface. This object provides a set of methods which are described in the coming chapters. In the `main.ts` example above, we simply start up our HTTP listener, which lets the application await inbound HTTP requests.
-->
Nestアプリケーションのインスタンスを作成するために、コアの`NestFactory`クラスを使います。`NestFactory`アプリケーションインスタンスの作成のための静的メソッドを公開します。この`create()`メソッドは、`INestApplication`インタフェースを満たすアプリケーションオブジェクトを返します。このオブジェクトは、後述の章で説明するメソッドの一式を提供します。上記の`main.ts`では、HTTPリスナーを起動し、アプリケーションがHTTPリクエストを受け取れるようになります。

<!--
Note that a project scaffolded with the Nest CLI creates an initial project structure that encourages developers to follow the convention of keeping each module in its own dedicated directory.
-->
Nest CLIで生成されたプロジェクトは初期的なプロジェクト構造であり、各モジュールはそれ専用のディレクトリに格納する規約に従っていくことが開発者に推奨されることにご留意ください。

<!--
#### Platform
-->
#### プラットフォーム

<!--
Nest aims to be a platform-agnostic framework. Platform independence makes it possible to create reusable logical parts that developers can take advantage of across several different types of applications. Technically, Nest is able to work with any Node HTTP framework once an adapter is created. There are two HTTP platforms supported out-of-the-box: [express](https://expressjs.com/) and [fastify](https://www.fastify.io). You can choose the one that best suits your needs.
-->
Nestはプラットフォームにとらわれないフレームワークを目指しています。プラットフォームに依存しないので、開発者はさまざまな種類のアプリケーションで再利用可能な論理的な部分を作成することができます。技術的には、アダプターを作りさえすれば、NestはどんなHTTPフレームワークともの連携できます。今すぐ使えるHTTPプラットフォームは2つあり、[express](https://expressjs.com/)と[fastify](https://www.fastify.io)です。開発者のニーズに最も合うものを選ぶことができます。

<!--
|                    |                                                                                                                                                                                                                                                                                                                                    |
| ------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `platform-express` | [Express](https://expressjs.com/) is a well-known minimalist web framework for node. It's a battle tested, production-ready library with lots of resources implemented by the community. The `@nestjs/platform-express` package is used by default. Many users are well served with Express, and need take no action to enable it. |
| `platform-fastify` | [Fastify](https://www.fastify.io/) is a high performance and low overhead framework highly focused on providing maximum efficiency and speed. Read how to use it [here](/techniques/performance).                                                                                                                                  |
-->

|                    |                                                                                                                                                                                                                                                                                                                                    |
| ------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `platform-express` | [Express](https://expressjs.com/)は、Node向けのミニマリストWebフレームワークとして有名です。Nodeは実戦で使い倒されており、コミュニティによって実装された数多くのリソースを備えたプロダクションで使えるライブラリです。この`@nestjs/platform-express`パッケージはデフォルトで使用されます。多くのユーザーにはExpressが役に立ち、有効にするためには何もする必要がありません。 |
| `platform-fastify` | [Fastify](https://www.fastify.io/)は、効率とスピードの最大化に重点を置いた、高性能で低オーバーヘッドのフレームワークです。 使い方は[こちら](/techniques/performance)をご覧ください。                                                                                                                                  |

<!--
Whichever platform is used, it exposes its own application interface. These are seen respectively as `NestExpressApplication` and `NestFastifyApplication`.
-->
どのプラットフォームを使用しても、固有のアプリケーションインタフェースを公開します。これらはそれぞれ`NestExpressApplication`と`NestFastifyApplication`として見えます。

<!--
When you pass a type to the `NestFactory.create()` method, as in the example below, the `app` object will have methods available exclusively for that specific platform. Note, however, you don't **need** to specify a type **unless** you actually want to access the underlying platform API.
-->
以下の例のように、`NestFactory.create()`メソッドに型を渡すと、`app`オブジェクトはその特定のプラットフォーム専用のメソッドを持つようになります。ただし、実際に基盤となるプラットフォームのAPIにアクセスする場合を**除き**、型を指定する**必要**はありません。

```typescript
const app = await NestFactory.create<NestExpressApplication>(ApplicationModule);
```

<!--
#### Running the application
-->
#### アプリケーションを実行する

<!--
Once the installation process is complete, you can run the following command at your OS command prompt to start the application listening for inbound HTTP requests:
-->
インストールの手順が完了したら、OSのコマンドプロンプトで次のコマンドを実行し、HTTPリクエストを待機するアプリケーションを起動できます:

```bash
$ npm run start
```

<!--
This command starts the app with the HTTP server listening on the port defined in the `src/main.ts` file. Once the application is running, open your browser and navigate to `http://localhost:3000/`. You should see the `Hello world!` message.
-->
このコマンドはアプリを起動します。HTTPサーバは`src/main.ts`で定義されたポートを利用します。アプリケーションが起動したら、ブラウザを開いて`http://localhost:3000/`にアクセスしてください。`Hello world!`というメッセージが表示されるはずです。

