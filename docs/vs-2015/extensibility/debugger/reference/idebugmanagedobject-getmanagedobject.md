---
title: IDebugManagedObject::GetManagedObject |Microsoft Docs
ms.custom: ''
ms.date: 2018-06-30
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- IDebugManagedObject::GetManagedObject
helpviewer_keywords:
- IDebugManagedObject::GetManagedObject method
ms.assetid: 6abe1402-6aad-41e6-8ec1-ae12d5945992
caps.latest.revision: 10
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 13a69db8e3b8a892a441c65f2752607814221667
ms.sourcegitcommit: 55f7ce2d5d2e458e35c45787f1935b237ee5c9f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/22/2018
ms.locfileid: "47546806"
---
# <a name="idebugmanagedobjectgetmanagedobject"></a>IDebugManagedObject::GetManagedObject
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

このトピックの最新バージョンをご覧[IDebugManagedObject::GetManagedObject](https://docs.microsoft.com/visualstudio/extensibility/debugger/reference/idebugmanagedobject-getmanagedobject)します。  
  
管理対象のオブジェクトを表すインターフェイスを返します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT GetManagedObject(   
   IUnknown** ppManagedObject  
);  
```  
  
```cpp#  
int GetManagedObject(  
   out object ppManagedObject  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `ppManagedObject`  
 [out]管理対象のオブジェクトを表すインターフェイスを返します。  
  
## <a name="return-value"></a>戻り値  
 成功した場合、S_OK を返します。それ以外の場合、エラー コードを返します。  
  
## <a name="remarks"></a>Remarks  
 このメソッドから返されるインターフェイスは、そのメソッドを呼び出せるように、マネージ クラスによって実装されるインターフェイスの照会できます。  
  
## <a name="see-also"></a>関連項目  
 [IDebugManagedObject](../../../extensibility/debugger/reference/idebugmanagedobject.md)

