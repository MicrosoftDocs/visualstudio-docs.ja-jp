---
description: このデバッグ イベントの属性を取得します。
title: IDebugEvent2::GetAttributes | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEvent2::GetAttributes
helpviewer_keywords:
- IDebugEvent2::GetAttributes
ms.assetid: 2ac5b5fb-da17-43f7-811a-313f677e60d7
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: b41e3f50b73c16c9acb28a809b8c33b535370c47
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105065854"
---
# <a name="idebugevent2getattributes"></a>IDebugEvent2::GetAttributes
このデバッグ イベントの属性を取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetAttribute( 
   DWORD* pdwAttrib
);
```

```csharp
int GetAttribute( 
   out uint pdwAttrib
);
```

## <a name="parameters"></a>パラメーター
`pdwAttrib`\
[出力] [EVENTATTRIBUTES](../../../extensibility/debugger/reference/eventattributes.md) 列挙型からのフラグの組み合わせ。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>解説
 [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md) インターフェイスは、すべてのイベントに共通です。 このメソッドは、たとえばイベントが同期または非同期であるか、およびそれが停止イベントであるかのイベントの種類を表します。

## <a name="see-also"></a>関連項目
- [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)
- [EVENTATTRIBUTES](../../../extensibility/debugger/reference/eventattributes.md)
