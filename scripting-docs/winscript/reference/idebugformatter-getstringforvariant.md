---
title: 'IDebugFormatter:: GetStringForVariant |Microsoft Docs'
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IDebugFormatter.GetStringForVariant
apilocation:
- jscript.dll
helpviewer_keywords:
- IDebugFormatter::GetStringForVariant
ms.assetid: 95189d03-1126-433e-8513-659107b3df16
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 5f703396190f1fb7791306ee9e389b676e749f8f
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/18/2019
ms.locfileid: "72576369"
---
# <a name="idebugformattergetstringforvariant"></a>IDebugFormatter::GetStringForVariant
指定されたバリアント値を表す文字列を返します。  
  
## <a name="syntax"></a>構文  
  
```cpp
HRESULT GetStringForVariant(  
   VARIANT*  pvar,  
   ULONG     nRadix,  
   BSTR*     pbstrValue  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `pvar`  
 から文字列として表すバリアント。  
  
 `nRadix`  
 から数値に使用する基数。  
  
 `pbstrValue`  
 入出力@No__t_0 を表す文字列。  
  
## <a name="return-value"></a>戻り値  
 このメソッドは `HRESULT` を返します。 有効な値を次の表に示しますが、これ以外にもあります。  
  
|[値]|説明|  
|-----------|-----------------|  
|`S_OK`|メソッドが成功しました。|  
  
## <a name="remarks"></a>Remarks  
 このメソッドは、指定されたバリアント値を表す文字列を返します。  
  
## <a name="see-also"></a>関連項目  
 [IDebugFormatter インターフェイス](../../winscript/reference/idebugformatter-interface.md)