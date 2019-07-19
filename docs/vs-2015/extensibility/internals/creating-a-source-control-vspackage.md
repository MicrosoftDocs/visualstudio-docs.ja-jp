---
title: ソース管理 VSPackage を作成する |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- source control [Visual Studio SDK], creating source control packages
- source control packages
ms.assetid: cca0a9ed-48ff-409f-8036-ed8db0f7533e
caps.latest.revision: 24
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 2b1516cf358a4488ff02e650f6c703a1761a94a2
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "68196955"
---
# <a name="creating-a-source-control-vspackage"></a>ソース管理 VSPackage の作成
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

このドキュメントには、統合ソース管理パッケージのアーキテクチャの概要へのリンクが含まれています[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]、実装するインターフェイスおよび消費するサービスで定義されている API と簡単なソースを示すサンプル。パッケージの実装を制御します。  
  
 ソース管理 VSPackage によるソース管理と統合する密接な統合パスを作成することができます[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]します。 これにより、既定のソース コントロールによってホストされている UI をバイパスするパッケージ[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]、プロジェクト システムからのソース制御要求に応答し、対話、[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]などのコンポーネント**ソリューション エクスプ ローラー**します。 [!INCLUDE[vsipsdk](../../includes/vsipsdk-md.md)]を支援[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]VSPackage を作成するメカニズムと統合可能なパートナー[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]サービス モデルを使用します。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [はじめに](../../extensibility/internals/getting-started-with-source-control-vspackages.md)  
 これはソース管理プラグインでソース管理機能を実装するためより高度な代替ソース管理パッケージについて説明します[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]します。  
  
 [アーキテクチャ](../../extensibility/internals/source-control-vspackage-architecture.md)  
 ダイアグラムを表示し、ソース管理パッケージのコンポーネントについて説明します。  
  
 [機能](../../extensibility/internals/source-control-vspackage-features.md)  
 ソース管理パッケージのさまざまな機能をについて説明します。  
  
 [デザイン要素](../../extensibility/internals/source-control-vspackage-design-elements.md)  
 VSPackage の密接な統合を実装しなければならないソース管理パッケージの構造について説明します。  
  
## <a name="related-sections"></a>関連項目  
 [ソース管理プラグインの作成](../../extensibility/internals/creating-a-source-control-plug-in.md)  
 ソース管理機能を提供するソース管理プラグインを作成する方法について説明します、[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]ソース制御ユーザー インターフェイス (UI)。  
  
 [ソース管理](../../extensibility/internals/source-control.md)  
 統合機能としてソース管理を実装するためのオプションについて説明します[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]します。
