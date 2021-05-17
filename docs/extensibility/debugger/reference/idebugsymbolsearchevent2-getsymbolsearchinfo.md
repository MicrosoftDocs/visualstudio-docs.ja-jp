---
description: シンボルの読み込みプロセスに関する結果を取得するために、イベント ハンドラーによって呼び出されます。
title: IDebugSymbolSearchEvent2::GetSymbolSearchInfo | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugSymbolSearchEvent2::GetSymbolSearchInfo
helpviewer_keywords:
- IDebugSymbolSearchEvent2::GetSymbolSearchInfo
ms.assetid: ae9eb72b-f2aa-43b8-87ca-da19d2e78d17
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 18ca042250d532fe886ac969df5a09bd5d1a49f1
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105081244"
---
# <a name="idebugsymbolsearchevent2getsymbolsearchinfo"></a>IDebugSymbolSearchEvent2::GetSymbolSearchInfo
シンボルの読み込みプロセスに関する結果を取得するために、イベント ハンドラーによって呼び出されます。

## <a name="syntax"></a>構文

```cpp
HRESULT GetSymbolSearchInfo(
   IDebugModule3**    pModule,
   BSTR*              pbstrDebugMessage,
   MODULE_INFO_FLAGS* pdwModuleInfoFlags
);
```

```csharp
int GetSymbolSearchInfo(
   IDebugModule3              pModule,
   ref string                 pbstrDebugMessage,
   out enum_MODULE_INFO_FLAGS pdwModuleInfoFlags
);
```

## <a name="parameters"></a>パラメーター
`pModule`\
[出力] シンボルが読み込まれたモジュールを表す IDebugModule3 オブジェクト。

`pbstrDebugMessage`\
[入力、出力] モジュールからのエラー メッセージを含む文字列を返します。 エラーがない場合、この文字列にはモジュールの名前だけが含まれますが、空になることはありません。

> [!NOTE]
> [C++] `pbstrDebugMessage` を `NULL` にすることはできません。また、`SysFreeString` で解放する必要があります。

`pdwModuleInfoFlags`\
[出力] シンボルが読み込まれたかどうかを示す、[MODULE_INFO_FLAGS](../../../extensibility/debugger/reference/module-info-flags.md) 列挙型のフラグの組み合わせ。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>解説
 モジュールのデバッグ シンボルの読み込みが試行された後にハンドラーで [IDebugSymbolSearchEvent2](../../../extensibility/debugger/reference/idebugsymbolsearchevent2.md) イベントを受け取ると、ハンドラーでは thismethod を呼び出して、その読み込みの結果を判別できます。

## <a name="see-also"></a>関連項目
- [IDebugModule3](../../../extensibility/debugger/reference/idebugmodule3.md)
- [MODULE_INFO_FLAGS](../../../extensibility/debugger/reference/module-info-flags.md)
- [IDebugSymbolSearchEvent2](../../../extensibility/debugger/reference/idebugsymbolsearchevent2.md)
