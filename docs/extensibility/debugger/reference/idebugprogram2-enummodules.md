---
description: このプログラムによって読み込まれ、実行されているモジュールの一覧を取得します。
title: IDebugProgram2::EnumModules | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgram2::EnumModules
helpviewer_keywords:
- IDebugProgram2::EnumModules
ms.assetid: 876ac9da-3b7c-4156-b79a-8f340e9fcea6
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: af640cf7e76da0e6cf7bb202cda08792c783e0d5
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105076031"
---
# <a name="idebugprogram2enummodules"></a>IDebugProgram2::EnumModules
このプログラムによって読み込まれ、実行されているモジュールの一覧を取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT EnumModules( 
   IEnumDebugModules2** ppEnum
);
```

```csharp
int EnumModules( 
   out IEnumDebugModules2 ppEnum
);
```

## <a name="parameters"></a>パラメーター
`ppEnum`\
[出力] モジュールの一覧を含む [IEnumDebugModules2](../../../extensibility/debugger/reference/ienumdebugmodules2.md) オブジェクトを返します。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>解説
 モジュールは DLL またはアセンブリであり、通常は **[モジュール]** デバッグ ウィンドウに表示されます。

## <a name="see-also"></a>関連項目
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
- [IEnumDebugModules2](../../../extensibility/debugger/reference/ienumdebugmodules2.md)
