---
title: devinit と GitHub Codespaces
description: devinit を使用して codespace を Visual Studio 向けにカスタマイズする方法について説明します。
ms.date: 08/28/2020
ms.topic: reference
author: andysterland
ms.author: andster
manager: jmartens
ms.workload:
- multiple
monikerRange: '>= vs-2019'
ms.prod: visual-studio-windows
ms.technology: devinit
ms.openlocfilehash: c98c00e0b62d3a2a755790b07621d717abcb41c1
ms.sourcegitcommit: 3fc099cdc484344c781f597581f299729c6bfb10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/19/2021
ms.locfileid: "108635335"
---
# <a name="devinit-and-github-codespaces"></a>devinit と GitHub Codespaces

> [!IMPORTANT]
> 2021 年 4 月 12 日以後は、Visual Studio 2019 から GitHub Codespaces への接続はサポートされなくなります。このプライベート プレビューは終了しています。 Microsoft では、クラウドを利用した内部ループと、さまざまな Visual Studio ワークロードに合わせて最適化された VDI ソリューションの進化し続けるエクスペリエンスに焦点を合わせています。 その一環として、`devinit` と関連ツールは利用できなくなります。 今後のプレビューとロードマップの情報のために、Visual Studio の開発者コミュニティ フォーラムに参加することをお勧めします。

devinit は [GitHub Codespaces](https://github.com/features/codespaces) をよく補完するものであり、共同作成者がすぐにビルド、実行、デバッグできるように devinit で codespace をセットアップできます。

> [!IMPORTANT]
> devinit を codespace と統合する前に、まず、依存関係を定義する `.devinit.json` ファイルがあることを確認する必要があります。 `.devinit.json` を作成する方法の詳細については、[概要ドキュメント](getting-started-with-devinit.md)を参照してください。

GitHub Codespace の内部で、アプリケーションが構築され、クラウドで実行されます。 クラウドに存在することは、アプリケーションがコンピューター上のローカル リソースにアクセスできないことを意味します。 これには、ローカルにインストールされているツールやプログラムが含まれます。 アプリケーションでシステム全体の依存関係をインストールまたは構成する必要がある場合は、codespace ごとに実行する必要があります。 これを実現する最も簡単な方法は、`.devinit.json` ファイルを使用することです。

アプリケーションに必要な依存関係を備えた codespace が作成されるようにするには、codespace の作成時に `devinit` を実行する必要があります。 これを行うには、リポジトリのルートに配置された `.devcontainer.json` ファイルで定義されている `postCreateCommand` から `devinit init` を呼び出します。 codespace でリポジトリが複製された後、`postCreateCommand` の文字列が既定のシェルで実行されます。 `postCreateCommand` の詳細については、GitHub Codespaces の[カスタマイズに関するドキュメント](https://docs.github.com/github/developing-online-with-codespaces/configuring-codespaces-for-your-project)を参照してください。 `devinit` コマンドを追加するには、次の例に示すように、`devinit init` を `postCreateCommand` に追加します。

また、codespace に接続した後、Visual Studio 統合ターミナルから `devinit init -f <path to .devinit.json>` を実行することもできます。

## <a name="examples"></a>例

次の両方の例で、`.devinit.json` は `.devcontainer.json` と共にリポジトリのルートにあります。

### <a name="with-a-devcontainerjson-file"></a>.devcontainer.json ファイルで

この例では、次の `.devcontainer.json` ファイルが `.devinit.json` ファイルと共にリポジトリのルートに配置されています。 また、これらのファイルを `.devcontainer` ディレクトリに配置することもできます。

```json
{
  "postCreateCommand": "devinit init"
}
```

`.devinit.json` が別のディレクトリにある場合は、-f フラグを使用できます。

```json
{
  "postCreateCommand": "devinit init -f path\\to\\.devinit.json"
}

```

```json
{
  "postCreateCommand": ["<some other command>", "devinit init"]
}
```

devinit の使用例については、Microsoft の[ドキュメント](sample-all-tool.md)と、GitHub の [.NET Core の例](https://github.com/microsoft/devinit-example-dotnet-core)および [Node.js の例](https://github.com/microsoft/devinit-example-nodejs)のリポジトリを参照してください。

### <a name="as-commands"></a>コマンドとして

この例では、次の `.devcontainer.json` ファイルがリポジトリのルートに配置されており、個別のツールを実行するために `devinit run` がコマンド ラインから直接呼び出されています。  

```json
{
  "postCreateCommand": ["devinit run –t require-dotnetcoresdk"]
}
```

### <a name="from-a-terminal-prompt"></a>ターミナルのプロンプトから

`.devinit.json` ファイルが現在の作業ディレクトリに含まれている場合。

```console
devinit init
```

`.devinit.json` が別のディレクトリにある場合。

```console
devinit init -f path/to/.devinit.json
```
