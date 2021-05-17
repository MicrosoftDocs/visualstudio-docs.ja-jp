---
description: 逆アセンブリ ストリーム内の現在位置から始まる命令を読み取ります。
title: IDebugDisassemblyStream2::Read | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugDisassemblyStream2::Read
helpviewer_keywords:
- IDebugDisassemblyStream2::Read
ms.assetid: 7db5f6bb-73ee-45bc-b187-c1b6aa2dfdd5
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: bcabd0cc42f013b579ee32deeb33d68cd9d45f5d
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105066920"
---
# <a name="idebugdisassemblystream2read"></a>IDebugDisassemblyStream2::Read
逆アセンブリ ストリーム内の現在位置から始まる命令を読み取ります。

## <a name="syntax"></a>構文

```cpp
HRESULT Read( 
   DWORD                     dwInstructions,
   DISASSEMBLY_STREAM_FIELDS dwFields,
   DWORD*                    pdwInstructionsRead,
   DisassemblyData*          prgDisassembly
);
```

```csharp
int Read( 
   uint                           dwInstructions,
   enum_DISASSEMBLY_STREAM_FIELDS dwFields,
   out uint                       pdwInstructionsRead,
   DisassemblyData[]              prgDisassembly
);
```

## <a name="parameters"></a>パラメーター
`dwInstructions`\
[入力] 逆アセンブルする命令の数。 この値は、`prgDisassembly` 配列の最大長でもあります。

`dwFields`\
[入力] `prgDisassembly` のどのフィールドが入力されるかを示す [DISASSEMBLY_STREAM_FIELDS](../../../extensibility/debugger/reference/disassembly-stream-fields.md) 列挙型のフラグの組み合わせ。

`pdwInstructionsRead`\
[出力] 実際に逆アセンブルされた命令の数を返します。

`prgDisassembly`\
[出力] 逆アセンブルされたコードが入力される [DisassemblyData](../../../extensibility/debugger/reference/disassemblydata.md) 構造体の配列。逆アセンブルされた命令ごとに 1 つの構造体になります。 この配列の長さは、`dwInstructions` パラメーターによって決定されます。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>解説
 現在のスコープで使用可能な命令の最大数は、[GetSize](../../../extensibility/debugger/reference/idebugdisassemblystream2-getsize.md) メソッドを呼び出して取得できます。

 次の命令が読み取られる現在位置は、[Seek](../../../extensibility/debugger/reference/idebugdisassemblystream2-seek.md) メソッドを呼び出して変更できます。

 `dwFields` パラメーターで `DSF_OPERANDS_SYMBOLS` フラグを `DSF_OPERANDS` フラグに追加して、命令を逆アセンブルするときはシンボル名を使用する必要があることを示すことができます。

## <a name="see-also"></a>関連項目
- [IDebugDisassemblyStream2](../../../extensibility/debugger/reference/idebugdisassemblystream2.md)
- [DISASSEMBLY_STREAM_FIELDS](../../../extensibility/debugger/reference/disassembly-stream-fields.md)
- [DisassemblyData](../../../extensibility/debugger/reference/disassemblydata.md)
- [GetSize](../../../extensibility/debugger/reference/idebugdisassemblystream2-getsize.md)
- [Seek](../../../extensibility/debugger/reference/idebugdisassemblystream2-seek.md)
