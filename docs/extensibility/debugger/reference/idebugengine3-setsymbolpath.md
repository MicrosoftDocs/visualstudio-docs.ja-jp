---
description: デバッグ シンボルを検索する 1 つ以上のパスを設定します。
title: IDebugEngine3::SetSymbolPath | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEngine3::SetSymbolPath
helpviewer_keywords:
- IDebugEngine3::SetSymbolPath
ms.assetid: 47b48f84-8a96-401f-84df-0baa8a96d26e
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: f3bc24aa6ae07505f4f1fce16593f11e44e752a9
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105066118"
---
# <a name="idebugengine3setsymbolpath"></a>IDebugEngine3::SetSymbolPath
デバッグ シンボルを検索する 1 つ以上のパスを設定します。

## <a name="syntax"></a>構文

```cpp
HRESULT SetSymbolPath (
   LPOLESTR            szSymbolSearchPath,
   LPOLESTR            szSymbolCachePath,
   LOAD_SYMBOLS_FLAGS  Flags
);
```

```csharp
int SetSymbolPath(
   string                    szSymbolSearchPath,
   string                    szSymbolCachePath,
   enum_LOAD_SYMBOLS_FLAGS   Flags
);
```

## <a name="parameters"></a>パラメーター

`szSymbolSearchPath`\
[入力] 1 つ以上のシンボル検索パスを含む文字列。 詳細については、「解説」を参照してください。 null にすることはできません。

`szSymbolCachePath`\
[入力] シンボルをキャッシュできるローカル パスを含む文字列。 null にすることはできません。

`Flags`\
[入力] 使用されません。常に 0 に設定します。

## <a name="return-value"></a>戻り値
 正常に終了した場合は、S_OK が返されます。それ以外の場合は、エラー コードが返されます。

## <a name="remarks"></a>解説
 文字列 `szSymbolSearchPath` は、シンボルを検索する 1 つ以上のパスをセミコロンで区切ったリストです。 これらのパスには、ローカル パス、UNC 形式のパス、または URL を指定できます。 これらのパスは、異なる種類を混在させることもできます。 パスが UNC (例: \\\Symserver\Symbols) の場合、デバッグ エンジンでは、パスがシンボル サーバーのパスであるかどうかを判断する必要があります。また、そのサーバーからシンボルを読み込み、`szSymbolCachePath` で指定されたパスにキャッシュできることが必要です。

 シンボル パスには 1 つ以上のキャッシュ位置を含めることもできます。 キャッシュは優先度順にリストされ、最も優先度が高いキャッシュが先頭になり、* 記号で区切られます。 次に例を示します。

```
\\symbols\symbols;\\someotherserver\symbols;c:\symbols\httpsymbols*https://msdl.microsoft.com
```

 [LoadSymbols](../../../extensibility/debugger/reference/idebugengine3-loadsymbols.md) メソッドは、シンボルの実際の読み込みを実行します。

## <a name="see-also"></a>関連項目
- [LoadSymbols](../../../extensibility/debugger/reference/idebugengine3-loadsymbols.md)
- [IDebugEngine3](../../../extensibility/debugger/reference/idebugengine3.md)
