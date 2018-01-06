---
title: "IDebugManagedObject::SetFromManagedObject |Microsoft ドキュメント"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology: vs-ide-sdk
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: IDebugManagedObject::SetFromManagedObject
helpviewer_keywords: IDebugManagedObject::SetFromManagedObject method
ms.assetid: 8700ee8d-2704-4580-bccc-046837a24edd
caps.latest.revision: "9"
author: gregvanl
ms.author: gregvanl
manager: ghogen
ms.workload: vssdk
ms.openlocfilehash: da0526c060175a6e00a7b45a7ef2e347dba0d89e
ms.sourcegitcommit: 32f1a690fc445f9586d53698fc82c7debd784eeb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/22/2017
---
# <a name="idebugmanagedobjectsetfrommanagedobject"></a>IDebugManagedObject::SetFromManagedObject
パラメーターとして指定する値クラスのインスタンスから値クラスのオブジェクトのインスタンスの値を設定します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT SetFromManagedObject(   
   IUnknown* pManagedObject  
);  
```  
  
```csharp  
int SetFromManagedObject(  
   object pManagedObject  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `pManagedObject`  
 [in]新しい値を含むマネージ オブジェクトを表すインターフェイスです。  
  
## <a name="return-value"></a>戻り値  
 成功した場合、S_OK を返します。それ以外の場合、エラー コードを返します。  
  
## <a name="remarks"></a>コメント  
 このメソッドで表される管理対象オブジェクトを変更するのには使用、 [IDebugManagedObject](../../../extensibility/debugger/reference/idebugmanagedobject.md)オブジェクト。  
  
## <a name="see-also"></a>参照  
 [IDebugManagedObject](../../../extensibility/debugger/reference/idebugmanagedobject.md)