---
description: オプションのフラグの有効な値を列挙します。
title: BP_FLAGS90 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- BP_FLAGS90 enumeration
ms.assetid: 3e5a06c5-fb30-4b8a-b2d5-4a0570fc80bd
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 9267e45c5aa8254323fee461899ad99caf14f868
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105085248"
---
# <a name="bp_flags90"></a>BP_FLAGS90
オプションのフラグの有効な値を列挙します。 ブレークポイントを設定するときに、オプションのフラグを使用して追加情報を指定できます。 この列挙によって [BP_FLAGS](../../../extensibility/debugger/reference/bp-flags.md) 列挙型が拡張されます。

## <a name="syntax"></a>構文

```cpp
enum enum_BP_FLAGS90
{
    // VS 8.0 values
    BP90_FLAG_NONE               = 0x0000,
    BP90_FLAG_MAP_DOCPOSITION    = 0x0001,
    BP90_FLAG_DONT_STOP          = 0x0002,

    // Values added in VS 9.0
    BP90_FLAG_TRACEPOINT_CONTINUE = 0x0004,
};
typedef DWORD BP_FLAGS90;
```

```csharp
public enum enum_BP_FLAGS90
{
    // VS 8.0 values
    BP90_FLAG_NONE                = 0x0000,
    BP90_FLAG_MAP_DOCPOSITION     = 0x0001,
    BP90_FLAG_DONT_STOP           = 0x0002,

    // Values added in VS 9.0
    BP90_FLAG_TRACEPOINT_CONTINUE = 0x0004,
};
```

## <a name="fields"></a>フィールド
`BP90_FLAG_NONE`\
ブレークポイントのフラグを指定しません。

`BP90_FLAG_MAP_DOCPOSITION`\
デバッグ エンジン (DE) でドキュメントの位置を使用してブレークポイントをマップするように指定します。 これは、Active Server Pages (ASP) などのスクリプト指向のソース ファイルに設定されているブレークポイントにのみ適用できます。

`BP90_FLAG_DONT_STOP`\
デバッグ エンジンによってブレークポイントが処理されるように指定するが、デバッグ エンジンが最終的にそこで停止しないようにします。つまり、[IDebugBreakpointEvent2](../../../extensibility/debugger/reference/idebugbreakpointevent2.md) イベント オブジェクトを送信することはできません。 このフラグは、主にトレース ポイントで使用されるように設計されています。

`BP90_FLAG_TRACEPOINT_CONTINUE`\
ステップ実行の状態をクリアする必要があるかどうかを判断するために、ネイティブ デバッグ エンジンによって使用されます。 トレース ポイントでマクロが実行される場合は BP90_FLAG_DONT_STOP が設定されないため、BP90_FLAG_DONT_STOP とは異なります。

## <a name="requirements"></a>必要条件
ヘッダー: Msdbg90.h

名前空間: Microsoft.VisualStudio.Debugger.Interop

アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [列挙型](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
