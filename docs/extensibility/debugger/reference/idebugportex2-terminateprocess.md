---
title: "IDebugPortEx2::TerminateProcess |Microsoft ドキュメント"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology: vs-ide-sdk
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: IDebugPortEx2::TerminateProcess
helpviewer_keywords: IDebugPortEx2::TerminateProcess
ms.assetid: bf8fa94c-6d9d-4e4f-ac08-3b44ba5ace68
caps.latest.revision: "10"
author: gregvanl
ms.author: gregvanl
manager: ghogen
ms.workload: vssdk
ms.openlocfilehash: e173e9ba6ae26086aae086eae5bd59530fb161cd
ms.sourcegitcommit: 32f1a690fc445f9586d53698fc82c7debd784eeb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/22/2017
---
# <a name="idebugportex2terminateprocess"></a>IDebugPortEx2::TerminateProcess
プロセスを終了します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT TerminateProcess(   
   IDebugProcess2* pPortProcess  
);  
```  
  
```csharp  
int TerminateProcess(   
   IDebugProcess2 pPortProcess  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `pPortProcess`  
 [in][IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)終了するプロセスを表すオブジェクト。  
  
## <a name="return-value"></a>戻り値  
 成功した場合を返します`S_OK`、それ以外のエラー コードを返します。  
  
## <a name="see-also"></a>参照  
 [IDebugPortEx2](../../../extensibility/debugger/reference/idebugportex2.md)   
 [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)