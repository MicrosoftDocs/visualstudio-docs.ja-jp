---
title: IActiveScriptProfilerCallback2::OnFunctionEnterByName |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IActiveScriptProfilerCallback2::OnFunctionEnterByName
ms.assetid: 24b1593a-97fc-4d70-9b85-ec86fb59f987
caps.latest.revision: 6
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: f6fdb4addace1b0bbabdd4303c3943b976763514
ms.sourcegitcommit: d3a485d47c6ba01b0fc9878cbbb7fe88755b29af
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/19/2019
ms.locfileid: "58146098"
---
# <a name="iactivescriptprofilercallback2onfunctionenterbyname"></a>IActiveScriptProfilerCallback2::OnFunctionEnterByName
プロファイラー オブジェクトをドキュメント オブジェクト モデル (DOM) の関数呼び出しを実行しようとして、スクリプト エンジンに通知します。  
  
## <a name="syntax"></a>構文  
  
```cpp
HRESULT OnFunctionEnterByName(  
    [in] [string] const WCHAR *pwszFunctionName,  
    [in] PROFILER_SCRIPT_TYPE scriptType);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `pwszFunctionName`  
 [in]スクリプト エンジンが実行しようとする関数の名前。  
  
 `scriptType`  
 [in]関数の型。 有効な値の説明については、[PROFILER_SCRIPT_TYPE 列挙型](../../winscript/reference/profiler-script-type-enumeration.md)を参照してください。  
  
## <a name="return-value"></a>戻り値  
 このメソッドの戻り値は、スクリプト エンジンによって無視されます。  
  
## <a name="remarks"></a>Remarks  
 DOM の呼び出しは、スクリプト エンジンは呼び出す代わりに、このメソッドを呼び出します。 [IActiveScriptProfilerCallback::OnFunctionEnter](../../winscript/reference/iactivescriptprofilercallback-onfunctionenter.md)します。 これは一意のメソッドと DOM のプロパティの数が多いためです。  
  
## <a name="see-also"></a>関連項目  
 [IActiveScriptProfilerCallback2::OnFunctionExitByName](../../winscript/reference/iactivescriptprofilercallback2-onfunctionexitbyname.md)   
 [IActiveScriptProfilerCallback2 インターフェイス](../../winscript/reference/iactivescriptprofilercallback2-interface.md)