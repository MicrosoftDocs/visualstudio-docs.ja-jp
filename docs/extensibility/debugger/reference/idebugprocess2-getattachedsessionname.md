---
title: "IDebugProcess2::GetAttachedSessionName |Microsoft ドキュメント"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology: vs-ide-sdk
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: IDebugProcess2::GetAttachedSessionName
helpviewer_keywords: IDebugProcess2::GetAttachedSessionName
ms.assetid: 7e5e116f-2c0c-4bc8-ad3f-e9fd2318a7e4
caps.latest.revision: "13"
author: gregvanl
ms.author: gregvanl
manager: ghogen
ms.workload: vssdk
ms.openlocfilehash: 8ca045a1fee17891fbe053d1d072a4affa41c787
ms.sourcegitcommit: 32f1a690fc445f9586d53698fc82c7debd784eeb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/22/2017
---
# <a name="idebugprocess2getattachedsessionname"></a>IDebugProcess2::GetAttachedSessionName
このプロセスのデバッグは、セッションの名前を取得します。 IDE では、特定のコンピューターに特定のプロセスのデバッグは、ユーザーにこの情報を表示できます。  
  
> [!NOTE]
>  このメソッドは廃止され、その実装を常に返します`E_NOTIMPL`です。  
  
## <a name="syntax"></a>構文  
  
```  
HRESULT GetAttachedSessionName(  
   BSTR* pbstrSessionName  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `pbstrSessionName`  
  
## <a name="return-value"></a>戻り値  
 このメソッドは常に返します`E_NOTIMPL`です。  
  
## <a name="see-also"></a>参照  
 [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)