---
title: IDebugExtendedProperty::GetExtendedPropertyInfo |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IDebugExtendedProperty.GetExtendedPropertyInfo
apilocation:
- scrobj.dll
helpviewer_keywords:
- IDebugExtendedProperty::GetExtendedPropertyInfo
ms.assetid: 56edf538-5082-4653-82b6-e6640d6f61ba
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 89067720b6643c8c187e6340fb529989f2439933
ms.sourcegitcommit: d3a485d47c6ba01b0fc9878cbbb7fe88755b29af
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/19/2019
ms.locfileid: "58159167"
---
# <a name="idebugextendedpropertygetextendedpropertyinfo"></a>IDebugExtendedProperty::GetExtendedPropertyInfo
詳細については、単純なよりである、拡張プロパティの拡張情報をフェッチ`IDebugProperty`します。  
  
## <a name="syntax"></a>構文  
  
```cpp
HRESULT GetExtendedPropertyInfo(  
   EX_DBGPROP_INFO_FLAGS  dwFieldSpec,  
   UINT  nRadix,  
   ExtendedDebugPropertyInfo*  pExtendedPropertyInfo  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `dwFieldSpec`  
 [in]入力するフィールドを決定する EX_DBGPROP_INFO_FLAGS 定数を指定します、`ExtendedDebugPropertyInfo`構造体。  
  
 `nRadix`  
 [in]任意の数値情報を解釈するときに使用する基数。  
  
 `pExtendedPropertyInfo`  
 [out]返します、`ExtendedDebugPropertyInfo`プロパティを記述する構造体。  
  
## <a name="return-value"></a>戻り値  
 有効な返します`HRESULT`、通常`S_OK`します。  
  
## <a name="see-also"></a>関連項目  
 [IDebugExtendedProperty インターフェイス](../../winscript/reference/idebugextendedproperty-interface.md)   
 [EX_DBGPROP_INFO_FLAGS](../../winscript/reference/ex-dbgprop-info-flags.md)   
 [ExtendedDebugPropertyInfo 構造体](../../winscript/reference/extendeddebugpropertyinfo-structure.md)