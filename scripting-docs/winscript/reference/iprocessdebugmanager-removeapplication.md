---
title: IProcessDebugManager::RemoveApplication |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IProcessDebugManager.RemoveApplication
apilocation:
- pdm.dll
helpviewer_keywords:
- IProcessDebugManager::RemoveApplication
ms.assetid: 334e869d-81ae-4d30-9e89-89763ad4f184
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 5c357fa5587d4fc5bf8c1752e20e7e0aa9df9835
ms.sourcegitcommit: d3a485d47c6ba01b0fc9878cbbb7fe88755b29af
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/19/2019
ms.locfileid: "58150700"
---
# <a name="iprocessdebugmanagerremoveapplication"></a>IProcessDebugManager::RemoveApplication
実行中のアプリケーションを削除します。 アプリケーションの一覧。  
  
## <a name="syntax"></a>構文  
  
```cpp
HRESULT RemoveApplication(  
   DWORD  dwAppCookie  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `dwAppCookie`  
 [in]によって提供される cookie`IProcessDebugManager::AddApplication`アプリケーションがアプリケーションの一覧に追加したときにします。  
  
## <a name="return-value"></a>戻り値  
 このメソッドは `HRESULT` を返します。 有効な値を次の表に示しますが、これ以外にもあります。  
  
|[値]|説明|  
|-----------|-----------------|  
|`S_OK`|メソッドが成功しました。|  
  
## <a name="remarks"></a>Remarks  
 このメソッドの実行からアプリケーションを削除するアプリケーションの一覧。  
  
## <a name="see-also"></a>関連項目  
 [Iprocessdebugmanager::addapplication](../../winscript/reference/iprocessdebugmanager-addapplication.md)   
 [IProcessDebugManager インターフェイス](../../winscript/reference/iprocessdebugmanager-interface.md)