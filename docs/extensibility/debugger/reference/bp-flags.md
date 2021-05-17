---
description: ブレークポイントを設定するときに追加情報を指定するために使用できるオプションのフラグを指定します。
title: BP_FLAGS | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- BP_FLAGS
helpviewer_keywords:
- BP_FLAGS enumeration
ms.assetid: c45dfc74-5e7f-4f1e-a147-ab2a55dccbd0
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 8e35e0b219bb77ce722f2e06a260de7ecc837dfb
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105085326"
---
# <a name="bp_flags"></a>BP_FLAGS
ブレークポイントを設定するときに追加情報を指定するために使用できるオプションのフラグを指定します。

## <a name="syntax"></a>構文

```cpp
enum enum_BP_FLAGS {
    BP_FLAG_NONE            = 0x0000,
    BP_FLAG_MAP_DOCPOSITION = 0x0001,
    BP_FLAG_DONT_STOP       = 0x0002
};
typedef DWORD BP_FLAGS;
```

```csharp
public enum enum_BP_FLAGS {
    BP_FLAG_NONE            = 0x0000,
    BP_FLAG_MAP_DOCPOSITION = 0x0001,
    BP_FLAG_DONT_STOP       = 0x0002
};
```

## <a name="fields"></a>フィールド
`BP_FLAG_NONE`\
ブレークポイントのフラグを指定しません。

`BP_FLAG_MAP_DOCPOSITION`\
デバッグ エンジン (DE) でドキュメントの位置を使用してブレークポイントをマップするように指定します。 これは、Active Server Pages (ASP) などのスクリプト指向のソース ファイルに設定されているブレークポイントにのみ適用できます。

`BP_FLAG_DONT_STOP`\
デバッグ エンジンによってブレークポイントが処理されるように指定するが、デバッグ エンジンが最終的にそこで停止しないようにします (つまり、[IDebugBreakpointEvent2](../../../extensibility/debugger/reference/idebugbreakpointevent2.md) イベント オブジェクトを送信することはできません)。 このフラグは、主にトレースポイントで使用されるように設計されています。

## <a name="remarks"></a>解説
[BP_REQUEST_INFO](../../../extensibility/debugger/reference/bp-request-info.md) および [BP_REQUEST_INFO2](../../../extensibility/debugger/reference/bp-request-info2.md) 構造体の `dwFlags` メンバーに使用されます。

これらの値は、ビットごとの `OR` で組み合わせることができます。

## <a name="requirements"></a>必要条件
ヘッダー: msdbg.h

名前空間: Microsoft.VisualStudio.Debugger.Interop

アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [列挙型](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [BP_REQUEST_INFO](../../../extensibility/debugger/reference/bp-request-info.md)
- [BP_REQUEST_INFO2](../../../extensibility/debugger/reference/bp-request-info2.md)
- [IDebugBreakpointEvent2](../../../extensibility/debugger/reference/idebugbreakpointevent2.md)
