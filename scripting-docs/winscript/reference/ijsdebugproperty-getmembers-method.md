---
title: 'IJsDebugProperty:: GetMembers メソッド |Microsoft Docs'
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IJsDebugProperty.GetMembers
apilocation:
- jscript9diag.dll
ms.assetid: a32b5372-d9cb-4b9a-9bc2-81b5e1df365c
caps.latest.revision: 4
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: a3e700e51dea6723238437bf1fed741698097ae2
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/18/2019
ms.locfileid: "72574059"
---
# <a name="ijsdebugpropertygetmembers-method"></a>IJsDebugProperty::GetMembers メソッド
このオブジェクトのメンバーを取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp
HRESULT GetMembers(  
   JS_PROPERTY_MEMBERS members,  
   IJsEnumDebugProperty **ppEnum  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `members`  
 [入力] メンバー情報の内容を指定するフラグ。  
  
 `ppEnum`  
 [出力] オブジェクトのメンバー。  
  
## <a name="return-value"></a>戻り値  
  
## <a name="requirements"></a>［要件］  
 **ヘッダー:** jscript9diag.h  
  
## <a name="see-also"></a>関連項目  
 [IJsDebugProperty インターフェイス](../../winscript/reference/ijsdebugproperty-interface.md)