---
description: 逆アセンブリ ストリーム内の読み取りポインターを、指定された位置を基準にして指定された命令数だけ移動します。
title: IDebugDisassemblyStream2::Seek | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugDisassemblyStream2::Seek
helpviewer_keywords:
- IDebugDisassemblyStream2::Seek
ms.assetid: afec3008-b1e0-4803-ad24-195dbfb6497e
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 02277bf84bdc12e904b2651ef5ba9fc2356d9090
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105066933"
---
# <a name="idebugdisassemblystream2seek"></a>IDebugDisassemblyStream2::Seek
逆アセンブリ ストリーム内の読み取りポインターを、指定された位置を基準にして指定された命令数だけ移動します。

## <a name="syntax"></a>構文

```cpp
HRESULT Seek( 
   SEEK_START          dwSeekStart,
   IDebugCodeContext2* pCodeContext,
   UINT64              uCodeLocationId,
   INT64               iInstructions
);
```

```csharp
int Seek( 
   enum_SEEK_START    dwSeekStart,
   IDebugCodeContext2 pCodeContext,
   ulong              uCodeLocationId,
   long               iInstructions
);
```

## <a name="parameters"></a>パラメーター
`dwSeekStart`\
[入力] シーク プロセスを開始する相対位置を指定する [SEEK_START](../../../extensibility/debugger/reference/seek-start.md) 列挙型の値。

`pCodeContext`\
[入力] シーク操作の相対基準となるコード コンテキストを表す [IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md) オブジェクト。 このパラメーターは `dwSeekStart` = `SEEK_START_CODECONTEXT` の場合にのみ使用されます。それ以外の場合、このパラメーターは無視され、null 値にすることができます。

`uCodeLocationId`\
[入力] シーク操作の相対基準となるコード位置識別子。 このパラメーターは `dwSeekStart` = `SEEK_START_CODELOCID` の場合に使用されます。それ以外の場合、このパラメーターは無視され、0 に設定することができます。 コード位置識別子の説明については、[GetCodeLocationId](../../../extensibility/debugger/reference/idebugdisassemblystream2-getcodelocationid.md) メソッドの「解説」セクションを参照してください。

`iInstructions`\
[入力] 移動する命令数を、`dwSeekStart` で指定された位置からの相対値で示します。 逆方向に移動するために負の値にすることができます。

## <a name="return-value"></a>戻り値
 正常に終了した場合は、`S_OK` を返します。 シーク位置が、使用可能な命令のリストを超えたポイントであった場合、`S_FALSE` を返します。 それ以外の場合はエラー コードを返します。

## <a name="remarks"></a>解説
 シーク先がリストの先頭より前の位置だった場合、読み取り位置はリストの最初の命令に設定されます。 シーク先がリストの末尾よりも後ろの位置だった場合、読み取り位置はリストの最後の命令に設定されます。

## <a name="see-also"></a>関連項目
- [IDebugDisassemblyStream2](../../../extensibility/debugger/reference/idebugdisassemblystream2.md)
- [SEEK_START](../../../extensibility/debugger/reference/seek-start.md)
- [IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md)
- [GetCodeLocationId](../../../extensibility/debugger/reference/idebugdisassemblystream2-getcodelocationid.md)
