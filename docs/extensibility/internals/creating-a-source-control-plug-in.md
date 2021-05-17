---
title: ソース管理プラグインの作成 |Microsoft Docs
description: Visual Studio 統合開発環境 (IDE) にソース管理機能を追加するソース管理プラグインの作成方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- plug-ins, source control
- source control plug-ins
- source control [Visual Studio SDK], plug-ins
ms.assetid: c7e69fa4-150e-469a-a6fc-fa1260bdbb07
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: dc302ee7327740380bb02e28c99e5117c926c7bc
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105056897"
---
# <a name="create-a-source-control-plug-in"></a>ソース管理プラグインの作成
Visual Studio SDK で提供されるリソースによって、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 統合開発環境 (IDE) にソース管理機能を追加できます。 それによって、このドキュメントに記載されているソース管理プラグイン API に準拠する任意のプラグイン DLL を使用できます。

## <a name="in-this-section"></a>このセクションの内容
- [開始するには](../../extensibility/internals/getting-started-with-source-control-plug-ins.md)

 ソース管理プラグインをインストールする方法について説明します。また、現在使用可能なソース管理プラグイン API のバージョンに重点を置いた説明を行います。

- [アーキテクチャ](../../extensibility/internals/source-control-plug-in-architecture.md)

 アーキテクチャ図を使用して、ソース管理プラグインの [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] IDE との統合について説明します。

- [テスト ガイド](../../extensibility/internals/test-guide-for-source-control-plug-ins.md)

 ソース管理プラグインのインストールと操作のテスト方法に関するガイダンスを提供します。

## <a name="related-sections"></a>関連項目
- [ソース管理 VSPackage の作成](../../extensibility/internals/creating-a-source-control-vspackage.md)

 ソース管理機能を提供すると共に、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ソース管理 UI に置き換わる、ソース管理 VSPackage の作成方法について説明します。

- [ソース管理プラグイン](../../extensibility/source-control-plug-ins.md)

 ソース管理プラグイン API のすべての要素の完全な一覧を提供します。

- [ソース管理](../../extensibility/internals/source-control.md)

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] の統合機能としてソース管理を実装するためのオプションについて説明します。
