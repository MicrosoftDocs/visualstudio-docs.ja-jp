---
title: ソース管理ストアをローカルのプロジェクト フォルダーの比較 (オプション) |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- source control plug-ins, comparing versions
- source control plug-ins, local project folders
ms.assetid: 65217e8b-15a6-4446-92b0-4cff1c6220f5
caps.latest.revision: 15
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: be26b4195e0db7b3b78fcc2223ff2a6f8bde47d3
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63438939"
---
# <a name="optional-comparison-of-local-project-folder-to-source-control-store"></a>ソース管理ストアとローカルのプロジェクト フォルダーとの比較 (オプション)
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

ソースの制御関数を使用して、ローカルのプロジェクト フォルダーとソース管理の間の比較が行われますプラグイン API 1.2 [SccDirQueryInfo](../../extensibility/sccdirqueryinfo-function.md)と[SccDirDiff](../../extensibility/sccdirdiff-function.md)します。  
  
 内で**ソリューション エクスプ ローラー**、個々 のファイルではなく、フォルダーが選択されている場合、**バージョンを比較**ショートカット メニューを起動、新しい[SccDirQueryInfo](../../extensibility/sccdirqueryinfo-function.md)と[SccDirDiff](../../extensibility/sccdirdiff-function.md)ソース管理プラグインでします。  
  
## <a name="new-capability-flags"></a>新しい機能フラグ  
 `SCC_CAP_DIRECTORYDIFF`  
  
 `SCC_CAP_DIRECTORYCHECKOUT`  
  
## <a name="new-functions"></a>新しい関数  
 [SccDirDiff](../../extensibility/sccdirdiff-function.md)  
  
 [SccDirQueryInfo](../../extensibility/sccdirqueryinfo-function.md)  
  
 `SccDirQueryInfo`関数は、前に呼び出されます`SccDirDiff`作業ディレクトリがソース管理の対象を判断します。 `SccDirDiff`関数は、現在のローカル ディレクトリと、対応するソース管理フォルダーの相違を表示します。 このコマンドは、ソース管理、ディレクトリに変更の一覧を表示するプラグインを確認します。 ソース管理プラグインは、相違点を表示する独自の UI を提供します。  
  
> [!NOTE]
> この関数と同じコマンド フラグを使用して[SccDiff](../../extensibility/sccdiff-function.md)します。 ソース管理プラグイン プロバイダーとしては、ディレクトリの"クイック diff"操作をサポートすることができます。  
  
## <a name="see-also"></a>関連項目  
 [ソース管理プラグイン API バージョン 1.2 の新機能](../../extensibility/internals/what-s-new-in-the-source-control-plug-in-api-version-1-2.md)
