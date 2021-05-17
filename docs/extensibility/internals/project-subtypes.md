---
title: プロジェクト サブタイプ | Microsoft Docs
description: プロジェクト サブタイプを使用して、Visual Studio のプロジェクト システムの動作をカスタマイズする方法について説明します。 VSPackage では、COM 集計を使用してプロジェクト サブタイプを実装します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- projects [Visual Studio SDK], subtypes
- project subtypes [Visual Studio SDK]
ms.assetid: d235b47b-cf11-4d47-a63f-e33d9d16105d
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: e1695bc79e38c7a9ebbda7736e57116123343f30
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105064333"
---
# <a name="project-subtypes"></a>プロジェクト サブタイプ
プロジェクト サブタイプを使用して、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] のプロジェクト システムの動作をカスタマイズまたは風味付けすることができます。 カスタマイズには、プロジェクト ファイルへの追加データの保存、 **[新しい項目の追加]** ダイアログ ボックスでの項目の追加またはフィルター処理、アセンブリのデバッグおよびデプロイ方法の制御、プロジェクトの **[プロパティ ページ]** ダイアログ ボックスの拡張などが含まれます。 VSPackage では、COM 集計を使用してプロジェクト サブタイプを実装します。

> [!NOTE]
> Visual C++ プロジェクト システムでは、プロジェクト サブタイプをサポートしていません。 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 自体では、プロジェクト サブタイプを使用して、SQL Server プロジェクトやスマート デバイス プロジェクトを実装します。

## <a name="in-this-section"></a>このセクションの内容

- [プロジェクト サブタイプのデザイン](../../extensibility/internals/project-subtypes-design.md)

  プロジェクト サブタイプの概念について説明します。

- [プロジェクト サブタイプの初期化シーケンス](../../extensibility/internals/initialization-sequence-of-project-subtypes.md)

  [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 環境による、プログラムからのプロジェクト サブタイプ初期化シーケンスについて説明します。

- [プロジェクト サブタイプによって拡張されるプロパティとメソッド](../../extensibility/internals/properties-and-methods-extended-by-project-subtypes.md)

  プロジェクト サブタイプを使用して拡張されることが最も多い関数およびメソッドについて詳しく説明します。

- [MSBuild プロジェクト ファイルでのデータの保持](../../extensibility/internals/persisting-data-in-the-msbuild-project-file.md)

  プロジェクト ファイルにデータを永続化する方法と、<xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment> を使用してプロジェクト サブタイプのアグリゲーション レベル全体でプロジェクト ファイルにデータを保持する方法について説明します。

- [プロジェクト プロパティのユーザー インターフェイス](../../extensibility/internals/project-property-user-interface.md)

  プロジェクト サブタイプでプロジェクトの **[プロパティ ページ]** ダイアログ ボックスを変更する方法について説明します。

- [ベース プロジェクトのオブジェクト モデルの拡張](../../extensibility/internals/extending-the-object-model-of-the-base-project.md)

  プロジェクト サブタイプでオートメーション エクステンダーを使用してオートメーション オブジェクト モデルを拡張する方法に関する情報を提供します。

- [[新しい項目の追加] ダイアログ ボックスへの投稿](../../extensibility/internals/contributing-to-the-add-new-item-dialog-box.md)

  **[新しい項目の追加]** ダイアログ ボックスに項目を追加する方法について説明します。

- [プロジェクト ファイルでのデータの保存](../../extensibility/saving-data-in-project-files.md)

  プロジェクト サブタイプで、マネージド パッケージ フレームワーク (MPF) を使用して、サブタイプ固有データをプロジェクト ファイルに保存および同ファイルから取得する方法について説明します。

- [特別な展開の処理](../../extensibility/internals/handling-specialized-deployment.md)

  プロジェクト サブタイプで、<xref:Microsoft.VisualStudio.Shell.Interop.IVsDeployableProjectCfg> インターフェイスを実装して特殊なデプロイ動作を提供する方法について説明します。

- [プロパティ ページの追加と削除](../../extensibility/adding-and-removing-property-pages.md)

  プロジェクト デザイナーでのプロパティ ページの追加と削除について説明します。

## <a name="related-sections"></a>関連項目

- [プロジェクトの種類](../../extensibility/internals/project-types.md)

  [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] プロジェクトについて詳しく説明したトピックへのリンクを提供します。
