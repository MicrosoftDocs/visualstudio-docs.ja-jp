---
title: 'IEnumDebugExtendedPropertyInfo:: GetCount |Microsoft Docs'
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IEnumDebugExtendedPropertyInfo.GetCount
apilocation:
- scrobj.dll
helpviewer_keywords:
- IEnumDebugExtendedPropertyInfo::GetCount
ms.assetid: 2c862f62-b57c-4cd4-ac4e-7d372fbda9a4
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 3b51e4cd765a03226800af95b5de318862d87946
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/18/2019
ms.locfileid: "72576837"
---
# <a name="ienumdebugextendedpropertyinfogetcount"></a>IEnumDebugExtendedPropertyInfo::GetCount
列挙子内の `ExtendedDebugPropertyInfo` 構造体の数を取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp
HRESULT GetCount (  
   ULONG* pcelt  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `pcelt`  
 入出力列挙子内の `ExtendedDebugPropertyInfo` 構造体の数を返します。  
  
## <a name="return-value"></a>戻り値  
 は、有効な `HRESULT`(通常は `S_OK`) を返します。  
  
## <a name="see-also"></a>参照  
 [IEnumDebugExtendedPropertyInfo インターフェイス](../../winscript/reference/ienumdebugextendedpropertyinfo-interface.md)   
 [ExtendedDebugPropertyInfo 構造体](../../winscript/reference/extendeddebugpropertyinfo-structure.md)