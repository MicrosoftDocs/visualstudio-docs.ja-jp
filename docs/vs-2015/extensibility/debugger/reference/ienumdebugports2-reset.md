---
title: 'IEnumDebugPorts2:: Reset |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IEnumDebugPorts2::Reset
helpviewer_keywords:
- IEnumDebugPorts2::Reset
ms.assetid: 67da406c-eadb-421e-ae12-e26e9866f262
caps.latest.revision: 10
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: a59443b16b9c133744ee6a638e56c3850109061a
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68155057"
---
# <a name="ienumdebugports2reset"></a>IEnumDebugPorts2::Reset
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

列挙体を最初の要素にリセットします。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT Reset(  
   void  
);  
```  
  
```csharp  
int Reset();  
```  
  
## <a name="return-value"></a>戻り値  
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。  
  
## <a name="remarks"></a>注釈  
 このメソッドが呼び出された後 [、次のメソッドを](../../../extensibility/debugger/reference/ienumdebugports2-next.md) 呼び出すと、列挙体の最初の要素が返されます。  
  
## <a name="see-also"></a>参照  
 [IEnumDebugPorts2](../../../extensibility/debugger/reference/ienumdebugports2.md)
