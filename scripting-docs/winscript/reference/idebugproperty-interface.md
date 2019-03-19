---
title: IDebugProperty インターフェイス |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IDebugProperty interface
ms.assetid: 7e8f5341-23ef-4029-814d-f5c2307b9203
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 963b11a4760fad8086822f13db129fae76467802
ms.sourcegitcommit: d3a485d47c6ba01b0fc9878cbbb7fe88755b29af
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/19/2019
ms.locfileid: "58145760"
---
# <a name="idebugproperty-interface"></a>IDebugProperty インターフェイス
デバッグ中のエンティティの階層のプロパティを名前、種類、および値の記述に使用します。 ほとんどの場合、`IDebugProperty`式の評価、ステートメントの評価、またはレジスタ評価の結果を記述するために使用します。  
  
## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド  
 次の表は、メソッドの`IDebugProperty`インターフェイス。  
  
|メソッド|説明|  
|------------|-----------------|  
|[IDebugProperty::GetPropertyInfo](../../winscript/reference/idebugproperty-getpropertyinfo.md)|取得、`DebugPropertyInfo`説明します。 `IDebugProperty``.`|  
|[IDebugProperty::GetExtendedInfo](../../winscript/reference/idebugproperty-getextendedinfo.md)|プロパティに拡張された情報を取得します。|  
|[IDebugProperty::SetValueAsString](../../winscript/reference/idebugproperty-setvalueasstring.md)|文字列からプロパティの値を設定します。|  
|[IDebugProperty::EnumMembers](../../winscript/reference/idebugproperty-enummembers.md)|プロパティのメンバーを列挙します。|  
|[IDebugProperty::GetParent](../../winscript/reference/idebugproperty-getparent.md)|プロパティの親を取得します。|  
  
## <a name="requirements"></a>必要条件  
 ヘッダー: dbgprop.h