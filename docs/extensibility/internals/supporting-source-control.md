---
title: ソース管理のサポート | Microsoft Docs
description: プロジェクトまたはエディターのファイルのチェックアウト、チェックイン、およびその他のソース管理操作が Visual Studio でどのようにサポートされるかについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control [Visual Studio SDK], supporting
ms.assetid: 567acde3-354e-4f39-8d99-0ef86c103396
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 56880cab310367a5c4da3af0cf310867a5519495
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105080607"
---
# <a name="supporting-source-control"></a>ソース管理のサポート
[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] では、プロジェクトまたはエディターのファイルのチェックアウト、チェックイン、およびその他のソース管理操作がサポートされています。 ソース管理クライアントとして、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] は、動的に定義された一連のファイルのアーカイブ、バージョン管理、および制御機能を提供する、[!INCLUDE[vsvss](../../extensibility/includes/vsvss_md.md)] などのソース管理パッケージと対話するように設計されています。

## <a name="in-this-section"></a>このセクションの内容
- [ソース管理パッケージのモデル](../../extensibility/internals/model-for-source-control-packages.md)

 ソース管理をサポートするためにプロジェクト タイプで実装する必要があるインターフェイスについて説明します。

- [設計上の決定事項](../../extensibility/internals/source-control-design-decisions.md)

 プロジェクト タイプの実装方法を左右する質問と回答を示します。

- [構成の詳細](../../extensibility/internals/source-control-configuration-details.md)

 ソース管理のサポートによってプロジェクト タイプの実装がどのように変更されるかについて説明します。

- [プロジェクトとエディターに関する追加のガイドライン](../../extensibility/internals/additional-source-control-guidelines-for-projects-and-editors.md)

 プロジェクト タイプとエディターのベスト プラクティスについて説明します。

- [ランタイムの詳細](../../extensibility/internals/source-control-runtime-details.md)

 ユーザーがプロジェクトをソース管理システムに追加するときにプロジェクトを登録する方法について説明します。

## <a name="reference"></a>関連項目
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2> は、ファイルがメモリ内で変更されようとしているか保存されようとしていることを、環境またはソース管理パッケージに示します。

 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccManager2> は、プロジェクトと階層がソース管理に自身を登録し、ソース管理の状態に関する情報を取得できるようにします。

 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccProject2> は、プロジェクト ファイルおよびプロジェクト項目のソース管理を提供するために、プロジェクト システムに実装されます。

 <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocuments2> は、ソリューション内のファイルまたはディレクトリの追加、削除、または名前変更を行う権限を環境に照会するために、プロジェクトによって使用されます。

 <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocumentsEvents2> は、プロジェクト ファイルまたはディレクトリに加えられた変更をクライアントに通知します。

## <a name="related-sections"></a>関連項目
- [プロジェクトの種類](../../extensibility/internals/project-types.md)

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 統合開発環境 (IDE) の基本的な構成要素であるプロジェクトの概要を説明します。 プロジェクトでコードのビルドとコンパイルを制御する仕組みを説明する追加のトピックへのリンクを提供しています。
