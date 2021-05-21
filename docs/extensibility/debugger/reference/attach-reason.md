---
description: デバッグ エンジン (DE) をプログラム ノードにアタッチする理由を指定します。
title: ATTACH_REASON | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- ATTACH_REASON
helpviewer_keywords:
- ATTACH_REASON enumeration
ms.assetid: 159fb70b-a344-4ba6-9115-b7eaa16e228f
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 9da162dd2c477d5b901be6c622e2456f44d26a35
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105085430"
---
# <a name="attach_reason"></a>ATTACH_REASON
デバッグ エンジン (DE) をプログラム ノードにアタッチする理由を指定します。

## <a name="syntax"></a>構文

```cpp
enum enum_ATTACH_REASON {
    ATTACH_REASON_LAUNCH = 0x0001,
    ATTACH_REASON_USER   = 0x0002,
    ATTACH_REASON_AUTO   = 0x0003
};
typedef DWORD ATTACH_REASON;
```

```csharp
public enum enum_ATTACH_REASON {
    ATTACH_REASON_LAUNCH = 0x0001,
    ATTACH_REASON_USER   = 0x0002,
    ATTACH_REASON_AUTO   = 0x0003
};
```

## <a name="fields"></a>フィールド
`ATTACH_REASON_AUTO`\
アタッチする理由は、プロセスが現在デバッグ モードであるためです。

`ATTACH_REASON_LAUNCH`\
アタッチする理由は、プロセスが起動されたためです。

`ATTACH_REASON_USER`\
アタッチする理由は、ユーザー要求のためです。

## <a name="remarks"></a>解説
これらの値は、[Attach](../../../extensibility/debugger/reference/idebugengine2-attach.md) メソッドと [Attach](../../../extensibility/debugger/reference/idebugprogramex2-attach.md) メソッドのパラメーターとして使用します。

## <a name="requirements"></a>必要条件
ヘッダー: msdbg.h

名前空間: Microsoft.VisualStudio.Debugger.Interop

アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [列挙型](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [[アタッチ]](../../../extensibility/debugger/reference/idebugengine2-attach.md)
- [[アタッチ]](../../../extensibility/debugger/reference/idebugprogramex2-attach.md)
