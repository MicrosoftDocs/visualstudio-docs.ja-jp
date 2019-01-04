---
title: IDebugProgram2::CanDetach |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- IDebugProgram2::CanDetach
helpviewer_keywords:
- IDebugProgram2::CanDetach
ms.assetid: dcd9ab6c-49e5-447e-aa7c-89f571f4a052
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 3c4c691da4b7f624b7d70f65ef59b537e8502251
ms.sourcegitcommit: 37fb7075b0a65d2add3b137a5230767aa3266c74
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/02/2019
ms.locfileid: "53916073"
---
# <a name="idebugprogram2candetach"></a>IDebugProgram2::CanDetach
デバッグ エンジン (DE) が、プログラムからデタッチできるかどうかを決定します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT CanDetach(  
   void  
);  
```  
  
```csharp  
int CanDetach();  
```  
  
## <a name="return-value"></a>戻り値  
 場合を返します、デタッチできます`S_OK`、それ以外のエラー コードを返します。 返します`S_FALSE`場合は、DE は、プログラムからデタッチできません。  
  
## <a name="see-also"></a>関連項目  
 [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)