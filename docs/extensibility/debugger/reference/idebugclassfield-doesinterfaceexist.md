---
title: IDebugClassField::DoesInterfaceExist |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugClassField::DoesInterfaceExist
helpviewer_keywords:
- IDebugClassField::DoesInterfaceExist method
ms.assetid: cc0c8642-1a76-4fda-a309-7018a34883c9
caps.latest.revision: 10
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 7884bff62321ed07c3a11a6db65855b1edea0adc
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "62922625"
---
# <a name="idebugclassfielddoesinterfaceexist"></a>IDebugClassField::DoesInterfaceExist
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

特定のインターフェイスは、クラスで定義されているかどうかを決定します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT DoesInterfaceExist(   
   LPCOLESTR pszInterfaceName  
);  
```  
  
```csharp  
int DoesInterfaceExist(  
   [In] string pszInterfaceName  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `pszInterfaceName`  
 [in]検索するインターフェイス名を含む文字列。  
  
## <a name="return-value"></a>戻り値  
 成功した場合は S_OK を返します、S_FALSE を返す場合は、インターフェイスは存在しません。それ以外の場合、エラー コードを返します。  
  
## <a name="remarks"></a>Remarks  
 有効で、このメソッドは、すべてのインターフェイスの列挙体を取得し、一致するインターフェイスの一覧を検索します。  
  
## <a name="see-also"></a>関連項目  
 [IDebugClassField](../../../extensibility/debugger/reference/idebugclassfield.md)
