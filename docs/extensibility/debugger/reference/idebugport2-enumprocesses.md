---
title: "IDebugPort2::EnumProcesses |Microsoft ドキュメント"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology: vs-ide-sdk
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: IDebugPort2::EnumProcesses
helpviewer_keywords: IDebugPort2::EnumProcesses
ms.assetid: aafb32c5-5790-4807-a448-878a80256438
caps.latest.revision: "10"
author: gregvanl
ms.author: gregvanl
manager: ghogen
ms.workload: vssdk
ms.openlocfilehash: 4ce702058c940b46075b524c781f662c62ec9aab
ms.sourcegitcommit: 32f1a690fc445f9586d53698fc82c7debd784eeb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/22/2017
---
# <a name="idebugport2enumprocesses"></a>IDebugPort2::EnumProcesses
ポートで実行されているすべてのプロセスの一覧を返します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT EnumProcesses(   
   IEnumDebugProcesses2** ppEnum  
);  
```  
  
```csharp  
int EnumProcesses(   
   out IEnumDebugProcesses2 ppEnum  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `ppEnum`  
 [out]返します、 [IEnumDebugProcesses2](../../../extensibility/debugger/reference/ienumdebugprocesses2.md)ポートで実行されているすべてのプロセスの一覧を含むオブジェクト。  
  
## <a name="return-value"></a>戻り値  
 成功した場合を返します`S_OK`、それ以外のエラー コードを返します。  
  
## <a name="see-also"></a>参照  
 [IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md)   
 [IEnumDebugProcesses2](../../../extensibility/debugger/reference/ienumdebugprocesses2.md)