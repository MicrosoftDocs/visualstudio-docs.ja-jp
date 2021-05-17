---
description: このインターフェイスでは、ユーザーに報告されるエラー メッセージを指定します。
title: IDebugErrorEvent2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugErrorEvent2
helpviewer_keywords:
- IDebugErrorEvent2 interface
ms.assetid: 275b6f38-b3d4-4cae-8491-491177f524fb
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: d531180ca2fad9a6605837105c4ec5d626584a19
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105054232"
---
# <a name="idebugerrorevent2"></a>IDebugErrorEvent2
このインターフェイスでは、ユーザーに報告されるエラー メッセージを指定します。

## <a name="syntax"></a>構文

```
IDebugErrorEvent2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 デバッグ エンジン (DE) では、エラーを人間が判読できるメッセージとして報告するために、このインターフェイスを実装します。 [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md) インターフェイスは、このインターフェイスと同じオブジェクトに実装する必要があります。 `IDebugEvent2` インターフェイスにアクセスするために SDM によって [QueryInterface](/cpp/atl/queryinterface) が使用されます。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 DE では、エラーを報告するために、このイベント オブジェクトを作成して送信します。 このイベントは、SDM がデバッグ対象のプログラムにアタッチされたときに提供される [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md) コールバック関数を使用して送信されます。

## <a name="methods-in-vtable-order"></a>Vtable の順序でのメソッド
 このインターフェイスには、次のメソッドが実装されています。

|メソッド|説明|
|------------|-----------------|
|`GetErrorMessage`|エラーを人間が判読できる文字列として返します。|

## <a name="remarks"></a>解説
 デバッグ エンジンでエラーが検出された場合、このインターフェイスを使用して、Visual Studio を介してユーザーにメッセージを報告できます。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)
- [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)
