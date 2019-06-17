---
title: IDebugSymbolSearchEvent2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugSymbolSearchEvent2
helpviewer_keywords:
- IDebugSymbolSearchEvent2
ms.assetid: 9b946d55-ff85-44eb-b40a-efbf8282eafd
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: ed7108c9e1349b01115bed8a6b2a77a3eaa71f45
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66320388"
---
# <a name="idebugsymbolsearchevent2"></a>IDebugSymbolSearchEvent2
このインターフェイスは、デバッグ中のモジュールのデバッグ シンボルが読み込まれたことを示すためにデバッグ エンジン (DE) によって送信されます。

## <a name="syntax"></a>構文

```
IDebugSymbolSearchEvent2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装についてのメモ
 デでは、モジュールのシンボルが読み込まれたことを報告するには、このインターフェイスを実装します。 [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)このインターフェイスと同じオブジェクトでインターフェイスを実装する必要があります。 SDM を使用して[QueryInterface](/cpp/atl/queryinterface)にアクセスする、`IDebugEvent2`インターフェイス。

## <a name="notes-for-callers"></a>呼び出し元のノート
 デは作成し、モジュールのシンボルが読み込まれたことを報告するには、このイベント オブジェクトを送信します。 使用して、イベントが送信される、 [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)デバッグ中のプログラムに添付するときに、SDM によって指定されたコールバック関数。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 `IDebugSymbolSearchEvent2`インターフェイスは、次のメソッドを公開します。

|メソッド|説明|
|------------|-----------------|
|[GetSymbolSearchInfo](../../../extensibility/debugger/reference/idebugsymbolsearchevent2-getsymbolsearchinfo.md)|シンボルの検索の結果に関する情報を取得します。|

## <a name="remarks"></a>Remarks
 シンボルの読み込みに失敗した場合でも、このイベントが送信されます。 呼び出す`IDebugSymbolSearchEvent2::GetSymbolSearchInfo`かどうか、モジュール、実際には、シンボルを確認するには、このイベントのハンドラーを使用します。

 Visual Studio が通常このイベントを使用で読み込まれているシンボルの状態を更新して、**モジュール**ウィンドウ。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ:Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [コア インターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)
- [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)