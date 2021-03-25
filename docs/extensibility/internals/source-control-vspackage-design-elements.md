---
title: ソース管理 VSPackage の設計要素 |Microsoft Docs
description: ソース管理 VSPackage が実装する必要がある構造と、ソース管理 VSPackage が実装できるインターフェイスとサービスについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control packages, design elements
ms.assetid: edd3f2ff-ca32-4465-8ace-4330493b67bb
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 1e3e8d70d721e77e0ed7b93dda3be5defdbf7dd9
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105064073"
---
# <a name="source-control-vspackage-design-elements"></a>ソース管理 VSPackage のデザイン要素
このセクションのトピックでは、詳細な統合のためにソース管理 VSPackage が実装する必要がある構造の概要を示します。 また、ソース管理 VSPackage が実装できるインターフェイスとサービス、およびソース管理 VSPackage がソース管理 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] モデルと機能をサポートするために他のコンポーネントから使用できるインターフェイスとサービスについても示します。

## <a name="in-this-section"></a>このセクションの内容
- [VSPackage 構造](../../extensibility/internals/vspackage-structure-source-control-vspackage.md)

 ソース管理 VSPackage の構造を定義します。

- [関連サービスとインターフェイス](../../extensibility/internals/related-services-and-interfaces-source-control-vspackage.md)

 ソース管理パッケージに関連するインターフェイスおよびサービスを一覧表示します。

- [提供されるサービス](../../extensibility/internals/services-provided-source-control-vspackage.md)

 ソース管理 VSPackage によって提供されるソース管理サービスについて説明します。

## <a name="related-sections"></a>関連項目
- [ソース管理 VSPackage の作成](../../extensibility/internals/creating-a-source-control-vspackage.md)

 ソース管理機能を提供するだけでなく、ソース管理 UI のカスタマイズに使用できるソース管理 VSPackage を作成する方法について説明し [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ます。
