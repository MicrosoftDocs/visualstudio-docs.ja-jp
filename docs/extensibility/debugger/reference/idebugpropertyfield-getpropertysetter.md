---
title: IDebugPropertyField::GetPropertySetter |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPropertyField::GetPropertySetter
helpviewer_keywords:
- IDebugPropertyField::GetPropertySetter method
ms.assetid: 744d76fd-2bcc-4917-a040-ce4cc714ef61
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 390d3b2c5d468552c3def5c7e2b1cd73ece5e0ab
ms.sourcegitcommit: 19ec963ed6d585719cb83ba677434ea6580e0d1f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2019
ms.locfileid: "66211406"
---
# <a name="idebugpropertyfieldgetpropertysetter"></a>IDebugPropertyField::GetPropertySetter
プロパティを設定するメソッドを取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetPropertySetter( 
   IDebugMethodField** ppField
);
```

```csharp
int GetPropertySetter(
   out IDebugMethodField ppField
);
```

## <a name="parameters"></a>パラメーター
`ppField`\
[out]返します、 [IDebugMethodField](../../../extensibility/debugger/reference/idebugmethodfield.md)プロパティを設定するメソッドを表すオブジェクト。

## <a name="return-value"></a>戻り値
 成功した場合、S_OK を返します。それ以外の場合はエラー コードを返します。

## <a name="remarks"></a>Remarks
 プロパティを取得するメソッドを取得する、 [GetPropertyGetter](../../../extensibility/debugger/reference/idebugpropertyfield-getpropertygetter.md)メソッド。

## <a name="see-also"></a>関連項目
- [IDebugPropertyField](../../../extensibility/debugger/reference/idebugpropertyfield.md)
- [IDebugMethodField](../../../extensibility/debugger/reference/idebugmethodfield.md)
- [GetPropertyGetter](../../../extensibility/debugger/reference/idebugpropertyfield-getpropertygetter.md)