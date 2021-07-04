---
title: 従来の言語サービスでの隠し文字サポートの提供
description: エディター制御の、またはクライアント制御の隠し文字領域を追加して、従来の言語サービスで隠し文字のサポートを提供する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- hidden text, supporting
- editors [Visual Studio SDK], hidden text
- language services, implementing hidden text regions
ms.assetid: 1c1dce9f-bbe2-4fc3-a736-5f78a237f4cc
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 31c62f50cfff8662c543d24dceabdb429a9b9b05
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2021
ms.locfileid: "112901787"
---
# <a name="how-to-provide-hidden-text-support-in-a-legacy-language-service"></a>方法: 従来の言語サービスでの隠し文字サポートの提供
アウトライン領域だけでなく、隠し文字領域も作成することができます。 隠し文字領域は、クライアントまたはエディターで制御でき、テキストの領域を完全に非表示にするために使用されます。 エディターでは、非表示領域は水平線で表示されます。 この例として、HTML エディターの **[スクリプトのみ]** ビューがあります。

## <a name="to-implement-a-hidden-text-region"></a>隠し文字領域を実装するには

1. <xref:Microsoft.VisualStudio.TextManager.Interop.SVsTextManager> に対して `QueryService` を呼び出します。

     <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextManager> へのポインターが返されます。

2. <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextManager.GetHiddenTextSession%2A> を呼び出し、特定のテキスト バッファーへのポインターを渡します。 これで、バッファーに隠し文字セッションが既に存在するかどうかが確認されます。

3. 既に存在する場合は、作成する必要はなく、既存の <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextSession> オブジェクトへのポインターが返されます。 このポインターを使用して、隠し文字領域を列挙および作成します。 それ以外の場合は、<xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextManager.CreateHiddenTextSession%2A> を呼び出して、バッファーの隠し文字セッションを作成します。

     <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextSession> オブジェクトへのポインターが返されます。

    > [!NOTE]
    > `CreateHiddenTextSession` を呼び出す際に、隠し文字クライアント (つまり、<xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextClient>) を指定できます。 隠し文字やアウトラインがユーザーによって展開または折りたたまれている場合は、隠し文字クライアントによって通知されます。

4. <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextSession.AddHiddenRegions%2A> を呼び出し、`reHidReg` (<xref:Microsoft.VisualStudio.TextManager.Interop.NewHiddenRegion>) パラメーターで次の情報を指定して、一度に 1 つまたは複数のアウトライン領域を新しく追加します。

    1. アウトライン領域ではなく、非表示領域を作成することを示すには、<xref:Microsoft.VisualStudio.TextManager.Interop.NewHiddenRegion> 構造体の `iType` メンバーに `hrtConcealed` の値を指定します。

        > [!NOTE]
        > 非表示の領域が非表示になっている場合、エディターでは、非表示領域の存在を示す線がその周囲に自動的に表示されます。

    2. <xref:Microsoft.VisualStudio.TextManager.Interop.NewHiddenRegion> 構造体の `dwBehavior` メンバーで、領域がクライアント制御であるか、エディター制御であるかを指定します。 スマート アウトライン実装では、エディターおよびクライアント制御のアウトラインと隠し文字領域を混在させることができます。
