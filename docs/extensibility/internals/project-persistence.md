---
title: プロジェクトの永続化 | Microsoft Docs
description: IPersistFileFormat を使用してファイルベースと非ファイルベースの両方のプロジェクト オブジェクトを永続化する場合など、プロジェクトの設計における永続化について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- persistence, projects
- projects [Visual Studio SDK], persistance
ms.assetid: 42907bcf-4e27-46bd-a8cb-01c2ccd2bde5
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 17b9fc40a93a926fde5edc28e93f7751b919611c
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2021
ms.locfileid: "112903647"
---
# <a name="project-persistence"></a>プロジェクトの永続化
永続化は、プロジェクトの設計上の主要な考慮事項です。 ほとんどのプロジェクトでは、ファイルを表すプロジェクト項目を使用します。[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] では、非ファイルベースのデータを持つプロジェクトもサポートされています。 プロジェクトで所有されるファイルとプロジェクト ファイルの両方を永続化する必要があります。 IDE により、プロジェクトは、それ自体またはプロジェクト項目を保存するように指示されます。

 プロジェクトのテンプレートは、プロジェクト ファクトリに渡されます。 テンプレートでは、特定のプロジェクト タイプの要件に従って、すべてのプロジェクト項目の初期化をサポートする必要があります。 これらのテンプレートは、後でプロジェクト ファイルとして保存し、ソリューション全体で IDE で管理できます。 詳細については、「[プロジェクト ファクトリを使用したプロジェクト インスタンスの作成](../../extensibility/internals/creating-project-instances-by-using-project-factories.md)」と「[ソリューション](../../extensibility/internals/solutions-overview.md)」を参照してください。

 プロジェクト項目は、ファイルベースの場合も、非ファイルベースの場合もあります。

- ファイルベースの項目は、ローカルにもリモートにもすることができます。 たとえば、C# の Web プロジェクトでは、リモート システム上のファイルへの接続はローカルに保持されますが、ファイル自体はリモート システムで保持されます。

- 非ファイルベースの項目は、データベースまたはリポジトリに項目を保存できます。

## <a name="commit-models"></a>コミット モデル
 プロジェクト項目が配置されている場所を決定したら、適切なコミット モデルを選択する必要があります。 たとえば、ローカル ファイルを使用したファイルベース モデルでは、各プロジェクトを自律的に保存できます。 リポジトリ モデルでは、1 つのトランザクションに複数の項目を保存できます。 詳細については、「[プロジェクト タイプのデザインの方針](../../extensibility/internals/project-type-design-decisions.md)」を参照してください。

 プロジェクトでは、ファイル名拡張子を決定するために、<xref:Microsoft.VisualStudio.Shell.Interop.IPersistFileFormat> インターフェイスを実装します。ここには、オブジェクトのクライアントで **[名前を付けて保存]** ダイアログ ボックスを実装できるようにする、つまり **[ファイルの種類]** ドロップダウン リストに入力して初期ファイル名拡張子を管理できるようにするための情報が表示されます。

 IDE では、プロジェクトの `IPersistFileFormat` インターフェイスを呼び出し、プロジェクトがプロジェクト項目を必要に応じて永続化する必要があることを示します。 そのため、オブジェクトは、そのファイルと形式のすべての側面を所有します。 これには、オブジェクトの形式の名前が含まれます。

 項目がファイルでない場合でも、`IPersistFileFormat` は非ファイルベース項目が永続化される方法を示します。 プロジェクト ファイル ([!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)] プロジェクトの場合は .vbp ファイル、[!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)] プロジェクトの場合は .vcproj ファイルなど) も永続化する必要があります。

 保存操作の場合、IDE では実行中のドキュメント テーブル (RDT) を調べ、階層により <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem> および <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem2> インターフェイスにコマンドが渡されます。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem.IsItemDirty%2A> メソッドは、項目が変更されているかどうかを判断するために実装されます。 項目が変更されている場合、<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem.SaveItem%2A> メソッドは変更された項目を保存するために実装されます。

 `IVsPersistHierarchyItem2` インターフェイスのメソッドを使用して、項目を再度読み込むことができるかどうかを判断し、項目を再度読み込める場合は再度読み込みます。 また、<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem2.IgnoreItemFileChanges%2A> メソッドを実装して、変更された項目が保存されずに破棄されるようにすることもできます。

## <a name="see-also"></a>関連項目
- [チェックリスト: 新しいプロジェクト タイプの作成](../../extensibility/internals/checklist-creating-new-project-types.md)
- [プロジェクト ファクトリを使用したプロジェクト インスタンスの作成](../../extensibility/internals/creating-project-instances-by-using-project-factories.md)
