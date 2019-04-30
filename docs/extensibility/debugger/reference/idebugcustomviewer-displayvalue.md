---
title: IDebugCustomViewer::DisplayValue |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugCustomViewer::DisplayValue
helpviewer_keywords:
- IDebugCustomViewer::DisplayValue
ms.assetid: 7a538248-5ced-450e-97cd-13fabe35fb1c
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 8734d97dfc8bcd7be2b12ce657071597deaea7a8
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "62921621"
---
# <a name="idebugcustomviewerdisplayvalue"></a>IDebugCustomViewer::DisplayValue
このメソッドは、指定した値を表示します。

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

#### <a name="parameters"></a>パラメーター
 `hwnd`

 [in]親ウィンドウ

 `dwID`

 [in]1 つ以上の種類をサポートしているカスタム ビューアーの ID。

 `pHostServices`

 [in] 予約されています。 常に設定を null にします。

 `pDebugProperty`

 [in]表示される値を取得するために使用するインターフェイスです。

## <a name="return-value"></a>戻り値
 成功した場合、返します`S_OK`; エラー コードを返します。

## <a name="remarks"></a>Remarks
 表示です。"modal"でこのメソッドは、必要な期間を作成、値を表示、入力を待機すべて呼び出し元に返す前に、ウィンドウを閉じます。 つまり、メソッドの出力では、ウィンドウを破棄するためのユーザー入力を待機するウィンドウの作成からのプロパティの値を表示するすべての側面を処理する必要があります。

 値の変更をサポートするために、指定された[IDebugProperty3](../../../extensibility/debugger/reference/idebugproperty3.md)オブジェクトを使用することができます、 [SetValueAsStringWithError](../../../extensibility/debugger/reference/idebugproperty3-setvalueasstringwitherror.md)メソッド: 場合は、値を文字列として表現できます。 それ以外の場合、カスタム インターフェイスを作成する必要が、これを実装する、式エバリュエーターに限定`DisplayValue`メソッド-を実装するオブジェクトと同じで、`IDebugProperty3`インターフェイス。 このカスタム インターフェイスが、任意のサイズおよび複雑さのデータを変更するためのメソッドを提供します。

## <a name="see-also"></a>関連項目
- [IDebugCustomViewer](../../../extensibility/debugger/reference/idebugcustomviewer.md)
- [IDebugProperty3](../../../extensibility/debugger/reference/idebugproperty3.md)
- [SetValueAsStringWithError](../../../extensibility/debugger/reference/idebugproperty3-setvalueasstringwitherror.md)