---
title: devinit の使用を開始する
description: devinit の概要ガイド。
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
ms.openlocfilehash: 660bb5a2c3d235a347e478d55ae8176e87c5d626
ms.sourcegitcommit: 3fc099cdc484344c781f597581f299729c6bfb10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/19/2021
ms.locfileid: "108635357"
---
# <a name="getting-started-with-devinit"></a>devinit の使用を開始する

> [!IMPORTANT]
> 2021 年 4 月 12 日以後は、Visual Studio 2019 から GitHub Codespaces への接続はサポートされなくなります。このプライベート プレビューは終了しています。 Microsoft では、クラウドを利用した内部ループと、さまざまな Visual Studio ワークロードに合わせて最適化された VDI ソリューションの進化し続けるエクスペリエンスに焦点を合わせています。 その一環として、`devinit` と関連ツールは利用できなくなります。 今後のプレビューとロードマップの情報のために、Visual Studio の開発者コミュニティ フォーラムに参加することをお勧めします。

devinit は、任意のユーザーが簡単なコマンドを実行してコードにアクセスし、リポジトリで生産性を向上させるために使用できるツールです。 devinit を使用すると、リポジトリに必要なシステム全体の依存関係 (SQL Server、Node.js、Docker、IIS など) をすべて定義できます。 devinit では、他のツールやパッケージ マネージャーを呼び出して、リポジトリに必要なものをインストールできます。 これらの依存関係は [.devinit.json](devinit-json.md) という名前の JSON ファイルで定義します。次にリポジトリを使用するユーザーは、[`devinit init`](devinit-commands.md#init) を実行するだけで、これらの依存関係をすべてインストールできます。 そのため、新しいリポジトリへのオンボードを数分で完了できます。

devinit 自体は、パッケージ マネージャーでも仮想マシン (VM) 構成ツールでもありません。 これは、アプリケーションが必要とするシステム全体の依存関係を定義する [.devinit.json](devinit-json.md) という名前のマニフェスト ファイルのタスク ランナーです。 これらの依存関係をインストールするために、devinit では既に使用されている可能性のあるツール ([Chocolatey](https://chocolatey.org) など) を使用します。 使用可能なツールの一覧は、[こちら](devinit-tool-list.md)で確認できます。 devinit では、ソフトウェアを直接配布するのではなく、これらのツールを使用することにより、ユーザーが任意のツールを使用して既存の構成 (Chocolatey の [packages.config](https://chocolatey.org/docs/commands-install#packagesconfig) ファイルなど) を使用できるようにします。  

## <a name="step-1-get-devinit"></a>手順 1: devinit を入手する

現在、devinit は Visual Studio の使用時に GitHub Codespaces の一部としてのみ入手可能であり、Visual Studio の統合ターミナルからアクセスできます。 今後、devinit を Visual Studio の一部として入手できるようになる予定です。

## <a name="step-2-define-your-environment"></a>手順 2: 環境を定義する

最も重要な手順は、[.devinit.json ファイル](devinit-json.md)で "開発" 環境を定義することです。 このファイルは、`devinit init` の実行時に環境を作成するために devinit によって使用されます。

ここでは、プロジェクト リポジトリの使用を開始するための手順について考えてみましょう。 たとえば、SQL がインストールされている必要はありますか。 特定のバージョンの .NET Core が必要ですか。 同様に続きます。 次に、それぞれの依存関係について、[ツールの一覧](devinit-tool-list.md)で devinit に対応するツールを探し、それをリポジトリの `.devinit.json` ファイルに追加します。

[サンプルに関するドキュメント](sample-readme.md)で、選択可能なサンプルを確認することもできます。または、この[チュートリアル](tutorial.md)を参照してください。

## <a name="step-3-enjoy"></a>手順 3: 使用を開始する

これで、リポジトリの複製が実行された後で、`devinit init` を使用できるようになります。

```console
devinit init
```

[GitHub Codespaces](https://github.com/features/codespaces) を使用する場合は、codespace のプロビジョニング時に自動的に実行されるように `devinit init` を構成できます。 詳細については、[devinit と GitHub Codespaces に関するドキュメント](devinit-and-codespaces.md)を参照してください。
