---
description: このプログラムをデバッグできるすべてのデバッグ エンジン (DE) の GUID を返します。
title: IDebugProgramEngines2::EnumPossibleEngines | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgramEngines2::EnumPossibleEngines
helpviewer_keywords:
- IDebugProgramEngines2::EnumPossibleEngines
ms.assetid: 993d70a4-f6a5-4e47-a603-0b162b9fde00
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 2a49a0590a1ec2f0b0e7d2be59fe2161b438154a
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105084208"
---
# <a name="idebugprogramengines2enumpossibleengines"></a>IDebugProgramEngines2::EnumPossibleEngines
このプログラムをデバッグできるすべてのデバッグ エンジン (DE) の GUID を返します。

## <a name="syntax"></a>構文

```cpp
HRESULT EnumPossibleEngines( 
   DWORD  celtBuffer,
   GUID*  rgguidEngines,
   DWORD* pceltEngines
);
```

```csharp
int EnumPossibleEngines( 
   uint      celtBuffer,
   GUID[]    rgguidEngines,
   ref DWORD pceltEngines
);
```

## <a name="parameters"></a>パラメーター
`celtBuffer`\
[入力] 返す DE GUID の数。 これで、`rgguidEngines` 配列の最大サイズも指定されます。

`rgguidEngines`\
[入力、出力] 入力される DE GUID の配列。

`pceltEngines`\
[出力] 返される DE GUID の実際の数を返します。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。 バッファーの大きさが十分でない場合は、[C++] `HRESULT_FROM_WIN32(ERROR_INSUFFICIENT_BUFFER)` または [C#] 0x8007007A を返します。

## <a name="remarks"></a>解説
 存在するエンジンの数を確認するには、`celtBuffer` パラメーターを 0 に設定し、`rgguidEngines` パラメーターを null 値に設定して、このメソッドを 1 回呼び出します。 これで `HRESULT_FROM_WIN32(ERROR_INSUFFICIENT_BUFFER)` (C# の場合は 0x8007007A) が返され、`pceltEngines` パラメーターではバッファーに必要なサイズが返されます。

## <a name="see-also"></a>関連項目
- [IDebugProgramEngines2](../../../extensibility/debugger/reference/idebugprogramengines2.md)
