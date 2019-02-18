---
title: CONNECTION_PROTOCOL |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- CONNECTION_PROTOCOL
helpviewer_keywords:
- CONNECTION_PROTOCOL enumeration
ms.assetid: 99df5865-8b36-486d-9f4c-d10ae2bc688a
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 4dcf3d271d331664d6d2ef210868245b50c264d6
ms.sourcegitcommit: 752f03977f45169585e407ef719450dbe219b7fc
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/15/2019
ms.locfileid: "56316485"
---
# <a name="connectionprotocol"></a>CONNECTION_PROTOCOL
デバッグ サーバーとパッケージのデバッグ (DE) 間の通信に使用されるプロトコルを示します。

## <a name="syntax"></a>構文

```cpp
typedef enum tagCONNECTION_PROTOCOL {
    CONNECTION_NONE    = 0,
    CONNECTION_UNKNOWN = 1,
    CONNECTION_LOCAL   = 2,
    CONNECTION_PIPE    = 3,
    CONNECTION_TCPIP   = 4,
    CONNECTION_HTTP    = 5,
    CONNECTION_OTHER   = 6
} CONNECTION_PROTOCOL;
```

```csharp
public enum CONNECTION_PROTOCOL {
    CONNECTION_NONE    = 0,
    CONNECTION_UNKNOWN = 1,
    CONNECTION_LOCAL   = 2,
    CONNECTION_PIPE    = 3,
    CONNECTION_TCPIP   = 4,
    CONNECTION_HTTP    = 5,
    CONNECTION_OTHER   = 6
};
```

#### <a name="parameters"></a>パラメーター
CONNECTION_NONE  
サーバーに接続が確立されていません。

CONNECTION_UNKNOWN  
接続が確立されていますが、不明な型のです。

CONNECTION_LOCAL  
ローカル サーバーへの接続です。

CONNECTION_PIPE  
接続では、名前付きパイプ経由です。

CONNECTION_TCPIP  
接続は、TCP/IP を使用します。

CONNECTION_HTTP  
接続は、(Web サーバー) 経由の HTTP を使用します。

CONNECTION_OTHER  
他の種類の接続が確立されています (この値は現在使用されません)。

## <a name="remarks"></a>Remarks
これらの値から返される、 [GetConnectionProtocol](../../../extensibility/debugger/reference/idebugcoreserver3-getconnectionprotocol.md)メソッド。

## <a name="requirements"></a>必要条件
ヘッダー: msdbg.h

名前空間: Microsoft.VisualStudio.Debugger.Interop

アセンブリ:Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
[列挙型](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)  
[GetConnectionProtocol](../../../extensibility/debugger/reference/idebugcoreserver3-getconnectionprotocol.md)
