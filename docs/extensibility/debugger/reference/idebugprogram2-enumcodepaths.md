---
description: ソース ファイル内の指定された位置のコード パスの一覧を取得します。
title: IDebugProgram2::EnumCodePaths | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgram2::EnumCodePaths
helpviewer_keywords:
- IDebugProgram2::EnumCodePaths
ms.assetid: fb100c3c-9c29-4d63-bd1f-a3e531cb395f
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 057089c8c7b68fd1109c31bbfc0014f49a71368c
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105076044"
---
# <a name="idebugprogram2enumcodepaths"></a>IDebugProgram2::EnumCodePaths
ソース ファイル内の指定された位置のコード パスの一覧を取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT EnumCodePaths( 
   LPCOLESTR            pszHint,
   IDebugCodeContext2*  pStart,
   IDebugStackFrame2*   pFrame,
   BOOL                 fSource,
   IEnumCodePaths2**    ppEnum,
   IDebugCodeContext2** ppSafety
);
```

```csharp
int EnumCodePaths( 
   string                 pszHint,
   IDebugCodeContext2     pStart,
   IDebugStackFrame2      pFrame,
   Int                    fSource,
   out IEnumCodePaths2    ppEnum,
   out IDebugCodeContext2 ppSafety
);
```

## <a name="parameters"></a>パラメーター
`pszHint`\
[入力] IDE の **[ソース]** または **[逆アセンブリ]** ビューで、カーソルの下にある単語。

`pStart`\
[入力] 現在のコード コンテキストを表す [IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md) オブジェクト。

`pFrame`\
[入力] 現在のブレークポイントに関連付けられているスタック フレームを表す [IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md) オブジェクト。

`fSource`\
[入力] **[ソース]** ビューの場合は 0 以外 (`TRUE`)、 **[逆アセンブリ]** ビューの場合は 0 (`FALSE`)。

`ppEnum`\
[出力] コード パスの一覧を格納している [IEnumCodePaths2](../../../extensibility/debugger/reference/ienumcodepaths2.md) オブジェクトを返します。

`ppSafety`\
[出力] 選択したコード パスがスキップされた場合のブレークポイントとして設定される追加のコード コンテキストを表す [IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md) オブジェクトを返します。 これは、たとえば短絡ブール式の場合に発生する可能性があります。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>解説
 コード パスは、プログラムの実行中に現在のポイントにアクセスするために呼び出されたメソッドまたは関数の名前を記述します。 コード パスの一覧は、呼び出し履歴を表します。

## <a name="see-also"></a>関連項目
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
- [IEnumCodePaths2](../../../extensibility/debugger/reference/ienumcodepaths2.md)
- [IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md)
- [IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md)
