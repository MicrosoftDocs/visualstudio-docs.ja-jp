---
title: プロジェクトとエディターの追加のソース制御のガイドライン |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control [Visual Studio SDK], guidelines for projects and editors
ms.assetid: 2483cce5-321c-4d3c-9c5c-ee8385263f74
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 3566709819d2023dfd6e38e40f88a454de83e3e6
ms.sourcegitcommit: d0425b6b7d4b99e17ca6ac0671282bc718f80910
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/21/2019
ms.locfileid: "56626103"
---
# <a name="additional-source-control-guidelines-for-projects-and-editors"></a>プロジェクトとエディターの追加のソース制御のガイドライン
プロジェクトとエディター ソース管理をサポートするために従う必要があるガイドラインを数多くあります。

## <a name="guidelines"></a>ガイドライン
 プロジェクトまたはエディターでは、次をソース管理をサポートするためにもを実行する必要があります。

|区分|Project|エディター|説明|
|----------|-------------|------------|-------------|
|ファイルのプライベート コピー|x||環境には、ファイルのプライベート コピーがサポートされています。 これは、プロジェクトに参加している各ユーザーにそのプロジェクト内のファイルの自分独自のプライベート コピーします。|
|ANSI または Unicode の永続化|x|x|永続化コードを記述する場合は、ほとんどのソース管理プログラムは、Unicode を現在サポートしていないため、ANSI 形式でファイルを永続化します。|
|ファイルを列挙します。|x||プロジェクト内のすべてのファイルの特定のリストを含める必要がありを使用してファイルの一覧を列挙できる必要があります、<xref:Microsoft.VisualStudio.Shell.Interop.IVsSccProject2>または<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.GetProperty%2A>(VSH_PROPID_First_Child/Next_Sibling)。 プロジェクトがを通じて項目名を公開する必要がありますもその<xref:Microsoft.VisualStudio.Shell.Interop.IVsProject.GetMkDocument%2A>実装とサポートの名前参照 (特殊なファイルを含む) をその<xref:Microsoft.VisualStudio.Shell.Interop.IVsProject.IsDocumentInProject%2A>実装します。|
|テキストの形式|x|x|可能であれば、ファイルは、異なるバージョンのマージをサポートするテキスト形式でなければなりません。 テキスト形式でないファイルは、ファイルの他のバージョンと後でマージすることはできません。 任意のテキスト形式には XML です。|
|参照に基づく|x||ソース管理では、参照ベースのプロジェクトはサポートされてすぐにします。 ただし、ディレクトリ ベースのプロジェクトは、プロジェクトは、それらのファイルがディスクに存在するかどうかに関係なく、オンデマンドでそのファイルの一覧を作成できる限りもソース コントロールによってサポートされます。 ソース管理からプロジェクトを開くときにそのファイルの前に、最初、プロジェクト ファイルが終了します。|
|オブジェクトと予測可能な順序でプロパティを保存します。|x|x|マージするためのアルファベット順などの予測可能な順序でファイルを維持します。|
|再読み込み|x|x|ファイルがディスクに変更されると、エディターが再読み込みできる必要があります。 環境のデータを呼び出すことによって再読み込みはソース管理に参加すると、<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData2.ReloadDocData%2A>実装します。 最も困難な再読み込み大文字と小文字が IVsQueryEditQuerySave を呼び出したときに、チェック アウトが発生した場合::<xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QueryEditFiles%2A>情報の処理とします。 ただし、再読み込みコードは、このような状況で実行できる必要があります。<br /><br /> 環境では、プロジェクト ファイルが自動的に再読み込みします。 ただし、プロジェクトを実装する必要があります<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem2>プロジェクト ファイルを再読み込みをサポートするために階層が入れ子になったに入れ子になった場合。|

## <a name="see-also"></a>関連項目
- [ソース管理をサポートします。](../../extensibility/internals/supporting-source-control.md)