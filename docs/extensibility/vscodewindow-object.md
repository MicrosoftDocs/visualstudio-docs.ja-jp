---
title: VSCodeWindow オブジェクト |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- VSCodeWindow
helpviewer_keywords:
- views [Visual Studio SDK], VSCodeWindow object
- VsCodeWindow object
ms.assetid: cf5fe926-e784-4098-bc01-cac49c7c55c6
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 8b1a3c19d349b84b10e0f36aca57a24aaac0d521
ms.sourcegitcommit: b0d8e61745f67bd1f7ecf7fe080a0fe73ac6a181
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/22/2019
ms.locfileid: "56688759"
---
# <a name="vscodewindow-object"></a>VSCodeWindow オブジェクト
コード ウィンドウは通常、1 つまたは複数のテキスト ビューを含めることができる特殊なドキュメント ウィンドウで、<xref:Microsoft.VisualStudio.TextManager.Interop.VsTextView>オブジェクト。

 アーキテクチャ上、コード ウィンドウには、ウィンドウ フレーム内では、ドキュメント ウィンドウです。 機能的には、コード ウィンドウは、機能が追加されたドキュメント ウィンドウだけです。 マルチ ドキュメント インターフェイス (MDI) モードでは、コード ウィンドウは、MDI 子フレームです。 詳細については、次を参照してください。[レガシ API を使用してコード ウィンドウをカスタマイズする](../extensibility/customizing-code-windows-by-using-the-legacy-api.md)します。

 次の表に、インターフェイス、<xref:Microsoft.VisualStudio.TextManager.Interop.VsCodeWindow>オブジェクト。

|メソッド|説明|
|------------|-----------------|
|<xref:Microsoft.VisualStudio.OLE.Interop.IServiceProvider>|グローバル一意識別子 (GUID) を識別するサービスを検索する汎用アクセス メカニズムを提供します。|
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindow>|1 つまたは複数のコード ビューを含む複数ドキュメント インターフェイス (MDI) 子を表します。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowPane>|ウィンドウ フレームを設定します。|

## <a name="see-also"></a>関連項目
- <xref:Microsoft.VisualStudio.OLE.Interop.IServiceProvider>
- [図の編集](https://www.microsoft.com/download/details.aspx?id=55984)