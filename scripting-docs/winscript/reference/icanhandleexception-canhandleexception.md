---
title: ICanHandleException::CanHandleException |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- ICanHandleException.CanHandleException
apilocation:
- scrobj.dll
helpviewer_keywords:
- ICanHandleException::CanHandleException
ms.assetid: 0fc703bf-9518-487e-af20-00e073b640f1
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 406787d5ee6811b80f9e6831e5a67cab8367e7d0
ms.sourcegitcommit: d3a485d47c6ba01b0fc9878cbbb7fe88755b29af
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/19/2019
ms.locfileid: "58146488"
---
# <a name="icanhandleexceptioncanhandleexception"></a>ICanHandleException::CanHandleException
スクリプト エンジンの呼び出し元が指定した例外を処理できるかどうかを決定します。  
  
## <a name="syntax"></a>構文  
  
```cpp
HRESULT CanHandleException(  
   EXCEPINFO*  pExcepInfo,  
   VARIANT*    pvar  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `pExcepInfo`  
 [in]ポインター、`EXCEPINFO`例外ハンドラーが見つからない場合に報告される情報を含む構造体。  
  
 `pvar`  
 [in]によってスローされた値など、例外に関連付けられている値を`throw`ステートメント。 このパラメーターは `NULL` の場合もあります。  
  
## <a name="return-value"></a>戻り値  
 このメソッドは `HRESULT` を返します。 有効な値を次の表に示しますが、これ以外にもあります。  
  
|[値]|説明|  
|-----------|-----------------|  
|`S_OK`|呼び出し元が例外を処理できます。|  
|`E_FAIL`|呼び出し元は、例外を処理できません。|  
  
## <a name="remarks"></a>Remarks  
 呼び出し`IDispatchEx::InvokeEx`、または同様のメソッドの結果が例外をサポートするスクリプトの最初の呼び出しチェーン内の呼び出し元のスクリプト エンジンのチェック、`ICanHandleException`インターフェイスし、例外を処理できることを示します。 例外を処理できる呼び出し元にはない、スクリプト エンジンが停止します。  
  
## <a name="see-also"></a>関連項目  
 [ICanHandleException インターフェイス](../../winscript/reference/icanhandleexception-interface.md)   
 [IDispatchEx::InvokeEx](../../winscript/reference/idispatchex-invokeex.md)