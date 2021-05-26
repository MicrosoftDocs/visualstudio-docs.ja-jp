---
title: Visual Studio Shell | Microsoft Docs
description: Visual Studio シェルは、Visual Studio での統合の主要なエージェントであり、基本的な機能を提供し、VSPackage 間の相互通信をサポートしています。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- shell, Visual Studio
- Visual Studio, shell
ms.assetid: cb124ef4-1a6b-4bfe-bfbf-295ef9c07f36
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 5dafd90294fd0968c78846d4162c1ff02c584f3f
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105074341"
---
# <a name="visual-studio-shell"></a>Visual Studio Shell
[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] シェルは、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] での統合の主要なエージェントです。 シェルには、VSPackage が共通サービスを共有できるようにするために必要な機能が用意されています。 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] のアーキテクチャ目標は VSPackage で主要機能を提供することであるため、シェルは基本的な機能を提供し、コンポーネント VSPackage 間の相互通信をサポートするフレームワークです。

## <a name="shell-responsibilities"></a>シェルの役割
 シェルには、次の主要な役割があります。

- (COM インターフェイスを通じて) ユーザー インターフェイス (UI) の基本要素をサポートします。 これには、既定のメニューとツール バー、ドキュメント ウィンドウ フレームまたはマルチドキュメント インターフェイス (MDI) 子ウィンドウ、ツール ウィンドウ フレーム、およびドッキング サポートが含まれます。

- ドキュメントの永続性を調整し、1 つのドキュメントを複数の方法または互換性のない方法で開くことができないようにするために、現在開いているすべてのドキュメントの実行中のリストを実行中のドキュメント テーブル (RDT) で保持する。

- コマンドルーティングとコマンド処理インターフェイス `IOleCommandTarget` をサポートします。

- 適切なタイミングで VSPackage を読み込みます。 シェルのパフォーマンスを向上させるには、VSPackage の遅延読み込みが必要です。

- 基本的なシェル機能を提供する <xref:Microsoft.VisualStudio.Shell.Interop.SVsShell>、基本的なウィンドウ機能を提供する <xref:Microsoft.VisualStudio.Shell.Interop.SVsUIShell> など、特定の共有サービスを管理します。

- ソリューション (.sln) ファイルを管理します。 Visual C++ 6.0 のワークスペース (dsw) ファイルと同様、ソリューションには関連するプロジェクトのグループが含まれます。

- シェル全体の選択、コンテキスト、および通貨を追跡します。 シェルは、次の種類の項目を追跡します。

  - 現在のプロジェクト

  - 現在のプロジェクト項目または現在の <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> の ItemID

  - **[プロパティ]** ウィンドウまたは `SelectionContainer` の現在の選択

  - コマンド、メニュー、およびツール バーの表示を制御する UI コンテキスト ID または CmdUIGuids

  - アクティブ ウィンドウ、ドキュメント、および Undo マネージャーなど、現在アクティブな要素

  - ダイナミック ヘルプを駆動するユーザー コンテキスト属性

  シェルは、インストールされている VSPackage と現在のサービスの間の通信も仲介します。 これにより、シェルのコア機能がサポートされ、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] で統合されているすべての VSPackage で使用できるようになります。 これらのコア機能には次の項目が含まれます。

- **[バージョン情報]** ダイアログ ボックスとスプラッシュ スクリーン

- **[新規追加] および [既存項目の追加]** ダイアログ ボックス

- **[クラス ビュー]** ウィンドウと **オブジェクト ブラウザー**

- **[参照]** ダイアログ ボックス

- **[ドキュメント アウトライン]** ウィンドウ

- **[ダイナミック ヘルプ]** ウィンドウ

- **[検索]** と **[置換]**

- **[新規]** メニューの **[プロジェクトを開く]** および **[ファイルを開く]** ダイアログ ボックス

- **[ツール]** メニューの **[オプション]** ダイアログ ボックス

- **[プロパティ]** ウィンドウ

- **ソリューション エクスプローラー**

- **[タスク一覧]** ウィンドウ

- **ツールボックス**

## <a name="see-also"></a>関連項目
- <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy>
- <xref:Microsoft.VisualStudio.Shell.Interop.SVsShell>
- <xref:Microsoft.VisualStudio.Shell.Interop.SVsUIShell>
- [VSPackages](../../extensibility/internals/vspackages.md)
