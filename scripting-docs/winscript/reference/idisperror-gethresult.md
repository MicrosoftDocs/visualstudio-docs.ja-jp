---
title: IDispError::GetHresult |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IDispError.GetHresult
apilocation:
- scrobj.dll
helpviewer_keywords:
- IDispError::GetHresult
ms.assetid: a14d566e-473f-497b-a2f9-85331433e6c9
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 161c29d4be70c388003ffc80ec5d885b9bcc632b
ms.sourcegitcommit: d3a485d47c6ba01b0fc9878cbbb7fe88755b29af
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/19/2019
ms.locfileid: "58157829"
---
# <a name="idisperrorgethresult"></a>IDispError::GetHresult
エラー コードを取得、`IDispError`オブジェクト。  
  
## <a name="syntax"></a>構文  
  
```cpp
HRESULT GetHresult(  
   HRESULT*  phr  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `phr`  
 [out]エラー コードを指定します。  
  
## <a name="return-value"></a>戻り値  
 このメソッドは `HRESULT` を返します。 有効な値を次の表に示しますが、これ以外にもあります。  
  
|[値]|説明|  
|-----------|-----------------|  
|`S_OK`|メソッドが成功しました。|  
  
## <a name="remarks"></a>Remarks  
 このメソッドからエラー コードを取得、`IDispError`オブジェクト。  
  
> [!NOTE]
>  このメソッドは実装されていません。  
  
## <a name="see-also"></a>関連項目  
 [IDispError インターフェイス](../../winscript/reference/idisperror-interface.md)