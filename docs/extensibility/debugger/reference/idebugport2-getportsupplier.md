---
title: "IDebugPort2::GetPortSupplier |Microsoft ドキュメント"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- IDebugPort2::GetPortSupplier
helpviewer_keywords:
- IDebugPort2::GetPortSupplier
ms.assetid: 7a7b0615-df6b-4726-ab35-39dfa1ebed8f
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
ms.openlocfilehash: 675529c920c933aae9425de9b3a90c40bbbe71a6
ms.lasthandoff: 02/22/2017

---
# <a name="idebugport2getportsupplier"></a>IDebugPort2::GetPortSupplier
このポートのポートのサプライヤーを取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT GetPortSupplier(   
   IDebugPortSupplier2** ppSupplier  
);  
```  
  
```c#  
int GetPortSupplier(   
   out IDebugPortSupplier2 ppSupplier  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `ppSupplier`  
 [out]返します。、 [IDebugPortSupplier2](../../../extensibility/debugger/reference/idebugportsupplier2.md)オブジェクトは、ポートのポートのサプライヤーを表します。  
  
## <a name="return-value"></a>戻り値  
 成功した場合、返す`S_OK`。 そうしないと、エラー コードを返します。  
  
## <a name="see-also"></a>関連項目  
 [IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md)   
 [IDebugPortSupplier2](../../../extensibility/debugger/reference/idebugportsupplier2.md)
