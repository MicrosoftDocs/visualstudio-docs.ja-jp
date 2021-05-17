---
description: このインターフェイスは、デバッグ エンジン (DE) によって送信され、デバッグ中のモジュールのデバッグ シンボルが読み込まれたことを示します。
title: IDebugSymbolSearchEvent2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugSymbolSearchEvent2
helpviewer_keywords:
- IDebugSymbolSearchEvent2
ms.assetid: 9b946d55-ff85-44eb-b40a-efbf8282eafd
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 5a4ef5008740f563f2f7f986f73c8bbfbb94ef6b
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105053140"
---
# <a name="idebugsymbolsearchevent2"></a>IDebugSymbolSearchEvent2
このインターフェイスは、デバッグ エンジン (DE) によって送信され、デバッグ中のモジュールのデバッグ シンボルが読み込まれたことを示します。

## <a name="syntax"></a>構文

```
IDebugSymbolSearchEvent2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 DE では、モジュールのシンボルが読み込まれたことを報告するために、このインターフェイスを実装します。 [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md) インターフェイスは、このインターフェイスと同じオブジェクトに実装する必要があります。 `IDebugEvent2` インターフェイスにアクセスするために SDM によって [QueryInterface](/cpp/atl/queryinterface) が使用されます。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 DE では、モジュールのシンボルが読み込まれたことを報告するために、このイベント オブジェクトを作成して送信します。 このイベントは、SDM がデバッグ対象のプログラムにアタッチされたときに提供される [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md) コールバック関数を使用して送信されます。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 `IDebugSymbolSearchEvent2` インターフェイスでは、以下のメソッドが公開されます。

|メソッド|説明|
|------------|-----------------|
|[GetSymbolSearchInfo](../../../extensibility/debugger/reference/idebugsymbolsearchevent2-getsymbolsearchinfo.md)|シンボル検索の結果に関する情報を取得します。|

## <a name="remarks"></a>解説
 このイベントは、シンボルの読み込みに失敗した場合でも送信されます。 このイベントのハンドラーで `IDebugSymbolSearchEvent2::GetSymbolSearchInfo` を呼び出すと、モジュールに実際にシンボルがあるかどうかを判定できます。

 Visual Studio では、通常、このイベントを使用して、 **[モジュール]** ウィンドウで読み込まれたシンボルの状態を更新します。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [コア インターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)
- [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)
