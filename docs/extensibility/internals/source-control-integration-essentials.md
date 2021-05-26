---
title: ソース管理の統合の基本情報 | Microsoft Docs
description: Visual Studio でサポートされている 2 種類のソース管理統合 (ソース管理プラグインと、VSPackage ベースのソース管理ソリューション) について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Source Control Integration, essentials
- Source Control Integration,overview
- essentials, Source Control Integration
ms.assetid: 442057cb-fd54-4283-96f8-2f6dc8bf2de7
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 155e662eae0dda6689a233e31fd62bb72259ae8b
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105069336"
---
# <a name="source-control-integration-essentials"></a>ソース管理の統合の基本情報
[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] では、2 種類のソース管理統合がサポートされています。ソース管理プラグインは基本的な機能を提供し、ソース管理プラグイン API (旧称 MSSCCI API) を使用して構築されています。VSPackage ベースのソース管理統合ソリューションは、より堅牢な機能を提供します。

## <a name="source-control-plug-in"></a>ソース管理プラグイン
 ソース管理プラグインは、ソース管理プラグイン API を実装する DLL として記述されます。 登録とソース管理の統合機能は、API を通じて提供されます。 この方法は、ソース管理 VSPackage よりも実装が容易であり、ほとんどのソース管理操作に [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] のユーザー インターフェイス (UI) を使用します。

 ソース管理プラグイン API を使用してソース管理プラグインを実装するには、次の手順を実行します。

1. [ソース管理プラグイン](../../extensibility/source-control-plug-ins.md)で指定された関数を実装する DLL を作成します。

2. 「[方法: ソース管理プラグインをインストールする](../../extensibility/internals/how-to-install-a-source-control-plug-in.md)」で説明されているように、適切なレジストリ エントリを作成して DLL を登録します。

3. ヘルパー UI を作成し、(ソース管理プラグインを通じてソース管理機能を処理する [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] コンポーネントである) ソース管理アダプター パッケージの要求に応じて表示します。

   詳細については、「[ソース管理プラグインの作成](../../extensibility/internals/creating-a-source-control-plug-in.md)」を参照してください。

## <a name="source-control-vspackage"></a>ソース管理 VSPackage
 ソース管理 VSPackage の実装では、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] のソース管理 UI をカスタマイズした代替 UI を開発できます。 この方法では、ソース管理の統合を完全に制御できますが、UI 要素を提供すること、また、プラグインの方法で提供されるソース管理インターフェイスを実装することが必要になります。

 ソース管理 VSPackage を実装するには、次の手順に従います。

1. 「[登録と選択](../../extensibility/internals/registration-and-selection-source-control-vspackage.md)」で説明されているように、独自のソース管理 VSPackage を作成して登録します。

2. 既定のソース管理 UI をカスタム UI に置き換えます。 「[カスタム ユーザー インターフェイス](../../extensibility/internals/custom-user-interface-source-control-vspackage.md)」を参照してください。

3. 使用するグリフを指定し、**ソリューション エクスプローラー** のグリフ イベントを処理します。 「[グリフ管理](../../extensibility/internals/glyph-control-source-control-vspackage.md)」を参照してください。

4. 「[クエリの編集とクエリの保存](../../extensibility/internals/query-edit-query-save-source-control-vspackage.md)」で示しているように、クエリの編集とクエリの保存イベントを処理します。

   詳細については、「[ソース管理 VSPackage の作成](../../extensibility/internals/creating-a-source-control-vspackage.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [概要](../../extensibility/internals/source-control-integration-overview.md)
- [ソース管理プラグインの作成](../../extensibility/internals/creating-a-source-control-plug-in.md)
- [ソース管理 VSPackage の作成](../../extensibility/internals/creating-a-source-control-vspackage.md)
