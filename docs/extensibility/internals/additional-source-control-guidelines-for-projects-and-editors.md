---
title: プロジェクトとエディターのソース管理のガイドライン
description: ソース管理をサポートするためにプロジェクトとエディターで従う必要があるガイドラインについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control [Visual Studio SDK], guidelines for projects and editors
ms.assetid: 2483cce5-321c-4d3c-9c5c-ee8385263f74
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 2509f2f6f9da91c3df60d6b041d5ebb6bdd367b6
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105079008"
---
# <a name="additional-source-control-guidelines-for-projects-and-editors"></a>プロジェクトとエディターのソース管理のその他のガイドライン
ソース管理をサポートするためにプロジェクトとエディターで従う必要がある多くのガイドラインがあります。

## <a name="guidelines"></a>ガイドライン
 プロジェクトまたはエディターでは、ソース管理をサポートするために次のことも行う必要があります。

|領域|Project|エディター|詳細|
|----------|-------------|------------|-------------|
|ファイルのプライベート コピー|X||環境では、ファイルのプライベート コピーがサポートされます。 つまり、プロジェクトに登録されている各ユーザーは、そのプロジェクト内のファイルの独自のプライベート コピーを持っています。|
|ANSI/Unicode の永続性|X|X|永続するコードを記述する場合は、現在、ほとんどのソース管理プログラムで Unicode がサポートされないため、ANSI 形式でファイルを保持します。|
|ファイルの列挙|X||プロジェクトには、その中にあるすべてのファイルの特定のリストが含まれている必要があり、<xref:Microsoft.VisualStudio.Shell.Interop.IVsSccProject2> または <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.GetProperty%2A> (VSH_PROPID_First_Child/Next_Sibling) を使用してファイルのリストを列挙できる必要があります。 また、プロジェクトでは、<xref:Microsoft.VisualStudio.Shell.Interop.IVsProject.GetMkDocument%2A> の実装によって項目名が公開され、<xref:Microsoft.VisualStudio.Shell.Interop.IVsProject.IsDocumentInProject%2A> の実装によって名前参照 (特殊ファイルを含む) がサポートされる必要があります。|
|テキスト形式|X|X|可能な場合、異なるバージョンのマージをサポートするために、ファイルはテキスト形式である必要があります。 テキスト形式ではないファイルは、後で他のバージョンのファイルとマージできません。 推奨されるテキスト形式は XML です。|
|参照ベース|X||参照ベースのプロジェクトは、ソース管理で容易にサポートされます。 ただし、ファイルがディスク上に存在するかどうかに関係なく、プロジェクトで要求に応じてファイルのリストを生成できる限り、ディレクトリベースのプロジェクトもソース管理でサポートされます。 ソース管理からプロジェクトを開くと、それに含まれるファイルの前にプロジェクト ファイルがまずダウンロードされます。|
|オブジェクトとプロパティを予測可能な順序で保持する|X|X|マージを容易にするために、ファイルをアルファベット順などの予測可能な順序で保持します。|
|再読み込み|X|X|ディスク上でファイルが変更された場合、エディターで再読み込みできる必要があります。 ソース管理に参加している場合、環境では <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData2.ReloadDocData%2A> の実装を呼び出すことによって、データが再読み込みされます。 再読み込みが最も困難なケースは、IVsQueryEditQuerySave::<xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QueryEditFiles%2A> を呼び出して情報を処理しているときにチェックアウトが発生した場合です。 ただし、この状況で再読み込みのコードを実行できる必要があります。<br /><br /> 環境では、プロジェクト ファイルが自動的に再読み込みされます。 ただし、入れ子になったプロジェクト ファイルの再読み込みをサポートするために、入れ子になった階層がある場合は、プロジェクトで <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem2> を実装する必要があります。|

## <a name="see-also"></a>関連項目
- [ソース管理のサポート](../../extensibility/internals/supporting-source-control.md)
