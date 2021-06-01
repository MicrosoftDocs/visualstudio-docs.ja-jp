---
description: ポートの名前を取得します。
title: IDebugPortRequest2::GetPortName | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPortRequest2::GetPortName
helpviewer_keywords:
- IDebugPortRequest2::GetPortName
ms.assetid: 53e2a3a4-bb34-4a02-a983-6bd84ea70587
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 89bff19026a8bbdab72f1bec84c5feef0b37d8c6
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105072235"
---
# <a name="idebugportrequest2getportname"></a>IDebugPortRequest2::GetPortName
ポートの名前を取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetPortName( 
   BSTR* pbstrPortName
);
```

```csharp
int GetPortName( 
   out string pbstrPortName
);
```

## <a name="parameters"></a>パラメーター
`pbstrPortName`\
[出力] ポートの名前を返します。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>解説
 [IDebugPortRequest2](../../../extensibility/debugger/reference/idebugportrequest2.md) インターフェイスは、ポートへの接続を取得するために、通常はデバッグ パッケージ (クライアント) からポート サプライヤー (サーバー) に渡されます。 ポートの選択肢は、デバッグ パッケージとポート サプライヤーの両方から認識されています。 単純な文字列でポートを記述できる場合、メソッドには `IDebugPortRequest2::GetPortName` 接続に必要な情報が含まれています。 それ以外の場合、クライアントで追加のインターフェイスを提供できます。これは、`IDebugPortRequest2::QueryInterface` を使用してサーバーで取得できます。

## <a name="see-also"></a>関連項目
- [IDebugPortRequest2](../../../extensibility/debugger/reference/idebugportrequest2.md)
