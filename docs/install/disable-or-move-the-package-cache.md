---
title: パッケージ キャッシュの無効化または移動
description: Visual Studio 展開のパッケージ キャッシュを無効化、有効化、移動する方法を説明します。
ms.date: 04/14/2017
ms.custom: seodec18
ms.topic: conceptual
f1_keywords:
- cache
- nocache
helpviewer_keywords:
- '{{PLACEHOLDER}}'
- '{{PLACEHOLDER}}'
ms.assetid: 2429993A-3F0E-41C5-9562-FEA6AE994440
author: heaths
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 8472394c06d3388b480abdaf262610811a7a72f4
ms.sourcegitcommit: 21d667104199c2493accec20c2388cf674b195c3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2019
ms.locfileid: "55970258"
---
# <a name="disable-or-move-the-package-cache"></a>パッケージ キャッシュの無効化または移動

パッケージ キャッシュは、インターネット接続がないときに Visual Studio やその他の関連製品の修復が必要になった場合のために、インストール済みパッケージのソースを提供します。 しかしながら、ドライブやシステムを設定しておくことで、すべてのパッケージを維持する必要がなくなることもあります。
インストーラーは必要なときにパッケージをダウンロードします。そのため、ディスク領域を節約または復元する場合、パッケージ キャッシュを無効化したり、移動したりできます。

## <a name="disable-the-package-cache"></a>パッケージ キャッシュの無効化

新しいインストーラーで Visual Studio やその他の製品をインストール、変更、修復する前に、`--nocache` スイッチでインストーラーを開始できます。

```cmd
"%ProgramFiles(x86)%\Microsoft Visual Studio\Installer\vs_installer.exe" --nocache
```

あらゆる製品に対して行うあらゆる操作でその製品の既存パッケージがすべて削除されます。インストール後、パッケージは保存されません。 Visual Studio の変更や修復でパッケージが必要になる場合、自動的にダウンロードされ、インストール後に削除されます。

キャッシュを再有効化する場合、代わりに `--cache` を渡します。 必要なパッケージのみがキャッシュされます。そのため、すべてのパッケージを復元する必要がある場合、ネットワークの接続を切断する前に Visual Studio を修復する必要があります。

```cmd
"%ProgramFiles(x86)%\Microsoft Visual Studio\Installer\vs_installer.exe" repair --passive --norestart --cache
```

また、Visual Studio をインストール、変更、修復する前にキャッシュを無効化するように `KeepDownloadedPayloads` [レジストリ ポリシー](set-defaults-for-enterprise-deployments.md)を設定できます。

## <a name="move-the-package-cache"></a>パッケージ キャッシュの移動

共通のシステム構成は、SSD に Windows をインストールし、ソース コードやプログラム バイナリなど、開発用には大きなハード ディスク (またはハード ディスクより大容量のストレージ) を利用することです。 オフラインで作業する場合、代わりにパッケージ キャッシュを移動できます。

現在のところ、Visual Studio をインストール、変更、修復する前に `CachePath` [レジストリ ポリシー](set-defaults-for-enterprise-deployments.md)を設定する場合にのみこれが可能です。

[!INCLUDE[install_get_support_md](includes/install_get_support_md.md)]

## <a name="see-also"></a>関連項目

* [Visual Studio のインストール](install-visual-studio.md)
* [エンタープライズ展開に既定値を設定する](set-defaults-for-enterprise-deployments.md)
* [コマンド ライン パラメーターを使用して Visual Studio をインストールする](use-command-line-parameters-to-install-visual-studio.md)
