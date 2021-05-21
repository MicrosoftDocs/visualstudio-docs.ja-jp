---
description: このメソッドは、このプロセス (および含まれているすべてのプログラム) のエディット コンティニュを明示的に無効にします。
title: IDebugProcess3::DisableENC | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProcess3::DisableENC
helpviewer_keywords:
- IDebugProcess3::DisableENC
ms.assetid: cffdbdac-4d76-4aeb-aa55-5d0410db99f1
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 7f9c4a1e05cf7d4a98489daf0c2ee3377d54f417
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105081621"
---
# <a name="idebugprocess3disableenc"></a>IDebugProcess3::DisableENC
このメソッドは、このプロセス (および含まれているすべてのプログラム) のエディット コンティニュを明示的に無効にします。 カスタム ポート サプライヤーは、常に `E_NOTIMPL` を返す必要があります。

## <a name="syntax"></a>構文

```cpp
HRESULT DisableENC(
   EncUnavailableReason reason
);
```

```csharp
   EncUnavailableReason reason
);
```

## <a name="parameters"></a>パラメーター
`reason`\
[in] [EncUnavailableReason](../../../extensibility/debugger/reference/encunavailablereason.md) 列挙体の値。

## <a name="return-value"></a>戻り値
 正常に終了した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。

> [!NOTE]
> カスタム ポート サプライヤーは、常に `E_NOTIMPL` を返す必要があります。

## <a name="remarks"></a>解説
 プロセスのエディット コンティニュを無効にすると、プロセスの再起動によってのみ再度有効にすることができます。

## <a name="see-also"></a>関連項目
- [IDebugProcess3](../../../extensibility/debugger/reference/idebugprocess3.md)
- [EncUnavailableReason](../../../extensibility/debugger/reference/encunavailablereason.md)
