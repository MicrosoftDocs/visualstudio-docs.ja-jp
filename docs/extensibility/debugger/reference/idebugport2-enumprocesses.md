---
title: "IDebugPort2::EnumProcesses |Microsoft ドキュメント"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- IDebugPort2::EnumProcesses
helpviewer_keywords:
- IDebugPort2::EnumProcesses
ms.assetid: aafb32c5-5790-4807-a448-878a80256438
caps.latest.revision: 10
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
ms.openlocfilehash: 15f31118b114819fac63b1cc9c8b1b0e66f353b0
ms.lasthandoff: 02/22/2017

---
# <a name="idebugport2enumprocesses"></a>IDebugPort2::EnumProcesses
ポートで実行されているすべてのプロセスの一覧を返します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT EnumProcesses(   
   IEnumDebugProcesses2** ppEnum  
);  
```  
  
```c#  
int EnumProcesses(   
   out IEnumDebugProcesses2 ppEnum  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `ppEnum`  
 [out]返します。、 [IEnumDebugProcesses2](../../../extensibility/debugger/reference/ienumdebugprocesses2.md)ポートで実行されているすべてのプロセスの一覧を含むオブジェクト。  
  
## <a name="return-value"></a>戻り値  
 成功した場合、返す`S_OK`。 そうしないと、エラー コードを返します。  
  
## <a name="see-also"></a>関連項目  
 [IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md)   
 [IEnumDebugProcesses2](../../../extensibility/debugger/reference/ienumdebugprocesses2.md)
