---
title: IDebugOutputStringEvent2 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugOutputStringEvent2
helpviewer_keywords:
- IDebugOutputStringEvent2 interface
ms.assetid: 86596fd1-cecc-4813-8add-dc3d70068f9b
caps.latest.revision: 13
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: fa62889e2af87325c124fa8e8af1cd9cc4cff253
ms.sourcegitcommit: 8b538eea125241e9d6d8b7297b72a66faa9a4a47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/23/2019
ms.locfileid: "58963529"
---
# <a name="idebugoutputstringevent2"></a>IDebugOutputStringEvent2
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

このインターフェイスは、文字列を出力する、デバッグ エンジン (DE) によって、セッション デバッグ マネージャー (SDM) に送信されます。  
  
## <a name="syntax"></a>構文  
  
```  
IDebugOutputStringEvent2 : IUnknown  
```  
  
## <a name="notes-for-implementers"></a>実装についてのメモ  
 文字列を送信するには、このインターフェイスを実装する、DE、**出力**IDE のウィンドウ。 [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)このインターフェイスと同じオブジェクトでインターフェイスを実装する必要があります。 SDM を使用して[QueryInterface](http://msdn.microsoft.com/library/62fce95e-aafa-4187-b50b-e6611b74c3b3)にアクセスする、`IDebugEvent2`インターフェイス。  
  
## <a name="notes-for-callers"></a>呼び出し元のノート  
 デは作成し、文字列を送信するには、このイベント オブジェクトを送信します、**出力**ウィンドウ。 使用して、イベントが送信される、 [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)デバッグ中のプログラムにアタッチされているときに、SDM によって指定されたコールバック関数。  
  
## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド  
 次の表は、メソッドの`IDebugOutputStringEvent2`します。  
  
|メソッド|説明|  
|------------|-----------------|  
|[GetString](../../../extensibility/debugger/reference/idebugoutputstringevent2-getstring.md)|表示可能なメッセージを取得します。|  
  
## <a name="remarks"></a>Remarks  
 たとえば、アンマネージ コードで出力される文字列開始できるはデバッグ中のプログラムは、Win32 に文字列を送信すると`OutputDebugString`関数。 この文字列は、DE によって傍受ありとして SDM に送られる、`IDebugOutputStringEvent2`イベント。  
  
 使用[IDebugMessageEvent2](../../../extensibility/debugger/reference/idebugmessageevent2.md)ユーザー応答を必要とするメッセージを送信します。  
  
 使用[IDebugErrorEvent2](../../../extensibility/debugger/reference/idebugerrorevent2.md)応答が不要なエラー メッセージを送信します。  
  
## <a name="requirements"></a>必要条件  
 ヘッダー: msdbg.h  
  
 名前空間: Microsoft.VisualStudio.Debugger.Interop  
  
 アセンブリ:Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>関連項目  
 [IDebugMessageEvent2](../../../extensibility/debugger/reference/idebugmessageevent2.md)   
 [IDebugErrorEvent2](../../../extensibility/debugger/reference/idebugerrorevent2.md)   
 [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)   
 [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)
