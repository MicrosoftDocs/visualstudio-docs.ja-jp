---
title: IEnumDebugPorts2::GetCount |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IEnumDebugPorts2::GetCount
helpviewer_keywords:
- IEnumDebugPorts2::GetCount
ms.assetid: d714455c-e4fc-48dc-a6d4-7e8b5d7c1bce
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 46b000ffefcd8b2277b87cbda3b5c5fafba0a1c0
ms.sourcegitcommit: 8b538eea125241e9d6d8b7297b72a66faa9a4a47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/23/2019
ms.locfileid: "58974709"
---
# <a name="ienumdebugports2getcount"></a>IEnumDebugPorts2::GetCount
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

列挙体の要素の数を返します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT GetCount(  
   ULONG* pcelt  
);  
```  
  
```csharp  
int GetCount(  
   out uint pcelt  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `pcelt`  
 [out]列挙体の要素の数を返します。  
  
## <a name="return-value"></a>戻り値  
 成功した場合、返します`S_OK`、それ以外のエラー コードを返します。  
  
## <a name="remarks"></a>Remarks  
 このメソッドだけを指定する、よく使用される列挙型の COM インターフェイスの一部でない、 `Next`、 `Clone`、 `Skip`、および`Reset`メソッドを実装する必要があります。  
  
## <a name="see-also"></a>関連項目  
 [IEnumDebugPorts2](../../../extensibility/debugger/reference/ienumdebugports2.md)
