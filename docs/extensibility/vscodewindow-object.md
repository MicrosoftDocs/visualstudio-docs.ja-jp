---
title: VSCodeWindow オブジェクト | Microsoft Docs
description: コード ウィンドウについて説明します。これは、1 つまたは複数のテキスト ビュー (通常は VsTextView オブジェクト) を含めることができる特殊なドキュメント ウィンドウです。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- VSCodeWindow
helpviewer_keywords:
- views [Visual Studio SDK], VSCodeWindow object
- VsCodeWindow object
ms.assetid: cf5fe926-e784-4098-bc01-cac49c7c55c6
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 77839bf80f30de3177f647795ffb89aa3e103d58
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105062422"
---
# <a name="vscodewindow-object"></a>VSCodeWindow オブジェクト
コード ウィンドウは、1 つまたは複数のテキスト ビュー (通常は <xref:Microsoft.VisualStudio.TextManager.Interop.VsTextView> オブジェクト) を含めることができる特殊なドキュメント ウィンドウです。

 アーキテクチャ的には、コード ウィンドウはウィンドウ フレーム内のドキュメント ウィンドウです。 機能的には、コード ウィンドウは追加機能を含む単なるドキュメント ウィンドウです。 マルチドキュメント インターフェイス (MDI) モードでは、コード ウィンドウは MDI の子フレームです。 詳細については、「[レガシ API を使用したコード ウィンドウのカスタマイズ](/previous-versions/visualstudio/visual-studio-2015/extensibility/customizing-code-windows-by-using-the-legacy-api?preserve-view=true&view=vs-2015)」を参照してください。

 <xref:Microsoft.VisualStudio.TextManager.Interop.VsCodeWindow> オブジェクトのインターフェイスを次の表に示します。

|メソッド|説明|
|------------|-----------------|
|<xref:Microsoft.VisualStudio.OLE.Interop.IServiceProvider>|グローバル一意識別子 (GUID) によって識別されるサービスを検索するための汎用アクセス機構を提供します。|
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindow>|1 つ以上のコード ビューを含むマルチドキュメント インターフェイス (MDI) の子を表します。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowPane>|ウィンドウ フレームを塗りつぶします。|

## <a name="see-also"></a>関連項目
- <xref:Microsoft.VisualStudio.OLE.Interop.IServiceProvider>
- [図形の編集](https://www.microsoft.com/download/details.aspx?id=55984)