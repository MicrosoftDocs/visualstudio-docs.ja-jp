---
description: ダンプするプログラムの状態 (実行中のスレッド、スタック フレーム、現在の命令アドレスなど) の量を指定します。
title: DUMPTYPE | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- DUMPTYPE
helpviewer_keywords:
- DUMPTYPE enumeration
ms.assetid: ea8160db-8732-4056-a1d7-892ef72da71e
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: bc27474b0012e60cccadda44665dc368178a02da
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105095967"
---
# <a name="dumptype"></a>DUMPTYPE
ダンプするプログラムの状態 (実行中のスレッド、スタック フレーム、現在の命令アドレスなど) の量を指定します。

## <a name="syntax"></a>構文

```cpp
enum enum_DUMPTYPE {
    DUMP_MINIDUMP = 0,
    DUMP_FULLDUMP = 1
};
typedef DWORD DUMPTYPE;
```

```csharp
public enum enum_DUMPTYPE {
    DUMP_MINIDUMP = 0,
    DUMP_FULLDUMP = 1
};
```

## <a name="fields"></a>フィールド
`DUMP_MINIDUMP`\
小さいコンパクトなダンプを指定します。

`DUMP_FULLDUMP`\
大きい完全なダンプを指定します。

## <a name="remarks"></a>解説
[WriteDump](../../../extensibility/debugger/reference/idebugprogram2-writedump.md) メソッドに引数として渡されます。

## <a name="requirements"></a>必要条件
ヘッダー: msdbg.h

名前空間: Microsoft.VisualStudio.Debugger.Interop

アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [列挙型](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [WriteDump](../../../extensibility/debugger/reference/idebugprogram2-writedump.md)
