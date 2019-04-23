---
title: '方法: テキスト バッファー イベント、レガシ API の登録 |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], legacy - register for text buffer events
ms.assetid: 5fc00ced-882c-4b48-b46c-1fa5a2469f94
caps.latest.revision: 14
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 5f36e8dd780788d241e3c286b1bbbe581311b143
ms.sourcegitcommit: 1fc6ee928733e61a1f42782f832ead9f7946d00c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2019
ms.locfileid: "60062684"
---
# <a name="how-to-register-for-text-buffer-events-with-the-legacy-api"></a>方法: テキスト バッファー イベント、レガシ API の登録します。
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

テキスト バッファーを従来の API を使用してアクセスする場合は、テキスト バッファー イベント、次の手順で示すように登録してください。  
  
### <a name="to-advise-text-buffer-events"></a>テキスト バッファーのイベントを通知するには  
  
1. 上のインターフェイスのいずれかへのポインターから<xref:Microsoft.VisualStudio.TextManager.Interop.VsTextBuffer>、呼び出す`QueryInterface`へのポインターの<xref:Microsoft.VisualStudio.OLE.Interop.IConnectionPointContainer>します。  
  
2. 呼び出す、<xref:Microsoft.VisualStudio.OLE.Interop.IConnectionPointContainer.FindConnectionPoint%2A>メソッド、および登録するイベントのインターフェイス ID を渡します。  
  
     例では、登録する場合の<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLinesEvents>、インターフェイス ID の IID_IVsTextLinesEvents で渡します。  
  
     テキスト バッファーへのポインターを返します、<xref:Microsoft.VisualStudio.OLE.Interop.IConnectionPoint>適切な接続ポイント オブジェクトのインターフェイス。  
  
3. このポインターを使用して、呼び出し、<xref:Microsoft.VisualStudio.OLE.Interop.IConnectionPoint.Advise%2A>を登録する、たとえば、イベント インターフェイスの実装にポインターを渡し、メソッド、`IVsTextLinesEvents`インターフェイス。  
  
     環境が呼び出すことによってイベントのリッスンを中止し、使用できるクッキーを返します、<xref:Microsoft.VisualStudio.OLE.Interop.IConnectionPoint.Unadvise%2A>メソッド。  
  
## <a name="see-also"></a>関連項目  
 [レガシ API のテキスト バッファー イベント](../extensibility/text-buffer-events-in-the-legacy-api.md)
