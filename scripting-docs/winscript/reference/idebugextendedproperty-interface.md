---
title: IDebugExtendedProperty Interface |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IDebugExtendedProperty interface
ms.assetid: e92ea064-0d92-44cf-bb9f-abda783d84be
caps.latest.revision: 10
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 24a93cb3bd230e2489b58d78f6d414ba1df006ed
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/18/2019
ms.locfileid: "72572495"
---
# <a name="idebugextendedproperty-interface"></a>IDebugExtendedProperty インターフェイス
@No__t_0 インターフェイスを拡張します。  
  
## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド  
 このインターフェイスは、`IDebugProperty` から継承されたメソッドに加えて、次のメソッドを公開します。  
  
|メソッド|説明|  
|------------|-----------------|  
|[IDebugExtendedProperty::GetExtendedPropertyInfo](../../winscript/reference/idebugextendedproperty-getextendedpropertyinfo.md)|このを説明する `ExtendedDebugPropertyInfo` を取得し `IDebugExtendedProperty``.`|  
|[IDebugExtendedProperty::EnumExtendedMembers](../../winscript/reference/idebugextendedproperty-enumextendedmembers.md)|拡張プロパティのメンバーを列挙します。|  
  
## <a name="requirements"></a>［要件］  
 ヘッダー: dbgprop. h  
  
## <a name="see-also"></a>関連項目  
 [IDebugProperty インターフェイス](../../winscript/reference/idebugproperty-interface.md)