---
title: チュートリアル
description: devinit のチュートリアル。
ms.date: 11/18/2020
ms.topic: reference
author: andysterland
ms.author: andster
manager: jmartens
ms.workload:
- multiple
monikerRange: '>= vs-2019'
ms.prod: visual-studio-windows
ms.technology: devinit
ms.openlocfilehash: 5fc53a534b592b4f6a4799100ce16b1d45049457
ms.sourcegitcommit: 3fc099cdc484344c781f597581f299729c6bfb10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/19/2021
ms.locfileid: "108635324"
---
# <a name="tutorial"></a>チュートリアル

> [!IMPORTANT]
> 2021 年 4 月 12 日以後は、Visual Studio 2019 から GitHub Codespaces への接続はサポートされなくなります。このプライベート プレビューは終了しています。 Microsoft では、クラウドを利用した内部ループと、さまざまな Visual Studio ワークロードに合わせて最適化された VDI ソリューションの進化し続けるエクスペリエンスに焦点を合わせています。 今後のプレビューとロードマップの情報のために、Visual Studio の開発者コミュニティ フォーラムに参加することをお勧めします。

このチュートリアルでは、devinit と Codespaces を使用して [eShopOnWeb リポジトリ](https://github.com/andysterland/eShopOnWeb)を設定する方法について説明します。 このチュートリアルでは、[概要ページ](getting-started-with-devinit.md)の説明に従って、devinit が既に使用可能になっていることを前提としています。

## <a name="step-1-determining-setup-steps"></a>手順 1: セットアップ手順を決定する

[概要ページ](getting-started-with-devinit.md)で説明されているように、最初の手順としては常に、プロジェクトの依存関係とセットアップ手順を決定します。 これはプロジェクトによって異なりますが、次のようないくつかの質問を考慮する必要があります。

- プロジェクトはどのランタイムや SDK に依存していますか?
- プロジェクトにはパッケージが必要ですか (Chocolatey のものなど)?
- セットアップ プロセスではアクションを実行する必要がありますか (スクリプトの実行など)?
- プロジェクトは、Visual Studio と共にインストールされるものに暗黙的に依存していますか?
  - その場合は、devinit のセットアップにもこれらを含めることをお勧めします。 これにより、Visual Studio のインストールに依存することを回避できます。

この情報を確認する最善の方法の 1 つは、現在リポジトリに対して行っている手動セットアップ手順を調べることです。 eShopOnWeb の場合、次のようないくつかの処理を行う必要があります。

- 最新バージョンの .NET Core SDK をインストールする
- 最新バージョンの .NET Entity Framework Core ツール CLI をインストールする
- SQL Server 2019 Express をインストールする
- .NET Entity Framework CLI を使用してローカル データベースを最新の移行に更新する

次に、このすべてを devinit のコンテキストで実現する方法について説明します。

## <a name="step-2-the-devinitjson"></a>手順 2: .devinit.json

まず、[.devinit.json ファイル](devinit-json.md)を作成し、リポジトリのルートに配置します。 このファイルには、`devinit init` コマンドの一部として後で実行される一連の手順を含めます。 `.devinit.json` ファイルに含める内容を決定するために、私たちのセットアップ手順の一覧を、[devinit ツール](devinit-tool-list.md)の一覧と比較します。 ここで、上記のセットアップ手順を使用してこれを行いましょう。

| 手順                                                              | これは devinit で処理できるか?                                                                        |
| :---------------------------------------------------------------- | :----------------------------------------------------------------------------------------------------  |
| 最新の .NET Core SDK をインストールする                                      | **はい**。 [`require-dotnetcoresdk` ツール](tool-require-dotnetcoresdk.md)を使用できます                  |
| .NET Entity Framework Core ツール CLI をインストールする                      | **はい**。 [`dotnet-toolinstall` ツール](tool-dotnet-toolinstall.md)を使用できます                        |
| SQL Server 2019 Express をインストールする                                   | **はい**。 [`choco-install` ツール](tool-choco-install.md)を使用できます                                  |
| .NET Entity Framework を使用してローカル データベースを更新する                 | **いいえ**。ただし、これは devinit とスクリプトを組み合わせることによって実現できます。                               |

このように把握できたので、基本的な `.devinit.json` から始めましょう。 [`.devinit.json` スキーマ](https://json.schemastore.org/devinit.schema-2.0)への参照と空の `run` セクションを含めます。

```json
{
  "$schema": "https://json.schemastore.org/devinit.schema-2.0",
  "run": []
}
```

次に、いくつかのツールを追加してみましょう。

まず、[`require-dotnetcoresdk`](tool-require-dotnetcoresdk.md) を追加します。 そのツールのドキュメントによると、既定の動作では最新の SDK バージョンがインストールされます。 まさにこれが必要なので、次のように `.devinit.json` に追加しましょう。

```json
{
  "$schema": "https://json.schemastore.org/devinit.schema-2.0",
  "run": [
    {
      "comments": "Install the latest version of the .NET Core SDK.",
      "tool": "require-dotnetcoresdk"
    }
  ]
}
```

次に、`dotnet-ef` ツールをグローバルにインストールするために [`dotnet-toolinstall`](tool-dotnet-toolinstall.md) を追加します。 そのドキュメントによると、`input` フィールドを使用してツール名を指定でき、`additionalOptions` フィールドでグローバル スコープを指定できます。

```json
{
  "run": [
    {
      "comments": "Install the latest version of the .NET Core SDK.",
      "tool": "require-dotnetcoresdk"
    },
    {
      "comments": "Install latest version of the .NET Entity Framework Core Tools CLI.",
      "tool": "dotnet-toolinstall",
      "input": "dotnet-ef",
      "additionalOptions": "--global"
    }
  ]
}
```

最後に、`sql-server-express` パッケージをインストールするために [`choco-install`](tool-choco-install.md) を追加します。

```json
{
  "run": [
    {
      "comments": "Install the latest version of the .NET Core SDK.",
      "tool": "require-dotnetcoresdk"
    },
    {
      "comments": "Install latest version of the .NET Entity Framework Core Tools CLI.",
      "tool": "dotnet-toolinstall",
      "input": "dotnet-ef",
      "additionalOptions": "--global"
    },
    {
      "comments": "Install SQL Server 2019 Express",
      "tool": "choco-install",
      "input": "sql-server-express"
    }
  ]
}
```

これで `.devinit.json` が完成しました。次は、devinit の実行とローカル データベースの更新を処理するセットアップ スクリプトについて説明します。

## <a name="step-3-the-setup-script"></a>手順 3: セットアップ スクリプト

devinit の実行とローカル データベースの更新の両方を処理するために、必要なコマンドを実行するスクリプトを作成します。 リポジトリのルートに、`PostCloneSetup.ps1` という名前の空の PowerShell スクリプトを作成しましょう。 まず、`devinit init` の呼び出しを追加します。

```powershell
devinit init
```

`devinit init` を実行すると、`.devinit.json` の `run` セクションで定義されているすべてのツールが実行されます。

最後に、ローカル データベースを更新するために `dotnet ef database update` を呼び出します。

```powershell
devinit init
dotnet ef database update -c catalogcontext -p src\Infrastructure\Infrastructure.csproj -s src\Web\Web.csproj
dotnet ef database update -c appidentitydbcontext -p src\Infrastructure\Infrastructure.csproj -s src\Web\Web.csproj
```

セットアップ スクリプトが完成したので、それを codespace のセットアップ中に実行する `.devcontainer.json` ファイルを追加する必要があります。

## <a name="step-4-the-devcontainerjson"></a>手順 4: .devcontainer.json

codespace の作成中にセットアップ スクリプトが確実に実行されるようにするために、`.devcontainer.json` ファイルを使用します。 他のファイルと同様に、これをリポジトリのルートに配置する必要があります。

`.devcontainer.json` ファイルで必要なのは、`postCreateCommand` の一部としてセットアップ スクリプトを呼び出すことだけです。 これは、codespace 作成プロセスの一部として実行されます。

```json
{
  "postCreateCommand": "Powershell.exe -ExecutionPolicy unrestricted -File .\\PostCloneSetup.ps1"
}
```

以上で作業は終了です。

## <a name="step-5-trying-it-out"></a>手順 5: 試してみる

セットアップ手順が完成したので、[実際のリポジトリ](https://github.com/andysterland/eShopOnWeb)を使用してライブ codespace で試してみましょう。

まず、Visual Studio を使用して codespace を作成します。

:::image type="content" source="media/eshoponweb-github-codespaces-prompt.png" alt-text="codespace を作成する":::

codespace の作成が開始されたら、セットアップ プロセスの進行状況を `C:\.vsonline\.vsoshared\vmTerminal.dat` で監視できます。

:::image type="content" source="media/eshoponweb-watching-progress.png" alt-text="セットアップの進行状況を監視する":::

完了したら、`Web.csproj` を使用してアプリを実行し、すべてが正常に動作していることを確認しましょう。

:::image type="content" source="media/eshoponweb-csproj.png" alt-text="プロジェクトを実行する":::

アプリがビルドされて起動すると、Web ブラウザーでショップを確認できます。

:::image type="content" source="media/eshoponweb-live.png" alt-text="サイトを表示する":::

セットアップ プロセスが正常に動作したので、eShopOnWeb プロジェクトの開発の準備ができました。
