---
title: IDebugContainerField::EnumFields |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugContainerField::EnumFields
helpviewer_keywords:
- IDebugContainerField::EnumFields method
ms.assetid: 9e5e681b-ad49-4c62-bd95-4afa11d61a57
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: a6d3edeb677af728b1a0fd0e9cf8685e7919d79e
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66317928"
---
# <a name="idebugcontainerfieldenumfields"></a>IDebugContainerField::EnumFields
コンテナーのフィールドの列挙子を作成します。

## <a name="syntax"></a>構文

```cpp
HRESULT EnumFields( 
   FIELD_KIND         dwKindFilter,
   FIELD_MODIFIERS    dwModifiersFilter,
   LPCOLESTR          pszNameFilter,
   NAME_MATCH         nameMatch,
   IEnumDebugFields** ppEnum
);
```

```csharp
int EnumFields(
   enum_ FIELD_KIND      dwKindFilter,
   enum_ FIELD_MODIFIERS dwModifiersFilter,
   string                pszNameFilter,
   NAME_MATCH            nameMatch,
   out IEnumDebugFields  ppEnum
);
```

## <a name="parameters"></a>パラメーター
`dwKindFilter`\
[in]組み合わせた[FIELD_KIND](../../../extensibility/debugger/reference/field-kind.md)定数を列挙するフィールドを選択します。 フィールドの種類には、記憶域の種類、クラスまたはプリミティブ型、または特定の情報など、ローカル、パラメーター、または"this"ポインターなどを記述できます。

`dwModifiersFilter`\
[in]組み合わせた[FIELD_MODIFIERS](../../../extensibility/debugger/reference/field-modifiers.md)定数を列挙するフィールドを選択します。 フィールド修飾子は、パブリックまたはプライベート、または記憶域については、仮想、静的、または最終的ななどなどのアクセス許可を指定できます。

`pszNameFilter`\
[in]列挙されるフィールドの名前。 すべてのフィールドが返される場合は、null 値にできます。

`nameMatch`\
[in]値、 [NAME_MATCH](../../../extensibility/debugger/reference/name-match.md)検索かどうかを制御する列挙値が大文字であるか。

`ppEnum`\
[out]返します、 [IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md)フィールドの一覧を表すオブジェクト。 フィールドが存在しない場合は、null 値を返します。

## <a name="return-value"></a>戻り値
 成功した場合は、S_OK または S_FALSE をフィールドが存在しない場合は、返します。 それ以外の場合はエラー コードを返します。

## <a name="remarks"></a>Remarks
 `dwKindFilter`、 `dwModifiersFilter`、および`pszNameFilter`パラメーター組み合わせることができます、たとえば、すべてのパブリック仮想メソッドを"作成した MyMethod"という名前を選択します。

## <a name="see-also"></a>関連項目
- [IDebugContainerField](../../../extensibility/debugger/reference/idebugcontainerfield.md)
- [IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md)
- [FIELD_KIND](../../../extensibility/debugger/reference/field-kind.md)
- [FIELD_MODIFIERS](../../../extensibility/debugger/reference/field-modifiers.md)
- [NAME_MATCH](../../../extensibility/debugger/reference/name-match.md)