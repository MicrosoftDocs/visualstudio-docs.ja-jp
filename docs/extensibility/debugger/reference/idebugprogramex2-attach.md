---
description: プログラムにセッションをアタッチします。
title: IDebugProgramEx2::Attach | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgramEx2::Attach
helpviewer_keywords:
- IDebugProgramEx2::Attach
ms.assetid: 33b22b2f-431e-4205-9441-d28a9c928c97
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: f4f7f6a083c37ece73be488ab0c4f6d4c25ce24c
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105084156"
---
# <a name="idebugprogramex2attach"></a>IDebugProgramEx2::Attach
プログラムにセッションをアタッチします。

## <a name="syntax"></a>構文

```cpp
HRESULT Attach( 
   IDebugEventCallback2* pCallback,
   DWORD                 dwReason,
   IDebugSession2*       pSession
);
```

```csharp
int Attach( 
   IDebugEventCallback2 pCallback,
   uint                 dwReason,
   IDebugSession2       pSession
);
```

## <a name="parameters"></a>パラメーター
`pCallback`\
[入力] アタッチされたデバッグ エンジンでイベントを送信する先のコールバック関数を表す [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md) オブジェクト。

`dwReason`\
[入力] アタッチ操作の理由を説明する [ATTACH_REASON](../../../extensibility/debugger/reference/attach-reason.md) 列挙型の値。

`pSession`\
[入力] プログラムにアタッチしているセッションを一意に識別する値。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。 プログラムが既にアタッチされている場合、このメソッドでは `E_ATTACH_DEBUGGER_ALREADY_ATTACHED` を返す必要があります。

## <a name="remarks"></a>解説
 プログラムを含むポートでは、`pSession` の値を使用して、どのセッションがプログラムにアタッチしようとしているかを判断できます。 たとえば、ポートで一度に 1 つのデバッグ セッションだけをプロセスにアタッチできる場合、ポートでは、同じセッションがプロセス内の他のプログラムに既にアタッチされているかどうかを判断できます。

> [!NOTE]
> 渡されるインターフェイス `pSession` は、Cookie としてのみ扱われます。これは、このプログラムにアタッチするセッション デバッグ マネージャーを一意に識別する値です。指定されたインターフェイスのメソッドは機能しません。

## <a name="see-also"></a>関連項目
- [IDebugProgramEx2](../../../extensibility/debugger/reference/idebugprogramex2.md)
