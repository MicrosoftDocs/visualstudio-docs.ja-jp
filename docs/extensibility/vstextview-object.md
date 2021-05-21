---
title: VSTextView オブジェクト | Microsoft Docs
description: VSTextView オブジェクトは、ユーザーがテキスト バッファーの Unicode テキストを表示し、編集することができるウィンドウです。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- VSTextView
helpviewer_keywords:
- VSTextView object, reference
- views [Visual Studio SDK], reference
ms.assetid: 78272ddc-9718-4c65-a94e-a44a2e8d54f4
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 1a7ec65ed2beb866bfbb4e35fd5b290d3457ad3a
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105062162"
---
# <a name="vstextview-object"></a>VSTextView オブジェクト

テキスト ビューは、ユーザーがテキスト バッファーの Unicode テキストを表示し、編集することができるウィンドウです。 基本的に、ビューはほとんどのユーザーがエディターと呼ぶものです。 ビューはさまざまなテキスト レイヤー (右端での折り返し、テキストのアウトライン化など) によってバッファーから分離されているため、ビューがバッファー内のテキストを正確に表すとは限りません。 テキスト ビューの詳細については、「[レガシ API を使用するテキスト ビューへのアクセス](/previous-versions/visualstudio/visual-studio-2015/extensibility/accessing-thetext-view-by-using-the-legacy-api?preserve-view=true&view=vs-2015)」を参照してください。

<xref:Microsoft.VisualStudio.TextManager.Interop.VsTextView> オブジェクト内のインターフェイスを次の表に示します。

|インターフェイス|説明|
|---------------|-----------------|
|[IDropSource](/windows/desktop/api/oleidl/nn-oleidl-idropsource)|標準の OLE インターフェイス。|
|<xref:Microsoft.VisualStudio.OLE.Interop.IDropTarget>|標準の OLE インターフェイス。|
|<xref:Microsoft.VisualStudio.OLE.Interop.IObjectWithSite>|標準の OLE インターフェイス。|
|<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>|標準の OLE インターフェイス。|
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsCompoundAction>|複合アクション (つまり、1 つの元に戻すとやり直しの単位にグループ化されたアクション) の作成を可能にします。|
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView>|ビューの管理とアクセスのための基本的なメソッドが用意されています。 `IVsTextView` はスレッド セーフではありません。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowPane>|ウィンドウ ペインを作成および管理します。|
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsLayeredTextView>|テキスト レイヤーと対話します。|
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsThreadSafeTextView>|別のスレッドからビューに対して操作を実行します。|

## <a name="see-also"></a>こちらもご覧ください

- [図形の編集](https://www.microsoft.com/download/details.aspx?id=55984)
- [VSTextBuffer オブジェクト](../extensibility/vstextbuffer-object.md)