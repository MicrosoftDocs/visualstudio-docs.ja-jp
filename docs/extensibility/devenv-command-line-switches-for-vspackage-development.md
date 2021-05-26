---
title: VSPackage 開発の Devenv コマンドライン スイッチ | Microsoft Docs
description: 開発者が、Visual Studio IDE を起動するファイルである devenv.exe を実行するときに、コマンド ラインからタスクを自動化する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 12/10/2018
ms.topic: conceptual
helpviewer_keywords:
- /Setup command line switch
- /ResetSkipPkgs command line switch
- /RootSuffix command line switch
- /SafeMode command line switch
- /Splash command line switch
- command-line switches
- registry, Visual Studio SDK
- command line, switches
- Visual Studio SDK, command-line switches
ms.assetid: d65d2c04-dd84-42b0-b956-555b11f5a645
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 94cca255390d9f5637f0bf4f5b24f2d0fd6b4e83
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105091267"
---
# <a name="devenv-command-line-switches-for-vspackage-development"></a>VSPackage 開発の Devenv コマンド ライン スイッチ

Visual Studio を使用すると、開発者は、Visual Studio IDE を起動するファイルである `devenv.exe` を実行するときに、コマンド ラインからタスクを自動化できます。

 タスクは次のとおりです。

- IDE 外部のあらかじめ設計された構成におけるアプリケーションのデプロイ。

- あらかじめ設定されたビルド設定またはデバッグ構成を使用したプロジェクトの自動ビルド。

- すべて IDE 外部からの特定の構成における IDE のロード。 起動時に IDE をカスタマイズすることもできます。

## <a name="guidelines-for-switches"></a>スイッチのガイドライン

Visual Studio ドキュメントでは、ユーザーレベルの `devenv` コマンドライン スイッチについて説明しています。 詳細については、「[Devenv コマンドライン スイッチ](../ide/reference/devenv-command-line-switches.md)」を参照してください。 この `devenv` ツールでは、VSPackage の開発、デプロイ、デバッグに役立つその他のコマンドライン スイッチもサポートされています。

| コマンドライン スイッチ | 説明 |
|---------------------| - |
| `/ResetSkipPkgs` | 問題のある VSPackage の読み込みを避ける必要があるユーザーが追加したスキップ読み込みオプションをすべてクリアしてから、Visual Studio を起動します。 SkipLoading タグがあると、VSPackage の読み込みが無効になります。 タグを消去すると、VSPackage の読み込みが再度有効になります。<br /><br /> このスイッチは引数を取りません。 |
| `/RootSuffix` | 別の場所を使用して、Visual Studio を起動します。 次のコマンドは、Visual Studio SDK インストーラーにより作成されるショートカットで実行されます。<br /><br /> `devenv /RootSuffix exp`<br /><br /> この場合、`exp` は、特定のサフィックス (たとえば `10.0` の代わりに `10.0Exp`) で場所を識別します。 実験用インスタンスを使用すると、コードの記述に使用している Visual Studio のインスタンスとは別に VSPackage をデバッグできます。<br /><br /> このスイッチは、VSRegEx.exe を使用して作成した場所を識別する文字列ならどれでも使用できます。 詳細については、「[実験用インスタンス](../extensibility/the-experimental-instance.md)」を参照してください。 |
| `/SafeMode` | Visual Studio は、既定の IDE およびサービスだけを読み込むセーフ モードで起動します。 `/SafeMode` スイッチを使用すると、Visual Studio の起動時にすべてのサード パーティ VSPackage が読み込まれなくなるため、安定した実行が実現します。<br /><br /> このスイッチは引数を取りません。 |
| `/Setup` | 使用できるすべての VSPackages にある、メニュー、ツールバー、およびコマンド グループを記述したリソース メタデータが Visual Studio により強制的にマージされます。 このコマンドの実行は、管理者としてのみ行えます。 <br /><br /> このスイッチは引数を取りません。 `devenv /Setup` コマンドは、一般的にインストール処理の最後の手順として提示されます。 `/Setup` スイッチを使用しても、IDE は起動しません。|
| `/Splash` | 通常どおり Visual Studio のスプラッシュ スクリーンが表示され、メイン IDE が表示される前にメッセージ ボックスが表示されます。 このメッセージ ボックスでは、スプラッシュ スクリーンの理解を深めることができます (VSPackage 製品アイコンを確認するなど)。<br /><br /> このスイッチは引数を取りません。 |

## <a name="see-also"></a>関連項目

- [コマンドライン スイッチの追加](../extensibility/adding-command-line-switches.md)
- [Devenv コマンドライン スイッチ](../ide/reference/devenv-command-line-switches.md)
