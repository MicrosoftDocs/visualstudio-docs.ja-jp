---
title: BP_FLAGS90 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- BP_FLAGS90 enumeration
ms.assetid: 3e5a06c5-fb30-4b8a-b2d5-4a0570fc80bd
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 5c423b8ecf0e4591913be5ef875057a947f42614
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66319156"
---
# <a name="bpflags90"></a>BP_FLAGS90
オプションのフラグの有効な値を列挙します。 ブレークポイントを設定するときに、追加情報を指定する省略可能なフラグを使用できます。 この列挙体を拡張、 [BP_FLAGS](../../../extensibility/debugger/reference/bp-flags.md)列挙体。

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
デバッグ エンジン (DE) がドキュメントの位置を使用して、ブレークポイントをマップする必要がありますを指定します。 これは、機能は、Active Server Pages (ASP) などのスクリプトを使用したソース ファイルに設定されたブレークポイントにのみ適用されます。

`BP90_FLAG_DONT_STOP`\
ブレークポイントが、デバッグ エンジンによって処理されることことデバッグ エンジン最終的にはとどまりません。 を指定しますつまり、 [IDebugBreakpointEvent2](../../../extensibility/debugger/reference/idebugbreakpointevent2.md)イベント オブジェクトを送信しない必要があります。 このフラグは、トレース ポイントで主に使用する設計されています。

`BP90_FLAG_TRACEPOINT_CONTINUE`\
ネイティブ デバッグ エンジンによってステップ実行の状態をクリアするかどうかを判断するために使用します。 トレース ポイントは、マクロを実行する場合、BP90_FLAG_DONT_STOP が設定されていないため BP90_FLAG_DONT_STOP とは異なります。

## <a name="requirements"></a>必要条件
ヘッダー:Msdbg90.h

名前空間: Microsoft.VisualStudio.Debugger.Interop

アセンブリ:Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [列挙型](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
