---
title: VSCodeWindowManager オブジェクト | Microsoft Docs
description: VSCodeWindowManager オブジェクトについて説明します。これは、ドロップダウン バーなどの修飾を管理する責任を担います。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- VSCodeWindowManager
helpviewer_keywords:
- VsCodeWindowManager object
- views [Visual Studio SDK], VSCodeWindowManager object
ms.assetid: e313add5-afdb-4d8d-abd1-764e1fc10c44
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 76ab3d2a72c957b20a79850dc312f5c16de98afc
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2021
ms.locfileid: "112905294"
---
# <a name="vscodewindowmanager-object"></a>VSCodeWindowManager オブジェクト

この言語サービスにより、コード ウィンドウ マネージャーが実装されます。これは、修飾 (たとえば、ドロップダウン バー) を管理する責任を担います。 詳細については、「[レガシ API を使用したコード ウィンドウのカスタマイズ](/previous-versions/visualstudio/visual-studio-2015/extensibility/customizing-code-windows-by-using-the-legacy-api?preserve-view=true&view=vs-2015)」を参照してください。

次の表は、`VSCodeWindowManager` オブジェクト内のインターフェイスを示しています。

|インターフェイス|説明|
|---------------|-----------------|
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindowManager>|コード ウィンドウとの間で修飾 (ドロップダウン バーなど) の追加または削除を許可します。|