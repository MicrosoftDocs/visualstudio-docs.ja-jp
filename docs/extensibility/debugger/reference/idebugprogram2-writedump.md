---
description: ダンプをファイルに書き込みます。
title: IDebugProgram2::WriteDump | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgram2::WriteDump
helpviewer_keywords:
- IDebugProgram2::WriteDump
ms.assetid: 375afb8c-882d-44db-bfa7-e2c9eb555122
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 8eca50eb6e828841a247ed51d7f73f61cb63e0e9
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105084429"
---
# <a name="idebugprogram2writedump"></a>IDebugProgram2::WriteDump
ダンプをファイルに書き込みます。

## <a name="syntax"></a>構文

```cpp
HRESULT WriteDump( 
   DUMPTYPE  DumpType,
   LPCOLESTR pszDumpUrl
);
```

```csharp
int WriteDump( 
   enum_DUMPTYPE  DumpType,
   string         pszDumpUrl
);
```

## <a name="parameters"></a>パラメーター
`DumpType`\
[入力] ダンプの型 (short、long など) を指定する [DUMPTYPE](../../../extensibility/debugger/reference/dumptype.md) 列挙型の値。

`pszDumpUrl`\
[入力] ダンプの書き込み先の URL。 通常、これは `file://c:\path\filename.ext` の形式ですが、任意の有効な URL を使用できます。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>解説
 通常、プログラム ダンプには、現在のスタック フレーム、スタック自体、プログラムで実行されているスレッドのリスト、および可能な場合はプログラムによって所有されるメモリが含まれます。

## <a name="see-also"></a>関連項目
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
