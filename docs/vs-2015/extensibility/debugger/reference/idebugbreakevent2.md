---
title: IDebugBreakEvent2 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugBreakEvent2
helpviewer_keywords:
- IDebugBreakEvent2 interface
ms.assetid: 57dfdbc2-4e68-4dbf-9579-006cd6fb1c62
caps.latest.revision: 14
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 4858d5086baf65b9d3e1e7c28fbd0d1707403412
ms.sourcegitcommit: 8b538eea125241e9d6d8b7297b72a66faa9a4a47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/23/2019
ms.locfileid: "58972819"
---
# <a name="idebugbreakevent2"></a>IDebugBreakEvent2
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

このインターフェイスは、非同期の中断が正常に完了したことをセッション デバッグ マネージャー (SDM) に指示します。  
  
## <a name="syntax"></a>構文  
  
```  
IDebugBreakEvent2 : IUnknown  
```  
  
## <a name="notes-for-implementers"></a>実装についてのメモ  
 デでは、プログラムでユーザーの中断をサポートするためにこのインターフェイスを実装します。 [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)このインターフェイスと同じオブジェクトでインターフェイスを実装する必要があります (、SDM を使用して[QueryInterface](http://msdn.microsoft.com/library/62fce95e-aafa-4187-b50b-e6611b74c3b3)にアクセスする、`IDebugEvent2`インターフェイス)。  
  
## <a name="notes-for-callers"></a>呼び出し元のノート  
 SDM コール[CauseBreak](../../../extensibility/debugger/reference/idebugprogram2-causebreak.md)ユーザーが一時停止するデバッグ中のプログラムを要求された場合。 プログラムが正常に一時停止されて、DE 送信、`IDebugBreakEvent2`イベント。 このイベントを使用して、送信、 [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)デバッグ中のプログラムに添付するときに、SDM によって提供されるコールバック関数。  
  
## <a name="remarks"></a>Remarks  
 たとえば、ユーザーが選択できる、**すべて中断**コマンドを**デバッグ**無限ループを実行しているプログラムから抜け出すメニュー。 プログラムに対して呼び出すことによって停止を指示、SDM [CauseBreak](../../../extensibility/debugger/reference/idebugprogram2-causebreak.md)します。 DE 送信`IDebugBreakEvent2`プログラムが最後に停止します。  
  
## <a name="requirements"></a>必要条件  
 ヘッダー: msdbg.h  
  
 名前空間: Microsoft.VisualStudio.Debugger.Interop  
  
 アセンブリ:Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>関連項目  
 [CauseBreak](../../../extensibility/debugger/reference/idebugprogram2-causebreak.md)   
 [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)   
 [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)
