---
title: IDebugMethodField::EnumArguments |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugMethodField::EnumArguments
helpviewer_keywords:
- IDebugMethodField::EnumArguments method
ms.assetid: 3ab55488-2437-4ff6-a9ae-78ea6d7b23a8
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: bf62392118ed3ddfb2dfbfca06588f0935f3192d
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "62918727"
---
# <a name="idebugmethodfieldenumarguments"></a>IDebugMethodField::EnumArguments
メソッドの呼び出しに必要な各引数の型の列挙子を作成します。

## <a name="syntax"></a>構文

```cpp
HRESULT EnumArguments( 
   IEnumDebugFields** ppParams
);
```

```csharp
int EnumArguments(
   out IEnumDebugFields ppParams
);
```

#### <a name="parameters"></a>パラメーター
 `ppParams`

 [out]返します、 [IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md)引数の型のリストを表すオブジェクト。 引数がない場合は、null 値を返します。

## <a name="return-value"></a>戻り値
 成功した場合は S_OK を返します。 または引数がない場合は S_FALSE を返します。 それ以外の場合はエラー コードを返します。

## <a name="remarks"></a>Remarks
 各要素は、 [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)各パラメーターの型を表すオブジェクト。 呼び出す、 [GetInfo](../../../extensibility/debugger/reference/idebugfield-getinfo.md)メソッドは各パラメーターの型に関する情報を取得します。

 型とパラメーターの名前が必要な場合を呼び出して、 [EnumParameters](../../../extensibility/debugger/reference/idebugmethodfield-enumparameters.md)メソッド。

## <a name="see-also"></a>関連項目
- [IDebugMethodField](../../../extensibility/debugger/reference/idebugmethodfield.md)
- [IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md)
- [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)
- [EnumParameters](../../../extensibility/debugger/reference/idebugmethodfield-enumparameters.md)