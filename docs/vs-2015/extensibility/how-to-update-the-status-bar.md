---
title: '方法: ステータス バーの更新 |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], legacy - update status bar
ms.assetid: 7500c8a7-4913-4818-a88b-bfd1b9887cb6
caps.latest.revision: 13
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: bf96d13f3791570b5f1f98e77411ed64db81fa4d
ms.sourcegitcommit: 1fc6ee928733e61a1f42782f832ead9f7946d00c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2019
ms.locfileid: "60099404"
---
# <a name="how-to-update-the-status-bar"></a>方法: ステータス バーを更新します。
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

**ステータス バー**状態テキストの行または評価指標の 1 つまたは複数を含む多くのアプリケーション ウィンドウの下部にあるコントロール バーがあります。  
  
### <a name="to-update-the-status-bar"></a>ステータス バーを更新するには  
  
1. 実装<xref:Microsoft.VisualStudio.Shell.Interop.IVsStatusbarUser>フォーム ビューとコード ビューなど、エディターを提供する各個々 のビュー オブジェクト (DocView)。  
  
2. IDE を呼び出すと<xref:Microsoft.VisualStudio.Shell.Interop.IVsStatusbarUser.SetInfo%2A>の情報を更新、**ステータス バー**のメソッドを呼び出して、<xref:Microsoft.VisualStudio.Shell.Interop.IVsStatusbarUser>します。  
  
    > [!NOTE]
    >  IDE 呼び出し<xref:Microsoft.VisualStudio.Shell.Interop.IVsStatusbarUser.SetInfo%2A>のみ、ドキュメント ウィンドウが最初に有効な場合。 ドキュメント ウィンドウがアクティブになっている時間の残りの部分を更新する必要があります、**ステータス バー**エディターの変更の状態と情報。  
  
## <a name="robust-programming"></a>信頼性の高いプログラミング  
 A**ステータス バー** 4 つの個別のフィールドが含まれています。  
  
- 状態テキスト  
  
- 進行状況バー  
  
- アニメーション化されたアイコン  
  
- エディターについて  
  
  詳細については、次を参照してください。[ステータス バー](http://msdn.microsoft.com/library/fcbc5029-1aab-4e14-adf7-419038a4935e)します。  
  
  IDE を自動的に呼び出す、<xref:Microsoft.VisualStudio.Shell.Interop.IVsStatusbarUser.SetInfo%2A>のメソッド、<xref:Microsoft.VisualStudio.Shell.Interop.IVsStatusbarUser>実装、ドキュメント ウィンドウがアクティブになります。  
  
  VSPackage の実装者は、ステータス バーで、ステータス テキストを更新します。 状態のテキスト フィールドが空のテキストに設定されている場合、IDE が「準備完了」には、この文字列をリセットします ("") のアイドル時間にします。  
  
## <a name="see-also"></a>関連項目  
 [ステータス バー](http://msdn.microsoft.com/library/fcbc5029-1aab-4e14-adf7-419038a4935e)
