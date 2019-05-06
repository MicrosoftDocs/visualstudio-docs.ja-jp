---
title: IEnumDebugExtendedPropertyInfo インターフェイス |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IEnumDebugExtendedPropertyInfo
apilocation:
- scrobj.dll
helpviewer_keywords:
- IEnumDebugExtendedPropertyInfo interface
ms.assetid: 316d5aa7-c949-48fc-89c1-239f00566cae
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 2440daf99d9dbb69713d1895ffbfaa18965480a4
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "62963479"
---
# <a name="ienumdebugextendedpropertyinfo-interface"></a>IEnumDebugExtendedPropertyInfo インターフェイス
列挙`ExtendedDebugPropertyInfo`構造体。  
  
## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド  
 次の表は、メソッドの`IEnumDebugExtendedPropertyInfo`します。  
  
|メソッド|説明|  
|------------|-----------------|  
|[IEnumDebugExtendedPropertyInfo::Clone](../../winscript/reference/ienumdebugextendedpropertyinfo-clone.md)|現在の列挙子と同じ列挙状態を格納する列挙子を作成します。|  
|[IEnumDebugExtendedPropertyInfo::GetCount](../../winscript/reference/ienumdebugextendedpropertyinfo-getcount.md)|数を取得`ExtendedDebugPropertyInfo`列挙子内の構造体。|  
|[IEnumDebugExtendedPropertyInfo::Next](../../winscript/reference/ienumdebugextendedpropertyinfo-next.md)|指定した数を取得`ExtendedDebugPropertyInfo`列挙体シーケンス内の構造体。|  
|[IEnumDebugExtendedPropertyInfo::Skip](../../winscript/reference/ienumdebugextendedpropertyinfo-skip.md)|指定した数のスキップ`ExtendedDebugPropertyInfo`列挙体シーケンス内の構造体。|  
|[IEnumDebugExtendedPropertyInfo::Reset](../../winscript/reference/ienumdebugextendedpropertyinfo-reset.md)|列挙のシーケンスを最初にリセットします。|  
  
## <a name="requirements"></a>必要条件  
 ヘッダー: dbgprop.h  
  
## <a name="see-also"></a>関連項目  
 [ExtendedDebugPropertyInfo 構造体](../../winscript/reference/extendeddebugpropertyinfo-structure.md)