---
description: ポートを選択するためのカスタマイズされた UI を表します。
title: IDebugPortPicker | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugPortPicker interface
ms.assetid: 8b7f6685-a3c5-4355-b706-c1b574f6ff84
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 8390c8a055a9c919bb1a35d8f3288fc810e5329d
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105072248"
---
# <a name="idebugportpicker"></a>IDebugPortPicker
ポートを選択するためのカスタマイズされた UI を表します。

## <a name="syntax"></a>構文

```
IDebugPortPicker : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 このインターフェイスはポート サプライヤーによって実装されます。 ポート サプライヤーではポート ピッカーを定義する場合、CLSID としてそれを公開し、`metricPortPickerCLSID` メトリックでその公開された CLSID を指し示します。

## <a name="methods"></a>メソッド
 次の表は、`IDebugPortPicker` のメソッドを示しています。

|メソッド|説明|
|------------|-----------------|
|[DisplayPortPicker](../../../extensibility/debugger/reference/idebugportpicker-displayportpicker.md)|指定されたダイアログ ボックスを表示し、ユーザーがポートを選択できるようにします。|
|[SetSite](../../../extensibility/debugger/reference/idebugportpicker-setsite.md)|サービス プロバイダーを設定します。|

## <a name="requirements"></a>必要条件
 ヘッダー: Msdbg.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll
