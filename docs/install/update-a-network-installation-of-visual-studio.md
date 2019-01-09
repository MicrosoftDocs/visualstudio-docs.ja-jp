---
title: ネットワーク ベース インストールを更新する
description: --layout コマンドを実行して Visual Studio のネットワークベース インストールを更新する方法について説明します
ms.date: 08/14/2017
ms.custom: seodec18
ms.prod: visual-studio-dev15
ms.topic: conceptual
helpviewer_keywords:
- '{{PLACEHOLDER}}'
- '{{PLACEHOLDER}}'
ms.assetid: 1AF69C0E-0AC9-451B-845D-AE4EDBCEA65C
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 55509f49aff21d5c4e4319a35de20b29a6bc3f75
ms.sourcegitcommit: 37fb7075b0a65d2add3b137a5230767aa3266c74
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/02/2019
ms.locfileid: "53906404"
---
# <a name="update-a-network-based-installation-of-visual-studio-2017"></a>Visual Studio 2017 のネットワーク ベース インストールを更新する

ネットワーク インストール レイアウトを Visual Studio の最新のインストール ポイントとして使用できるように、また、クライアント ワークステーションに既に配置されているインストールを保持するために、最新の製品の更新プログラムを使って Visual Studio のネットワーク インストール レイアウトを更新できます。

## <a name="how-to-update-a-network-layout"></a>ネットワーク レイアウトの更新方法

最新の更新プログラムが含まれるように、ネットワーク インストールの共有を更新するには、--layout コマンドを実行して、更新されたパッケージの増分をダウンロードします。

最初にネットワーク レイアウトを作成したときに部分的レイアウトを選択した場合は、その設定が保存されます。  以後のレイアウト コマンドでは以前のオプションと、指定した新しいすべてのオプションが使用されます。  (これは 15.3 の新機能です。)古いバージョンのレイアウトを使用している場合は、コンテンツの更新時に最初にネットワーク インストール レイアウトを作成したときに使用したものと同じコマンドライン パラメーター (つまり、同じワークロードと言語) を使用してください。

ファイル共有上にレイアウトをホストしている場合は、レイアウトのプライベート コピーを更新し (例: c:\vs2017offline)、すべての更新されたコンテンツがダウンロードされた後に、ファイル共有にコピーします (例: \\server\products\VS2017)。 この操作を行わない場合、レイアウトの更新中にユーザーがセットアップを実行しても、レイアウトが完全に更新されていないため、レイアウトからすべてのコンテンツを取得できない可能性が非常に高くなります。

レイアウトを作成して更新する方法について順番に説明します。

* 最初に、英語のみ対象の 1 つのワークロードを含むレイアウトの作成例を示します。

  ```cmd
  vs_enterprise.exe --layout c:\VS2017Layout --add Microsoft.VisualStudio.Workload.ManagedDesktop --lang en-US
  ```

* 以下は、同じレイアウトを新しいバージョンに更新する場合です。 追加のコマンド ライン パラメーターを指定する必要はありません。 このレイアウト フォルダーに保存されている以前の設定が、後続のすべてのレイアウト コマンドで使用されます。

  ```cmd
  vs_enterprise.exe --layout c:\VS2017Layout
  ```

* ここでは、お使いのレイアウトを無人方式で新しいバージョンに更新する方法を示します。 レイアウト操作は、新しいコンソール ウィンドウでセットアップ プロセスを実行します。 ユーザーが最終的な結果と、発生した可能性のあるエラーの概要を確認できるように、ウィンドウは開いたままになります。 無人方式でレイアウト操作を実行している場合は (たとえば、定期的に実行してお使いのレイアウトを最新バージョンに更新するスクリプトがある場合)、`--passive` パラメーターを使うと、プロセスは自動的にウィンドウを閉じます。

  ```cmd
  vs_enterprise.exe --layout c:\VS2017Layout --passive
  ```

* 次に、追加のワークロードとローカライズされた言語を追加する方法を示します。  (このコマンドでは、Azure のワークロードを追加しています。)これで、Managed Desktop と Azure の両方がこのレイアウトに含まれるようになります。  英語とドイツ語の言語リソースもすべてのワークロードに含まれます。  さらに、レイアウトが利用可能な最新バージョンに更新されます。

  ```cmd
  vs_enterprise.exe --layout c:\VS2017Layout --add Microsoft.VisualStudio.Workload.Azure --lang de-DE
  ```

* 最後に、バージョンを更新せずに追加のワークロードとローカライズされた言語を追加する方法を示します。 (このコマンドでは、ASP.NET Web のワークロードを追加しています。)これで、Managed Desktop、Azure、ASP.NET Web のワークロードがこのレイアウトに含まれるようになりました。  英語、ドイツ語、フランス語の言語リソースもすべてのワークロードに含まれます。  ただし、このコマンドが実行されたときにレイアウトが利用可能な最新バージョンに更新されませんでした。  そのため、既存のバージョンのままになります。

  ```cmd
  vs_enterprise.exe --layout c:\VS2017Layout --add Microsoft.VisualStudio.Workload.NetWeb --lang fr-FR --keepLayoutVersion
  ```

## <a name="how-to-deploy-an-update-to-client-machines"></a>クライアント マシンに更新を配置する方法

ネットワーク環境が構成される方法によって、更新プログラムをエンタープライズ管理者が配置することも、クライアント マシンから開始することもできます。

* ユーザーは、オフラインのインストール フォルダーからインストールした Visual Studio インスタンスを更新することができます。
  * Visual Studio インストーラーを実行します。
  * 次に、**[更新]** をクリックします。

* 管理者は、次の 2 つの別々のコマンドを使用して、ユーザーの相互作用なしに、Visual Studio のクライアント展開を更新できます。
  * 最初に、Visual Studio インストーラーを更新します。 <br>```vs_enterprise.exe --quiet --update```
  * 次に、Visual Studio アプリケーション自体を更新します。 <br>```vs_enterprise.exe update --installPath "C:\Program Files (x86)\Microsoft Visual Studio\2017\Enterprise" --quiet --wait --norestart```

> [!NOTE]
> [vswhere.exe コマンド](tools-for-managing-visual-studio-instances.md)を使用して、クライアント コンピューター上にある Visual Studio の既存のインスタンスのインストール パスを特定します。
>
> [!TIP]
> 更新通知をユーザーに表示するときの制御方法の詳細については、「[Control updates to network-based Visual Studio deployments](controlling-updates-to-visual-studio-deployments.md)」 (ネットワーク ベースの Visual Studio 配置の更新プログラムを制御する) を参照してください。

## <a name="how-to-verify-a-layout"></a>レイアウトを検証する方法

`--verify` を使用して指定したオフライン キャッシュに対する検証を行います。 パッケージ ファイルが見つからないか、無効であるかどうかがチェックされます。 検証の最後に、見つからないファイルと無効なファイルのリストを出力します。

```cmd
vs_enterprise.exe --layout <layoutDir> --verify
```

layoutDir 内の vs_enterprise.exe を呼び出すことができます。

> [!NOTE]
> レイアウト オフライン キャッシュには `--verify` オプションで必要とされるいくつかの重要なメタデータ ファイルが必要です。 これらのメタデータ ファイルが見つからない場合、"--verify" が実行できず、セットアップでエラーが返されます。 このエラーが発生した場合、新しいオフライン レイアウトを別のフォルダー (または同じオフライン キャッシュ フォルダー) に再作成してください。 そのためには、初期オフライン レイアウトの作成に使用したものと同じレイアウト コマンドを実行します。 たとえば、`Vs_enterprise.exe --layout <layoutDir>` のようにします。

