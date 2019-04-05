---
title: ソース管理のサポート |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- source control [Visual Studio SDK], supporting
ms.assetid: 567acde3-354e-4f39-8d99-0ef86c103396
caps.latest.revision: 19
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: d1166197a5c79dcb0d1ddf4018227914346a6172
ms.sourcegitcommit: 8b538eea125241e9d6d8b7297b72a66faa9a4a47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/23/2019
ms.locfileid: "58973654"
---
# <a name="supporting-source-control"></a>ソース管理のサポート
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] ファイルのチェック アウト、チェックイン、およびプロジェクトまたはエディターの他のソース管理操作をサポートしています。 ソース管理クライアントでは、として[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]はソース管理パッケージでは、対話するように設計[!INCLUDE[vsvss](../../includes/vsvss-md.md)]、アーカイブ、バージョン管理、および、動的に定義された一連のファイルの制御機能を提供します。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [ソース管理パッケージのモデル](../../extensibility/internals/model-for-source-control-packages.md)  
 プロジェクトの種類を実装する必要がありますインターフェイスをについて説明します。 ソース管理をサポートするためにします。  
  
 [設計上の決定事項](../../extensibility/internals/source-control-design-decisions.md)  
 質問の回答を変更するプロジェクトの種類を実装する方法を提供します。  
  
 [構成の詳細](../../extensibility/internals/source-control-configuration-details.md)  
 プロジェクトの種類の実装がどのように変化ソース管理のサポートについて説明します。  
  
 [プロジェクトとエディターに関する追加のガイドライン](../../extensibility/internals/additional-source-control-guidelines-for-projects-and-editors.md)  
 プロジェクトの種類とエディターのベスト プラクティスをについて説明します。  
  
 [ランタイムの詳細](../../extensibility/internals/source-control-runtime-details.md)  
 ユーザーがソース管理システムに追加するときに、プロジェクトを登録する方法について説明します。  
  
## <a name="reference"></a>参照  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2>  
 環境またはソース管理パッケージ ファイルがメモリ内で変更または保存にすることを示します。  
  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccManager2>  
 プロジェクトとソース管理に登録して、ソース管理の状態に関する情報を取得する階層を使用できます。  
  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccProject2>  
 プロジェクト ファイルとプロジェクト項目のソース管理を提供するプロジェクト システムで実装されます。  
  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocuments2>  
 環境を追加、削除、またはファイルまたはソリューション内のディレクトリの名前を変更するアクセス許可を照会するプロジェクトで使用します。  
  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocumentsEvents2>  
 プロジェクト ファイルまたはディレクトリに加えられた変更のクライアントに通知します。  
  
## <a name="related-sections"></a>関連項目  
 [プロジェクト タイプ](../../extensibility/internals/project-types.md)  
 基本ビルディング ブロックとしてプロジェクトの概要、[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]統合開発環境 (IDE) です。 プロジェクトがビルドとコードのコンパイルを制御する方法を説明する追加のトピックへのリンクが提供されます。
