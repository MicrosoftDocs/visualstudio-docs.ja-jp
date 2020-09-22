---
title: 'IDebugProcess2:: GetAttachedSessionName |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugProcess2::GetAttachedSessionName
helpviewer_keywords:
- IDebugProcess2::GetAttachedSessionName
ms.assetid: 7e5e116f-2c0c-4bc8-ad3f-e9fd2318a7e4
caps.latest.revision: 14
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 3acc40e2b906bd46b832d9fa11578de346014042
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "90841468"
---
# <a name="idebugprocess2getattachedsessionname"></a>IDebugProcess2::GetAttachedSessionName
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

このプロセスをデバッグしているセッションの名前を取得します。 IDE では、特定のコンピューターで特定のプロセスをデバッグしているユーザーにこの情報を表示できます。  
  
> [!NOTE]
> このメソッドは非推奨とされ、その実装は常にを返す必要があり `E_NOTIMPL` ます。  
  
## <a name="syntax"></a>構文  
  
```  
HRESULT GetAttachedSessionName(  
   BSTR* pbstrSessionName  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `pbstrSessionName`  
  
## <a name="return-value"></a>戻り値  
 このメソッドは常にを返す必要があり `E_NOTIMPL` ます。  
  
## <a name="see-also"></a>参照  
 [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)
