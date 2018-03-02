---
title: IDebugProgramNode2::DetachDebugger_V7 | Microsoft Docs
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- IDebugProgramNode2::DetachDebugger
helpviewer_keywords:
- IDebugProgramNode2::DetachDebugger
- IDebugProgramNode2::DetachDebugger_V7
author: gregvanl
ms.author: gregvanl
manager: ghogen
ms.workload:
- vssdk
ms.openlocfilehash: fdf4875c30bebaeed925af57c0d80910f8fcbf21
ms.sourcegitcommit: 8cbe6b38b810529a6c364d0f1918e5c71dee2c68
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/28/2018
---
# <a name="idebugprogramnode2detachdebuggerv7"></a>IDebugProgramNode2::DetachDebugger_V7

> [!Note]
> 推奨されなくなりました。 使用しないでください。

## <a name="syntax"></a>構文

```cpp
HRESULT DetachDebugger_V7 (
   void 
);
```

```csharp
int DetachDebugger_V7 ();
```

## <a name="return-value"></a>戻り値

実装を常に返します`E_NOTIMPL`です。

## <a name="remarks"></a>コメント

> [!WARNING]
> Visual Studio 2005 の時点でこのメソッドは使用されなくを常に返す必要があります`E_NOTIMPL`です。

このメソッドは、デバッガーが突然終了するときに呼び出されます。 このメソッドが呼び出されたときに、DE は必要があります、ユーザーがそこからデタッチされたものとしてプログラムを再開します。 これ以上のデバッグ イベントを送信する必要があります。 プログラムは、デバッガーの別のインスタンスからアタッチ可能な状態である必要があります。

## <a name="see-also"></a>参照

[IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md)