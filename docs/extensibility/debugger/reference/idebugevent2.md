---
title: "IDebugEvent2 |Microsoft ドキュメント"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- IDebugEvent2
helpviewer_keywords:
- IDebugEvent2 interface
ms.assetid: de3d714d-96fb-4e12-b66b-a75391472153
caps.latest.revision: 11
ms.author: gregvanl
manager: ghogen
translation.priority.mt:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
translationtype: Machine Translation
ms.sourcegitcommit: ca7c86466fa23fb21a932f26dc24e37c71cf29b4
ms.openlocfilehash: cf76a596a42b166a7e19686ecbae5fe4ddd41ea4
ms.lasthandoff: 04/05/2017

---
# <a name="idebugevent2"></a>IDebugEvent2
このインターフェイスは、ブレークポイントで停止するなどの重要なデバッグ情報とデバッグ メッセージなどの重大でない情報の両方の通信に使用されます。  
  
## <a name="syntax"></a>構文  
  
```  
IDebugEvent2 : IUnknown  
```  
  
## <a name="notes-for-implementers"></a>実装についてのメモ  
 デバッグ エンジン (DE) とカスタム ポート サプライヤーは、その他のすべてのイベント インターフェイスと同じオブジェクトでこのインターフェイスを実装します。  
  
## <a name="notes-for-callers"></a>呼び出し元のノート  
 インターフェイスに指定された ID (IID) 引数を使用して[イベント](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)または[イベント](../../../extensibility/debugger/reference/idebugportevents2-event.md)、セッション デバッグ マネージャー (SDM) を呼び出す[QueryInterface](/cpp/atl/queryinterface)上、`IDebugEvent2`を適切なイベント インターフェイスを取得するインターフェイスです。  
  
## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド  
 次の表は、メソッドの`IDebugEvent2`します。  
  
|メソッド|説明|  
|------------|-----------------|  
|[GetAttributes](../../../extensibility/debugger/reference/idebugevent2-getattributes.md)|このデバッグ イベントの属性を取得します。|  
  
## <a name="remarks"></a>コメント  
 特定のイベント インターフェイスなど[IDebugBreakpointEvent2](../../../extensibility/debugger/reference/idebugbreakpointevent2.md)IDebugEvent2 インターフェイスから派生していませんが、上と同じオブジェクトを別のインターフェイスとして実装される代わりに、`IDebugEvent2`です。  
  
## <a name="requirements"></a>要件  
 ヘッダー: msdbg.h  
  
 Namespace: Microsoft.VisualStudio.Debugger.Interop  
  
 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>関連項目  
 [コア インターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)   
 [イベント](../../../extensibility/debugger/reference/idebugportevents2-event.md)   
 [イベント](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)
