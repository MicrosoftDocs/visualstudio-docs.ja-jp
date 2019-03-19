---
title: SCRIPTTHREADID 定数 |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- SCRIPTTHREADID
apilocation:
- scrobj.dll
helpviewer_keywords:
- SCRIPTTHREADID
ms.assetid: 1df9940c-ad0c-42d8-96b9-6a6abe2382e6
caps.latest.revision: 9
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: dfbb39d10d552141a68d40a7be3f1715a80f8f57
ms.sourcegitcommit: d3a485d47c6ba01b0fc9878cbbb7fe88755b29af
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/19/2019
ms.locfileid: "58158053"
---
# <a name="scriptthreadid-constants"></a>SCRIPTTHREADID 定数
スレッドの種類を指定するために使用します。  
  
## <a name="syntax"></a>構文  
  
```cpp
typedef DWORD SCRIPTTHREADID;  
```  
  
## <a name="constants"></a>定数  
  
|定数|[値]|説明|  
|--------------|-----------|-------------|  
|SCRIPTTHREADID_CURRENT|0xFFFFFFFD|現在実行中のスレッド。|  
|SCRIPTTHREADID_BASE|0xFFFFFFFE|基本スレッドです。つまり、これで、スクリプト エンジンのスレッドがインスタンス化されました。|  
|SCRIPTTHREADID_ALL|0 xffffffff|すべてのスレッド。|  
  
## <a name="remarks"></a>Remarks  
 `SCRIPTTHREADID`型によって使用されます`IActiveScript::GetCurrentScriptThreadID`、 `IActiveScript::GetScriptThreadID`、 `IActiveScript::GetScriptThreadState`、および`IActiveScript::InterruptScriptThread`、定数でのみ使用できますが、`IActiveScript::GetScriptThreadState`と`IActiveScript::InterruptScriptThread`します。  
  
## <a name="see-also"></a>関連項目  
 [IActiveScript::GetCurrentScriptThreadID](../../winscript/reference/iactivescript-getcurrentscriptthreadid.md)   
 [IActiveScript::GetScriptThreadID](../../winscript/reference/iactivescript-getscriptthreadid.md)   
 [IActiveScript::GetScriptThreadState](../../winscript/reference/iactivescript-getscriptthreadstate.md)   
 [IActiveScript::InterruptScriptThread](../../winscript/reference/iactivescript-interruptscriptthread.md)