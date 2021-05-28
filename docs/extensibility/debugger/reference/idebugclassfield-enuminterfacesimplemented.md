---
description: このクラスによって実装されたインターフェイスの列挙子を作成します。
title: IDebugClassField::EnumInterfacesImplemented | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugClassField::EnumInterfacesImplemented
helpviewer_keywords:
- IDebugClassField::EnumInterfacesImplemented method
ms.assetid: e5523e45-d350-491e-a92c-fe0ca97d2052
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 1763cbcd0a1c61150a054752c94a42f10127251a
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105088615"
---
# <a name="idebugclassfieldenuminterfacesimplemented"></a>IDebugClassField::EnumInterfacesImplemented
このクラスによって実装されたインターフェイスの列挙子を作成します。

## <a name="syntax"></a>構文

```cpp
HRESULT EnumInterfacesImplemented( 
   IEnumDebugFields** ppEnum
);
```

```csharp
int EnumInterfacesImplemented(
   out IEnumDebugFields ppEnum
);
```

## <a name="parameters"></a>パラメーター
`ppEnum`\
[出力] 実装されたインターフェイスの一覧を表す [IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md) オブジェクトを返します。 インターフェイスがない場合は、null 値を返します。

## <a name="return-value"></a>戻り値
 成功した場合は、S_OK を返します。このクラスに実装されたインターフェイスがない場合は、S_FALSE を返します。 それ以外の場合はエラー コードを返します。

## <a name="remarks"></a>解説
 列挙の各要素は、インターフェイスを記述する [IDebugClassField](../../../extensibility/debugger/reference/idebugclassfield.md) オブジェクトです。 アンマネージド [!INCLUDE[vcprvc](../../../code-quality/includes/vcprvc_md.md)] コードではインターフェイスを離散エンティティとして使用しないので、このメソッドからは常にアンマネージド [!INCLUDE[vcprvc](../../../code-quality/includes/vcprvc_md.md)] コードに対して null 値が返されます。

## <a name="see-also"></a>関連項目
- [IDebugClassField](../../../extensibility/debugger/reference/idebugclassfield.md)
- [IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md)
