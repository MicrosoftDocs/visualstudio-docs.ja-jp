---
description: サーバー上にデバッグ エンジンのインスタンスを作成します。
title: IDebugCoreServer3::CreateInstanceInServer | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugCoreServer3::CreateInstanceInServer
helpviewer_keywords:
- IDebugCoreServer3::CreateInstanceInServer
ms.assetid: 76f36bae-f6ab-413c-a8a9-8808bfeba05b
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 3511e67300725dc46e6d0e3978b2cb034b92d84e
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105058691"
---
# <a name="idebugcoreserver3createinstanceinserver"></a>IDebugCoreServer3::CreateInstanceInServer
サーバー上にデバッグ エンジンのインスタンスを作成します。

## <a name="syntax"></a>構文

```cpp
HRESULT CreateInstanceInServer(
   LPCWSTR  szDll,
   WORD     wLangId,
   REFCLSID clsidObject,
   REFIID   riid,
   void**   ppvObject
);
```

```csharp
int CreateInstanceInServer(
   string     szDll,
   ushort     wLangID,
   ref Guid   clsidObject,
   ref Guid   riid,
   out IntPtr ppvObject
);
```

## <a name="parameters"></a>パラメーター
`szDll`\
[入力] `clsidObject` で指定されたパラメーター CLSID を実装する dll へのパス。 これが `NULL`の場合、COM の `CoCreateInstance` が呼び出されます。

`wLangId`\
[入力] デバッグ エンジンのロケール。 [SetLocale](../../../extensibility/debugger/reference/idebugengine2-setlocale.md) メソッドを呼び出す必要がない場合、これを 0 にすることができます。

`clsidObject`\
[入力] 作成するデバッグ エンジンの CLSID。

`riid`\
[入力] クラス オブジェクトから取得する特定のインターフェイスのインターフェイス ID。

`ppvObject`\
[出力] インスタンスを作成したオブジェクトからの `IUnknown` インターフェイス。 このオブジェクトを目的のインターフェイスにキャストまたはマーシャリングします。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。

## <a name="see-also"></a>関連項目
- [IDebugCoreServer3](../../../extensibility/debugger/reference/idebugcoreserver3.md)
- [SetLocale](../../../extensibility/debugger/reference/idebugengine2-setlocale.md)
