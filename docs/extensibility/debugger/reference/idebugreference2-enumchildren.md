---
description: 参照の選択された子の一覧を取得します。
title: IDebugReference2::EnumChildren | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugReference2::EnumChildren
helpviewer_keywords:
- IDebugReference2::EnumChildren
ms.assetid: 35b3c2f3-69f4-4013-b555-f847221f62e8
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 92f55f511a68cca6685579eeb6d686108bf70799
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105071455"
---
# <a name="idebugreference2enumchildren"></a>IDebugReference2::EnumChildren
参照の選択された子の一覧を取得します。 将来使用するために予約されています。

## <a name="syntax"></a>構文

```cpp
HRESULT EnumChildren ( 
   DEBUGREF_INFO_FLAGS        dwFields,
   DWORD                      dwRadix,
   DBG_ATTRIB_FLAGS           dwAttribFilter,
   LPCOLESTR                  pszNameFilter,
   DWORD                      dwTimeout,
   IEnumDebugReferenceInfo2** ppEnum
);
```

```csharp
int EnumChildren ( 
   enum_DEBUGREF_INFO_FLAGS     dwFields,
   uint                         dwRadix,
   enum_DBG_ATTRIB_FLAGS        dwAttribFilter,
   string                       pszNameFilter,
   uint                         dwTimeout,
   out IEnumDebugReferenceInfo2 ppEnum
);
```

## <a name="parameters"></a>パラメーター
`dwFields`\
[入力] [DEBUGREF_INFO_FLAGS](../../../extensibility/debugger/reference/debugref-info-flags.md) 列挙型からのフラグの組み合わせ。列挙された [DEBUG_REFERENCE_INFO](../../../extensibility/debugger/reference/debug-reference-info.md) 構造体のどのフィールドに格納されるかを指定します。

`dwRadix`\
[入力] 数値情報の書式設定に使用される基数。

`dwAttribFilter`\
[入力] 列挙する構造体を選択するために `pszNameFilter` パラメーターと組み合わせてフィルターとして使用される、 [DBG_ATTRIB_FLAGS](../../../extensibility/debugger/reference/dbg-attrib-flags.md) 列挙型のフラグの組み合わせ。

`pszNameFilter`\
[入力] 列挙する構造体を選択するために `dwAttribFilter` パラメーターと組み合わせて使用される、"MyX" などのフィルターを指定する文字列。

`dwTimeout`\
[入力] このメソッドから戻る前に待機する最大時間 (ミリ秒単位)。 待機時間を指定しない場合は `INFINITE` を使用します。

`ppEnum`\
[出力] 要求された子プロパティの一覧を含む [IEnumDebugReferenceInfo2](../../../extensibility/debugger/reference/ienumdebugreferenceinfo2.md) オブジェクトを返します。

## <a name="return-value"></a>戻り値
 常に `E_NOTIMPL` を返します。

## <a name="see-also"></a>関連項目
- [IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md)
- [DEBUGREF_INFO_FLAGS](../../../extensibility/debugger/reference/debugref-info-flags.md)
- [DBG_ATTRIB_FLAGS](../../../extensibility/debugger/reference/dbg-attrib-flags.md)
- [IEnumDebugReferenceInfo2](../../../extensibility/debugger/reference/ienumdebugreferenceinfo2.md)
