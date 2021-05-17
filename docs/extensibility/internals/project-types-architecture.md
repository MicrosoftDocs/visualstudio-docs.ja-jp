---
title: プロジェクト タイプのアーキテクチャ | Microsoft Docs
description: この記事は、Visual Studio でのプロジェクト タイプのアーキテクチャに関する詳細な情報を含む記事にリンクしています。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- projects [Visual Studio SDK], architecture
ms.assetid: 9c1d940f-8a54-41f7-a8aa-c870e324371c
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 4b03ca1db09df7176eb52d5c8141bf87b1637d79
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105064276"
---
# <a name="project-types-architecture"></a>プロジェクト タイプのアーキテクチャ
このセクションには、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] でのプロジェクト タイプのアーキテクチャに関する詳細な情報が含まれています。

## <a name="in-this-section"></a>このセクションの内容
- [プロジェクト モデルの要素](../../extensibility/internals/elements-of-a-project-model.md)

 プロジェクト タイプで使用できるサービスと、実装する必要があるインターフェイスの一覧を示します。

- [プロジェクト モデルのコア コンポーネント](../../extensibility/internals/project-model-core-components.md)

 追加の機能を提供するために、プロジェクト タイプで実装する必要があるインターフェイスと、必要に応じて実装できるインターフェイスの両方について説明します。

- [プロジェクト タイプを作成する状況](../../extensibility/internals/when-to-create-project-types.md)

 プロジェクト タイプを作成する必要があるのはいつか、また、同じ目標を達成するために VSPackage やエディターなどの別の [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 拡張機能を使用できるのはいつか、の判断に役立ちます。

- [階層と選択](../../extensibility/internals/hierarchies-and-selection.md)

 一貫性があって簡明なユーザー エクスペリエンスを提供するために、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] で階層と選択コンテキストを使用する方法について説明します。

## <a name="related-sections"></a>関連項目
- [プロジェクト サブタイプ](../../extensibility/internals/project-subtypes.md)

 プロジェクト サブタイプを使用して、[!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)] および [!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)] のプロジェクト システムの動作をカスタマイズする方法について説明します。

- [プロジェクトの種類](../../extensibility/internals/project-types.md)

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 統合開発環境 (IDE) の基本的な構成要素であるプロジェクトの概要を説明します。 プロジェクトでコードのビルドとコンパイルを制御するしくみを説明する追加のトピックへのリンクを提供しています。
