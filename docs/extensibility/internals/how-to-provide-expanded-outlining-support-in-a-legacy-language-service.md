---
title: 言語サービスでのアウトラインのサポートの提供 |Microsoft Docs
description: エディター制御のアウトライン領域、およびクライアント制御のアウトライン領域を追加して、従来の言語サービスでアウトラインの拡張サポートを提供する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- editors [Visual Studio SDK], outlining support
- language services, supporting outlining
- outlining, supporting
ms.assetid: df759e89-8193-418c-8038-6626304d387b
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 11d04af2afac04d4ec9ab197c3d3f7b5a15ad28c
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105078787"
---
# <a name="how-to-provide-expanded-outlining-support-in-a-legacy-language-service"></a>方法: 従来の言語サービスでのアウトラインの拡張サポートの提供
**[定義に縮小]** コマンドのサポートにとどまらず、言語のアウトラインのサポートを拡張する 2 つのオプションがあります。 エディター制御のアウトライン領域、およびクライアント制御のアウトライン領域を追加できます。

## <a name="adding-editor-controlled-outline-regions"></a>エディター制御のアウトライン領域の追加
 この方法でアウトライン領域を作成し、その領域の展開や折りたたみなどをエディターで処理できるようにします。 アウトライン サポートを提供する 2 つのオプションでは、このオプションのほうが堅牢性は低いです。 このオプションでは、<xref:Microsoft.VisualStudio.TextManager.Interop.IVsOutliningSession.AddOutlineRegions%2A> を使用して、特定の範囲のテキストに新しいアウトライン領域を作成します。 領域が作成されると、その動作はエディターによって制御されます。 エディター制御のアウトライン領域を実装するには、次の手順に従います。

### <a name="to-implement-an-editor-controlled-outline-region"></a>エディター制御のアウトライン領域を実装するには

1. <xref:Microsoft.VisualStudio.TextManager.Interop.SVsTextManager> に対して `QueryService` を呼び出します

     <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextManager> へのポインターが返されます。

2. <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextManager.GetHiddenTextSession%2A> を呼び出し、特定のテキスト バッファーへのポインターを渡します。 これで、バッファーの <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextSession> オブジェクトへのポインターが返されます。

3. <xref:Microsoft.VisualStudio.TextManager.Interop.IVsOutliningSession> へのポインターについて、<xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextSession> で <xref:System.Runtime.InteropServices.Marshal.QueryInterface%2A> を呼び出します。

4. <xref:Microsoft.VisualStudio.TextManager.Interop.IVsOutliningSession.AddOutlineRegions%2A> を呼び出して、一度に 1 つまたは複数のアウトライン領域を新しく追加します。

     この方法では、アウトラインにするテキストの範囲、既存のアウトライン領域を削除するか維持するか、アウトライン領域を既定で展開するか折りたたむかを指定できます。

## <a name="add-client-controlled-outline-regions"></a>クライアント制御のアウトライン領域の追加
 この方法を使用して、[!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)] および [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)] の言語サービスで使用されているような、クライアント制御 (またはスマート) のアウトラインを実装します。 独自のアウトラインを管理する言語サービスでは、古いアウトライン領域が無効になったときにそれを破棄し、必要に応じて新しいアウトライン領域を作成するため、テキスト バッファーの内容が監視されます。

### <a name="to-implement-a-client-controlled-outline-region"></a>クライアント制御のアウトライン領域を実装するには

1. <xref:Microsoft.VisualStudio.TextManager.Interop.SVsTextManager> に対して `QueryService` を呼び出します。 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextManager> へのポインターが返されます。

2. <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextManager.GetHiddenTextSession%2A> を呼び出し、特定のテキスト バッファーへのポインターを渡します。 これで、バッファーに隠し文字セッションが既に存在するかどうかが確認されます。

3. テキスト セッションが既に存在する場合は、作成する必要はなく、既存の <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextSession> オブジェクトへのポインターが返されます。 このポインターを使用して、アウトライン領域を列挙および作成します。 それ以外の場合は、<xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextManager.CreateHiddenTextSession%2A> を呼び出して、バッファーの隠し文字セッションを作成します。 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextSession> オブジェクトへのポインターが返されます。

    > [!NOTE]
    > <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextManager.CreateHiddenTextSession%2A> を呼び出す際に、隠し文字クライアント (つまり、<xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextClient> オブジェクト) を指定できます。 隠し文字やアウトライン領域がユーザーによって展開または折りたたまれている場合は、このクライアントによって通知されます。

4. <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextSession.AddHiddenRegions%2A> 構造体のパラメーターを呼び出します。非表示領域ではなく、アウトライン領域を作成することを示すには、<xref:Microsoft.VisualStudio.TextManager.Interop.NewHiddenRegion> 構造体の `iType` メンバーに <xref:Microsoft.VisualStudio.TextManager.Interop.HIDDEN_REGION_TYPE> の値を指定します。 <xref:Microsoft.VisualStudio.TextManager.Interop.NewHiddenRegion> 構造体の `dwBehavior` メンバーで、領域がクライアント制御であるか、またはエディター制御であるかを指定します。 スマート アウトラインの実装には、エディター制御およびクライアント制御のアウトライン領域を混在させることができます。 <xref:Microsoft.VisualStudio.TextManager.Interop.NewHiddenRegion> 構造体の `pszBanner` メンバーで、アウトライン領域が折りたたまれているときに表示されるバナー テキスト ("..." など) を指定します。 エディターにおける非表示領域の既定のバナー テキストは "..." です。
