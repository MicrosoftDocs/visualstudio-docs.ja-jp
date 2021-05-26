---
title: プロジェクト テンプレートとプロジェクト項目テンプレートの追加 | Microsoft Docs
description: Visual Studio 統合開発環境 (IDE) のダイアログ ボックスにプロジェクト テンプレートとプロジェクト項目テンプレートを追加する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- projects [Visual Studio SDK], adding
- project items [Visual Studio], adding
ms.assetid: 8c59217f-56e5-4540-a73b-cd10de189373
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 3f2c10b310569a412025fd114f7818734106bc18
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105079060"
---
# <a name="add-project-and-project-item-templates"></a>プロジェクト テンプレートとプロジェクト項目テンプレートの追加
独自のプロジェクトの種類を作成する場合は、標準の [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 統合開発環境 (IDE) のダイアログ ボックスを使用して新しいプロジェクトとプロジェクト項目を追加するためのサポートを提供する必要があります。 以降のトピックでは、プロジェクトおよびプロジェクト項目を追加するためのさまざまな手法について説明します。

## <a name="in-this-section"></a>このセクションの内容
- [プロジェクトのコンテキスト](../../extensibility/internals/project-context.md)

 環境で発生するもののコンテキスト情報の大部分がプロジェクトによって提供されることについて説明します。

- [プロジェクトの優先順位](../../extensibility/internals/project-priority.md)

 通常、プロジェクトの項目は 1 つのプロジェクトのメンバーであるため、項目を開くために使用されるプロジェクトが不明確になるのを防ぐために役立つことについて説明します。

- [その他のファイル プロジェクト](../../extensibility/internals/miscellaneous-files-project.md)

 プロジェクト内のファイルを開くために使用できる 2 種類のエディターと、プロジェクト項目を開くときに使用されるエディターを決定するためにプロジェクトが果たす役割に関する情報を提供します。

- [プロジェクトと項目テンプレートの登録](../../extensibility/internals/registering-project-and-item-templates.md)

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] プロジェクトが作成されるときの動作について説明します。

- [[新しい項目の追加] ダイアログ ボックスへの項目の追加](../../extensibility/internals/adding-items-to-the-add-new-item-dialog-boxes.md)

 **[新しい項目の追加]** ダイアログ ボックスに項目を追加するプロセスについて説明します。

- [[新しいプロジェクト] ダイアログ ボックスにディレクトリを追加する](../../extensibility/internals/adding-directories-to-the-new-project-dialog-box.md)

 VSPackage によって使用可能になったカスタム テンプレートを含む新しいディレクトリを登録する例を示します。

- [[新しい項目の追加] ダイアログ ボックスにディレクトリを追加する](../../extensibility/internals/adding-directories-to-the-add-new-item-dialog-box.md)

 **[新しい項目の追加]** ダイアログ ボックスに一連の新しいディレクトリを登録する例を示します。

- [プロジェクト システムを拡張するための IDE 定義コマンド](../../extensibility/internals/ide-defined-commands-for-extending-project-systems.md)

 プロジェクト システムの拡張に使用されるさまざまな種類のコマンド項目の一覧を示します。

- [プロジェクトの拡張に通常使用されるオブジェクトの CATID](../../extensibility/internals/catids-for-objects-that-are-typically-used-to-extend-projects.md)

 [!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)]、[!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)]、[!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)] の各プロジェクト システムを拡張するために使用されるオブジェクトの CATID の一覧を示します。

## <a name="related-sections"></a>関連項目
- [方法: プロジェクト固有のエディターを開く](../../extensibility/how-to-open-project-specific-editors.md)

 プロジェクト固有のエディターに本来バインドされる項目を開くためのステップバイステップの手順について説明します。

- [方法: 標準エディターを開く](../../extensibility/how-to-open-standard-editors.md)

 標準のエディターを開くためのステップバイステップの手順について説明します。

- [プロジェクト サブタイプ](../../extensibility/internals/project-subtypes.md)

 プロジェクトのサブタイプの概念に関するトピックへのリンクを示します。 プロジェクトのサブタイプにより、既存の [!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)] および [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)] プロジェクトが拡張されます。

- [プロジェクトの種類](../../extensibility/internals/project-types.md)

 新しいプロジェクトの種類を設計する方法に関する情報を提供するその他のトピックへのリンクを示します。
