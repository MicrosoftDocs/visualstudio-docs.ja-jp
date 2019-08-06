---
title: 'IDebugArrayObject:: GetDimensions |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugArrayObject::GetDimensions
helpviewer_keywords:
- IDebugArrayObject::GetDimensions method
ms.assetid: 113e0aff-9028-49d6-b104-9fe7be4772d7
caps.latest.revision: 10
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 09902c60f87cfb92d0f0778fcbd106ade4d8dac4
ms.sourcegitcommit: 9cfd3ef6c65f671a26322320818212a1ed5955fe
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/26/2019
ms.locfileid: "68197786"
---
# <a name="idebugarrayobjectgetdimensions"></a>IDebugArrayObject::GetDimensions
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

配列の次元を取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT GetDimensions(   
   DWORD dwCount,  
   DWORD dwDimensions[]  
);  
```  
  
```csharp  
int GetDimensions(  
   [In] uint    dwCount,   
   [Out] uint[] dwDimensions  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `dwCount`  
 から取得する次元の数。  
  
 `dwDimensions`  
 [入力、出力]各次元のサイズを格納する配列。 `dwCount``dwDimensions`配列の最大サイズを指定します。  
  
## <a name="return-value"></a>戻り値  
 成功した場合、は S_OK を返します。それ以外の場合は、エラーコードを返します。  
  
## <a name="remarks"></a>Remarks  
 多次元配列のサイズは、次元ごとに異なる場合があります。 たとえば、3次元配列`myarray[3][2][6]`の場合、このメソッドは、パラメーターの`dwDimensions` 3、2、および6をこの順序で返します。  
  
## <a name="see-also"></a>関連項目  
 [IDebugArrayObject](../../../extensibility/debugger/reference/idebugarrayobject.md)