Microsoft は定期的に Visual Studio の更新プログラムを提供しているため、作成した新しいレイアウトが初期レイアウトと同じバージョンでない可能性があります。

## <a name="how-to-fix-a-layout"></a>レイアウトの修正方法

`--fix` を使用して `--verify` と同じ検証を実行して、特定された問題の修正も試みます。 `--fix` の処理にはインターネット接続が必要なため、`--fix` を呼び出す前に、コンピューターがインターネットに接続していることを確認してください。

```cmd
vs_enterprise.exe --layout <layoutDir> --fix
```

layoutDir 内の vs_enterprise.exe を呼び出すことができます。

## <a name="how-to-remove-older-versions-from-a-layout"></a>以前のバージョンをレイアウトから削除する方法

オフライン キャッシュにレイアウトの更新を実行した後、レイアウト キャッシュ フォルダーには最新の Visual Studio のインストールに不要な古いパッケージがいくつか含まれている場合があります。 `--clean` オプションを使用すると、オフライン キャッシュ フォルダーから古いパッケージを削除できます。

これを行うには、その古いパッケージが含まれるカタログ マニフェストのファイル パスが必要になります。 カタログ マニフェストは、オフライン レイアウト キャッシュの "Archive" フォルダーにあります。 これは、レイアウトの更新時に保存されたものです。 "Archive" フォルダーには、1 つまたは複数の "GUID" 名フォルダーがあり、そのそれぞれに古いカタログ マニフェストが含まれています。 "GUID" フォルダーの数は、オフライン キャッシュに対する更新プログラムの数と同じである必要があります。

各 "GUID" フォルダー内にいくつかのファイルが保存されています。 特に関係のあるファイルが "catalog.json" ファイルと "version.txt" ファイルの 2 つです。 "catalog.json" ファイルは `--clean` オプションに渡す必要がある古いカタログ マニフェストです。 その他の version.txt ファイルには、この古いカタログ マニフェストのバージョンが含まれています。 バージョン番号に基づき、このカタログ マニフェストから古いパッケージを削除するかどうかを決定できます。 他の "GUID" フォルダーでも同じように行います。 クリーンアップを実行するカタログが決まったら、そのカタログのファイル パスを指定して `--clean` カタログを実行します。

--clean オプションを使用するいくつかの例を示します。

```cmd
vs_enterprise.exe --layout <layoutDir> --clean <file-path-of-catalog1> <file-path-of-catalog2> …
```

```cmd
vs_enterprise.exe --layout <layoutDir> --clean <file-path-of-catalog1> --clean <file-path-of-catalog2> …
```

&lt;layoutDir&gt; 内の vs_enterprise.exe を呼び出すことができます。 次に例を示します。

```cmd
c:\VS2017Layout\vs_enterprise.exe --layout c:\VS2017Layout --clean c:\VS2017Layout\Archive\1cd70189-fc55-4583-8ad8-a2711e928325\Catalog.json --clean c:\VS2017Layout\Archive\d420889f-6aad-4ba4-99e4-ed7833795a10\Catalog.json
```

このコマンドを実行すると、セットアップでオフライン キャッシュ フォルダーが分析され、削除されるファイルのリストが検索されます。 このリストで、削除されるファイルを確認し、削除を確定できます。

[!INCLUDE[install_get_support_md](includes/install_get_support_md.md)]

## <a name="see-also"></a>関連項目

* [Visual Studio のインストール](install-visual-studio.md)
* [Visual Studio 管理者ガイド](visual-studio-administrator-guide.md)
* [コマンド ライン パラメーターを使用して Visual Studio をインストールする](use-command-line-parameters-to-install-visual-studio.md)
* [Visual Studio インスタンスの検出および管理用のツール](tools-for-managing-visual-studio-instances.md)
* [ネットワーク ベースの Visual Studio 配置の更新プログラムを制御する](controlling-updates-to-visual-studio-deployments.md)
