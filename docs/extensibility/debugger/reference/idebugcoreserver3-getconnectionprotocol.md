---
title: "IDebugCoreServer3::GetConnectionProtocol |Microsoft ドキュメント"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- IDebugCoreServer3::GetConnectionProtocol
helpviewer_keywords:
- IDebugCoreServer3::GetConnectionProtocol
ms.assetid: 368ced5b-c5d9-4090-a5b4-26ff400d1a55
caps.latest.revision: 8
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
ms.sourcegitcommit: 5db97d19b1b823388a465bba15d057b30ff0b3ce
ms.openlocfilehash: da90a4143297af71ae85f10b10ca31c66f617e17
ms.lasthandoff: 02/22/2017

---
# <a name="idebugcoreserver3getconnectionprotocol"></a>IDebugCoreServer3::GetConnectionProtocol
サーバーとデバッグ パッケージ間の通信に使用されているプロトコルを示す値を返します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT GetConnectionProtocol(  
   CONNECTION_PROTOCOL* pProtocol  
);  
```  
  
```c#  
int GetConnectionProtocol(  
   CONNECTION_PROTOCOL[] pProtocol  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `pProtocol`  
 [out]値のいずれかを返す、 [CONNECTION_PROTOCOL](../../../extensibility/debugger/reference/connection-protocol.md)列挙します。  
  
## <a name="return-value"></a>戻り値  
 成功した場合、返す`S_OK`。 そうしないと、エラー コードを返します。  
  
## <a name="see-also"></a>関連項目  
 [IDebugCoreServer3](../../../extensibility/debugger/reference/idebugcoreserver3.md)   
 [CONNECTION_PROTOCOL](../../../extensibility/debugger/reference/connection-protocol.md)
