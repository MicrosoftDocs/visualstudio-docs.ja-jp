---
title: Visual Studio 2019 の JavaScript および TypeScript
description: JavaScript を直接使用する場合と、TypeScript プログラミング言語を使用する場合の両方について、Visual Studio 2019 が提供するさまざまな JavaScript 開発のサポートを説明します。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 03/16/2020
ms.technology: vs-javascript
ms.topic: conceptual
dev_langs:
- JavaScript
- TypeScript
- DHTML
author: mikejo5000
ms.author: mikejo
manager: jmartens
monikerRange: '>= vs-2019'
ms.openlocfilehash: 267bd8567b60a66bcf9d78c3aef8f02bbc942e0d
ms.sourcegitcommit: e12d6cdaeb37564f05361965db2ec8ad0d4f21ad
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/27/2021
ms.locfileid: "108025879"
---
# <a name="javascript-and-typescript-in-visual-studio-2019"></a>Visual Studio 2019 の JavaScript および TypeScript

## <a name="overview"></a>概要

Visual Studio 2019 は、JavaScript 開発のサポートが充実しており、JavaScript を直接使用することも、[TypeScript プログラミング言語](http://www.typescriptlang.org/)を使用することもできます。TypeScript プログラミング言語は、特に大規模なプロジェクトの開発で、JavaScript 開発の生産性や楽しさが向上するように作成されています。 Visual Studio では、多くのアプリケーション タイプやサービス用に JavaScript または TypeScript コードを記述できます。

## <a name="javascript-language-service"></a>JavaScript 言語サービス

Visual Studio 2019 の JavaScript エクスペリエンスは、TypeScript サポートを提供するのと同じエンジンで実現されています。 このため、機能のサポートや豊富さが向上し、統合も簡単に行えるようになっています。

レガシ JavaScript 言語サービスに復元するオプションは、利用できなくなりました。 現在は、すぐに利用できる新しい JavaScript 言語サービスが用意されています。 新しい言語サービスは、静的分析によって強化された TypeScript 言語サービスのみをベースにしています。 これによりツールの機能が向上するため、JavaScript コードは型定義に基づく高度な IntelliSense の恩恵を受けられるようになります。 新しいサービスは軽量で、消費メモリがレガシ サービスより少ないため、コード サイズが大きくなっても、優れたパフォーマンスが得られます。 また、より大きなプロジェクトを処理するために、言語サービスのパフォーマンスが向上しています。

## <a name="typescript-support"></a>TypeScript のサポート

Visual Studio 2019 では、TypeScript のコンパイルをプロジェクトに統合するためのオプションが複数用意されています。

* [TypeScript NuGet パッケージ](https://www.nuget.org/packages/Microsoft.TypeScript.MSBuild)。 TypeScript 3.2 以降の NuGet パッケージがプロジェクトにインストールされているときは、対応するバージョンの TypeScript 言語サービスがエディターに読み込まれます。
* [TypeScript npm パッケージ](https://www.npmjs.com/package/typescript)。 TypeScript 2.1 以降の npm パッケージがプロジェクトにインストールされているときは、対応するバージョンの TypeScript 言語サービスがエディターに読み込まれます。
* Visual Studio のインストーラーで既定で使用可能な TypeScript SDK、および [VS Marketplace](https://marketplace.visualstudio.com/items?itemName=TypeScriptTeam.typescript-395) からダウンロードされたスタンドアロンの SDK。

> [!TIP]
> プロジェクトが Visual Studio 2019 で開発されている場合は、TypeScript NuGet または TypeScript npm パッケージを使用することをお勧めします。これにより、さまざまなプラットフォームや環境の間で移植性が向上します。 詳細については、[NuGet を使用した TypeScript コードのコンパイル](../javascript/compile-typescript-code-nuget.md)と [tsc を使用した TypeScript コードのコンパイル](../javascript/compile-typescript-code-npm.md)に関する記事をご覧ください。

## <a name="projects"></a>プロジェクト

Visual Studio 2019 で、UWP JavaScript アプリはサポートされなくなりました。 JavaScript UWP プロジェクト (拡張子が *.jsproj* のファイル) は、作成することも、開くこともできません。 詳細については、Windows 上で適切に実行される[プログレッシブ Web アプリ (PWA) の作成](/microsoft-edge/progressive-web-apps-chromium)に関するドキュメントを参照してください。
