---
description: コンテナーのフィールドの列挙子を作成します。
title: IDebugContainerField::EnumFields | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugContainerField::EnumFields
helpviewer_keywords:
- IDebugContainerField::EnumFields method
ms.assetid: 9e5e681b-ad49-4c62-bd95-4afa11d61a57
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 63ce34fc9eddec84326982cf7d30fda919817040
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105077929"
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
[入力] 列挙するフィールドを選択する [FIELD_KIND](../../../extensibility/debugger/reference/field-kind.md) 定数の組み合わせ。 フィールドの種類では、クラスやプリミティブなどのストレージの種類、またはローカル、パラメーター、または "this" ポインターなどの特定の情報を記述できます。

`dwModifiersFilter`\
[入力] 列挙するフィールドを選択する [FIELD_MODIFIERS](../../../extensibility/debugger/reference/field-modifiers.md) 定数の組み合わせ。 フィールド修飾子には、パブリックまたはプライベートなどのアクセス許可や、virtual、static、final などのストレージ情報を指定できます。

`pszNameFilter`\
[入力] 列挙するフィールドの名前。 すべてのフィールドが返される場合は、null 値を指定できます。

`nameMatch`\
[入力] 検索で大文字と小文字を区別するかどうかを制御する [NAME_MATCH](../../../extensibility/debugger/reference/name-match.md) 列挙の値。

`ppEnum`\
[出力] フィールドの一覧を表す [IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md) オブジェクトを返します。 フィールドがない場合は、null 値を返します。

## <a name="return-value"></a>戻り値
 成功した場合は S_OK、フィールドがない場合は S_FALSE を返します。 それ以外の場合はエラー コードを返します。

## <a name="remarks"></a>解説
 `dwKindFilter`、`dwModifiersFilter`、および `pszNameFilter` パラメーターを組み合わせると、たとえば "MyMethod" という名前のパブリック仮想メソッドをすべて選択できます。

## <a name="see-also"></a>関連項目
- [IDebugContainerField](../../../extensibility/debugger/reference/idebugcontainerfield.md)
- [IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md)
- [FIELD_KIND](../../../extensibility/debugger/reference/field-kind.md)
- [FIELD_MODIFIERS](../../../extensibility/debugger/reference/field-modifiers.md)
- [NAME_MATCH](../../../extensibility/debugger/reference/name-match.md)
