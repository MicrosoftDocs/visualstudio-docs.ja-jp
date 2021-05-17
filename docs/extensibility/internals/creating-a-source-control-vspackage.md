---
title: ソース管理 VSPackage の作成 | Microsoft Docs
description: Visual Studio への統合のための、ソース管理の深い統合パスを作成するソース管理 VSPackage の作成方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control [Visual Studio SDK], creating source control packages
- source control packages
ms.assetid: cca0a9ed-48ff-409f-8036-ed8db0f7533e
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 1085275427aeb02a767a66088ee58ced890dcb05
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105056858"
---
# <a name="create-a-source-control-vspackage"></a>ソース管理 VSPackage の作成
このドキュメントには、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] に統合されるソース管理パッケージのアーキテクチャの概要、実装されるインターフェイスと使用されるサービスによって定義される API、および単純なソース管理パッケージの実装を示すサンプルへのリンクが含まれています。

 ソース管理 VSPackage を使用すると、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] への統合のための、ソース管理の深い統合パスを作成できます。 これにより、パッケージでは、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] でホストされている既定のソース管理 UI のバイパス、プロジェクト システムからのソース管理要求への応答、**ソリューション エクスプローラー** などの [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] コンポーネントとの対話ができるようになります。 [!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)] では、サービス モデルを使用して [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] に統合できる VSPackage を作成するメカニズムによって、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] パートナーが強化されます。

## <a name="in-this-section"></a>このセクションの内容
- [開始するには](../../extensibility/internals/getting-started-with-source-control-vspackages.md)

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] にソース管理機能を実装するための、ソース管理プラグインに代わる、より高度な手段である、ソース管理パッケージについて説明します。

- [アーキテクチャ](../../extensibility/internals/source-control-vspackage-architecture.md)

 図を示し、ソース管理パッケージのコンポーネントについて説明します。

- [機能](../../extensibility/internals/source-control-vspackage-features.md)

 ソース管理パッケージのさまざまな機能について説明します。

- [デザイン要素](../../extensibility/internals/source-control-vspackage-design-elements.md)

 深い統合のために、ソース管理パッケージによって実装される必要がある VSPackage の構造について説明します。

## <a name="related-sections"></a>関連項目
- [ソース管理プラグインの作成](../../extensibility/internals/creating-a-source-control-plug-in.md)

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ソース管理ユーザー インターフェイス (UI) でソース管理機能を提供するソース管理プラグインを作成する方法について説明します。

- [ソース管理](../../extensibility/internals/source-control.md)

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] の統合機能としてソース管理を実装するためのオプションについて説明します。
