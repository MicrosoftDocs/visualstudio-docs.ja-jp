---
description: このメソッドは、指定された値を表示するために呼び出されます。
title: IDebugCustomViewer::DisplayValue | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugCustomViewer::DisplayValue
helpviewer_keywords:
- IDebugCustomViewer::DisplayValue
ms.assetid: 7a538248-5ced-450e-97cd-13fabe35fb1c
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 11a93ba7a3367a9ff61debfe338c349549ee429d
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105077578"
---
# <a name="idebugcustomviewerdisplayvalue"></a>IDebugCustomViewer::DisplayValue
このメソッドは、指定された値を表示するために呼び出されます。

## <a name="syntax"></a>構文

```cpp
HRESULT DisplayValue(
   HWND             hwnd,
   DWORD            dwID,
   IUnknown *       pHostServices,
   IDebugProperty3* pDebugProperty);
);
```

```csharp
int DisplayValue(
   IntPtr          hwnd,
   uint            dwID,
   object          pHostServices,
   IDebugProperty3 pDebugProperty
);
```

## <a name="parameters"></a>パラメーター
`hwnd`\
[入力] 親ウィンドウ

`dwID`\
[入力] 複数の種類をサポートするカスタム ビューアーの ID。

`pHostServices`\
[in] 予約されています。 常に null に設定します。

`pDebugProperty`\
[入力] 表示される値を取得するために使用できるインターフェイス。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>解説
 このメソッドでは必要なウィンドウを作成し、値を表示し、入力を待機し、ウィンドウを閉じ、それらすべてが終了してから呼び出し元に戻るという点で、表示は "モーダル" です。 つまり、メソッドでは、出力用のウィンドウの作成から、ユーザー入力を待機し、ウィンドウを破棄するまで、プロパティの値の表示に関するすべての側面を処理する必要があります。

 指定された [IDebugProperty3](../../../extensibility/debugger/reference/idebugproperty3.md) オブジェクトの値の変更をサポートするために、値を文字列として表現できる場合は、[SetValueAsStringWithError](../../../extensibility/debugger/reference/idebugproperty3-setvalueasstringwitherror.md) メソッドを使用できます。 それ以外の場合は、`IDebugProperty3` インターフェイスを実装するのと同じオブジェクト上で、この `DisplayValue` メソッドを実装する式エバリュエーターに限定したカスタム インターフェイスを作成する必要があります。 このカスタム インターフェイスでは、任意のサイズまたは複雑度のデータを変更するためのメソッドを用意します。

## <a name="see-also"></a>関連項目
- [IDebugCustomViewer](../../../extensibility/debugger/reference/idebugcustomviewer.md)
- [IDebugProperty3](../../../extensibility/debugger/reference/idebugproperty3.md)
- [SetValueAsStringWithError](../../../extensibility/debugger/reference/idebugproperty3-setvalueasstringwitherror.md)
