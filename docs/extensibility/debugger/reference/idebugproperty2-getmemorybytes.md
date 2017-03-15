---
title: "IDebugProperty2::GetMemoryBytes |Microsoft ドキュメント"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- IDebugProperty2::GetMemoryBytes
helpviewer_keywords:
- IDebugProperty2::GetMemoryBytes
ms.assetid: b32042ed-7a06-4b4a-99ef-fe03b0aa61cc
caps.latest.revision: 9
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
ms.openlocfilehash: 52208276b8e2ca2d6fd7f98b0b497a6c7b237c31
ms.lasthandoff: 02/22/2017

---
# <a name="idebugproperty2getmemorybytes"></a>IDebugProperty2::GetMemoryBytes
プロパティの値を構成するメモリのバイトを取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT GetMemoryBytes (   
   IDebugMemoryBytes2** ppMemoryBytes  
);  
```  
  
```c#  
int GetMemoryBytes (   
   out IDebugMemoryBytes2 ppMemoryBytes  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `ppMemoryBytes`  
 [out]返します。、 [IDebugMemoryBytes2](../../../extensibility/debugger/reference/idebugmemorybytes2.md)プロパティの値を保持するメモリを取得するために使用できるオブジェクト。  
  
## <a name="return-value"></a>戻り値  
 成功した場合、返す`S_OK`です。 それ以外の場合エラー コードを返します。 返します。`S_GETMEMORYBYTES_NO_MEMORY_BYTES`取得するバイトのメモリがない場合。  
  
## <a name="see-also"></a>関連項目  
 [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)   
 [IDebugMemoryBytes2](../../../extensibility/debugger/reference/idebugmemorybytes2.md)
