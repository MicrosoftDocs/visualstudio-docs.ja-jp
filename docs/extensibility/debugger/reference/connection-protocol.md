---
description: デバッグ サーバーとデバッグ パッケージ (DE) 間の通信に使用されるプロトコルを示します。
title: CONNECTION_PROTOCOL | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- CONNECTION_PROTOCOL
helpviewer_keywords:
- CONNECTION_PROTOCOL enumeration
ms.assetid: 99df5865-8b36-486d-9f4c-d10ae2bc688a
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: d514b9aa0e37e90e99f21b5b4906cff9d32472db
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105059497"
---
# <a name="connection_protocol"></a>CONNECTION_PROTOCOL
デバッグ サーバーとデバッグ パッケージ (DE) 間の通信に使用されるプロトコルを示します。

## <a name="syntax"></a>構文

```cpp
typedef enum tagCONNECTION_PROTOCOL {
    CONNECTION_NONE    = 0,
    CONNECTION_UNKNOWN = 1,
    CONNECTION_LOCAL   = 2,
    CONNECTION_PIPE    = 3,
    CONNECTION_TCPIP   = 4,
    CONNECTION_HTTP    = 5,
    CONNECTION_OTHER   = 6
} CONNECTION_PROTOCOL;
```

```csharp
public enum CONNECTION_PROTOCOL {
    CONNECTION_NONE    = 0,
    CONNECTION_UNKNOWN = 1,
    CONNECTION_LOCAL   = 2,
    CONNECTION_PIPE    = 3,
    CONNECTION_TCPIP   = 4,
    CONNECTION_HTTP    = 5,
    CONNECTION_OTHER   = 6
};
```

## <a name="fields"></a>フィールド
`CONNECTION_NONE`\
サーバーに接続されていません。

`CONNECTION_UNKNOWN`\
接続されていますが、不明な種類です。

`CONNECTION_LOCAL`\
ローカル サーバーに接続されます。

`CONNECTION_PIPE`\
名前付きパイプを介して接続されます。

`CONNECTION_TCPIP`\
接続では TCP/IP が使用されます。

`CONNECTION_HTTP`\
接続では、HTTP (Web サーバー経由) が使用されます。

`CONNECTION_OTHER`\
その他の種類の何らかの接続が確立されました (この値は現在使用されていません)。

## <a name="remarks"></a>解説
これらの値は、[GetConnectionProtocol](../../../extensibility/debugger/reference/idebugcoreserver3-getconnectionprotocol.md) メソッドから返されます。

## <a name="requirements"></a>必要条件
ヘッダー: msdbg.h

名前空間: Microsoft.VisualStudio.Debugger.Interop

アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [列挙型](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [GetConnectionProtocol](../../../extensibility/debugger/reference/idebugcoreserver3-getconnectionprotocol.md)
