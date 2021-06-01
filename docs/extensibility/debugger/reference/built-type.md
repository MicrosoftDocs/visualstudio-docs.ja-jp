---
description: BUILT_TYPE 構造体は、メタデータから取得したフィールドの型に関する情報を指定します。
title: BUILT_TYPE | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- BUILT_TYPE
helpviewer_keywords:
- BUILT_TYPE structure
ms.assetid: cc02c32c-0f65-4210-ad25-a9b1899066e8
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 00a031d02bba7ffcc1dca6f2cf73cfceeed04838
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105096578"
---
# <a name="built_type"></a>BUILT_TYPE
この構造体は、メタデータから取得したフィールドの型に関する情報を指定します。

## <a name="syntax"></a>構文

```cpp
typedef struct _tagTYPE_BUILT {
    ULONG32      ulAppDomainID;
    GUID         guidModule;
    IDebugField* pUnderlyingField;
} BUILT_TYPE;
```

```csharp
public struct BUILT_TYPE {
    public uint        ulAppDomainID;
    public Guid        guidModule;
    public IDebugField pUnderlyingField;
};
```

## <a name="members"></a>メンバー
`ulAppDomainID`\
シンボルの取得元のアプリケーションの ID。 これは、アプリケーションのインスタンスを一意に識別するために使用されます。

`guidModule`\
このフィールドが含まれるモジュールの GUID。

`pUnderlyingField`\
このビルト フィールドに関連付けられた基になるフィールドを識別する [IDebugField](../../../extensibility/debugger/reference/idebugfield.md) オブジェクト。

## <a name="remarks"></a>解説
この構造体は、`TYPE_INFO` 構造体の `dwKind` フィールドを `TYPE_KIND_BUILT` ([dwTYPE_KIND](../../../extensibility/debugger/reference/dwtype-kind.md) 列挙型の値) に設定した場合、[TYPE_INFO](../../../extensibility/debugger/reference/type-info.md) 構造体に含まれる共用体の一部になります。

## <a name="requirements"></a>必要条件
ヘッダー: sh.h

名前空間: Microsoft.VisualStudio.Debugger.Interop

アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [構造体と共用体](../../../extensibility/debugger/reference/structures-and-unions.md)
- [TYPE_INFO](../../../extensibility/debugger/reference/type-info.md)
- [dwTYPE_KIND](../../../extensibility/debugger/reference/dwtype-kind.md)
- [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)
