---
title: よく寄せられる質問
description: devinit ツールに関してよく寄せられる質問。
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
ms.openlocfilehash: 603d09de5a37ea7ea4f0ff10c377c56eb9a3d63e
ms.sourcegitcommit: 3fc099cdc484344c781f597581f299729c6bfb10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/19/2021
ms.locfileid: "108635331"
---
# <a name="frequently-asked-questions-for-devinit"></a>devinit に関してよく寄せられる質問

> [!IMPORTANT]
> 2021 年 4 月 12 日以後は、Visual Studio 2019 から GitHub Codespaces への接続はサポートされなくなります。このプライベート プレビューは終了しています。 Microsoft では、クラウドを利用した内部ループと、さまざまな Visual Studio ワークロードに合わせて最適化された VDI ソリューションの進化し続けるエクスペリエンスに焦点を合わせています。 その一環として、`devinit` と関連ツールは利用できなくなります。 今後のプレビューとロードマップの情報のために、Visual Studio の開発者コミュニティ フォーラムに参加することをお勧めします。

## <a name="is-devinit-just-for-github-codespaces"></a>devinit は GitHub Codespaces 用のみですか?

現時点では、devinit は GitHub Codespaces プライベート ベータ版の一部としてのみ使用できます。 ただし、Visual Studio 2019 の今後のリリースに devinit を含めることを計画しています。

## <a name="is-it-windows-only"></a>Windows のみですか?
はい。devinit は、Visual Studio を使用している開発者にとって役立つ開発者環境の作成に重点を置いています。これは、Windows を意味します。 他のプラットフォームも検討していますが、その多くは既に優れたソリューションを備えているため、Visual Studio と Windows から始める必要がありました。

## <a name="theres-no-tool-for-the-dependency-i-need"></a>必要な依存関係のためのツールがありません!

申し訳ございません。 GitHub Codespaces プライベート ベータ版に参加なさっている場合は、プライベート ベータ版のフィードバック チャネルを通じてご連絡いただけます。 プライベート ベータ版に参加なさっていない場合でも、必要な情報についてのフィードバックをお待ちしております。また、問題を [Visual Studio Docs](https://github.com/MicrosoftDocs/visualstudio-docs/) にラベル `devinit` で登録して、必要なツールのサポートを要求していただくことができます。

## <a name="something-went-wrong-how-do-i-debug"></a>問題が発生しました。デバッグするにはどうすればよいですか?

devinit で障害が発生した場合は、まず、`--verbose / -v` フラグで詳細情報を取得してみてください。 devinit から呼び出されている基になるツールで問題が発生している可能性があります。 詳細なログ情報には、次に調べるべき場所の手掛かりが含まれているはずです。

## <a name="why-not-just-a-script"></a>単にスクリプトではだめですか?

スクリプトを使用した環境の設定は、古い手法であり、うまく機能します。 あなたにとってうまく機能するのであれば、使用してください。 開発者にとってスクリプトが最適な選択肢ではない場合に、devinit はもう 1 つのオプションとなります。

## <a name="why-not-a-container"></a>コンテナーではだめですか?

コンテナー (Docker) は、コードを使用して環境をデプロイするための優れたツールです。 コンテナーが適切なソリューションにならない理由はいくつかあります。

1. Windows デスクトップ ベースの開発環境を使用する場合。
1. OS は既にあり、新しい環境をデプロイするのではなくその OS の調整だけを行う場合。

このような理由から、devinit は現在使用している Windows 環境のカスタマイズを目的としています。

## <a name="what-about-other-vm-creation-tools-for-example-terraform-packer-chef-vagrant-etc"></a>他の VM 作成ツール (Terraform、Packer、Chef、Vagrant など) はどうですか

Windows イメージを作成するための優れたツールは多数あり、使用することをお勧めします。 しかし、当社が考えていたすべてのシナリオを満たすものは見つかりませんでした。 devinit の目的は、VM イメージを作成するためのツールではなく、開発者が環境をカスタマイズして特定のリポジトリに必要なものを備え、Visual Studio との優れた統合を行うことができるツールとなることです。

## <a name="what-about-winget"></a>winget はどうですか?

devinit は winget のようなパッケージ マネージャーではなく、そうなる必要はありません。 devinit で winget を使用できるようにしたいため、そのためのツールに取り組んでいます。

## <a name="how-are-restarts-handled"></a>再起動はどのように処理されますか?

devinit によってインストールされたものが OS の再起動を必要としている場合は、コンソールにエラー メッセージが出力されます。 後で都合のよいときに OS を再起動する必要があります。 再起動後、すべての依存関係がインストールされていない場合は、devinit の再実行が必要になることがあります。

## <a name="working-with-others"></a>他との連携

devinit は、アプリが持つ可能性のある依存関係をデプロイおよび構成するために、世にある広範なエコシステムを使用できるようにするためのものです。 devinit には、その提供内容に関する考えがありますが、devinit の主な目的は、他のツールを宣言型の JSON ファイルから実行できるようにすることです。

現在、devinit は開始されたばかりで、[ツールの一覧](devinit-tool-list.md)も始まりにすぎません。
