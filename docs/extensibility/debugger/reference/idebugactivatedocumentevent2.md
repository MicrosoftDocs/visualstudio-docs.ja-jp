---
description: デバッグ エンジン (DE) は、このインターフェイスを使用してドキュメントの読み込みを要求します。
title: IDebugActivateDocumentEvent2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugActivateDocumentEvent2
helpviewer_keywords:
- IDebugActivateDocumentEvent2 interface
ms.assetid: 6f37edd7-a48c-4b41-b160-dff9be63a284
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: dbf24620b3dfa508a52463598219be4b2d7439a8
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105094404"
---
# <a name="idebugactivatedocumentevent2"></a>IDebugActivateDocumentEvent2
デバッグ エンジン (DE) は、このインターフェイスを使用してドキュメントの読み込みを要求します。

## <a name="syntax"></a>構文

```
IDebugActivateDocumentEvent2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 DE は、ソース ファイルを開く必要があるときに、このインターフェイスを実装します。 このインターフェイスは、スクリプト インタープリターを操作する、またはその一部である、デバッグ エンジンによってのみ実装されます。 [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md) インターフェイスは、このインターフェイスと同じオブジェクトに実装する必要があります (SDM では、[QueryInterface](/cpp/atl/queryinterface) メソッドを使用して `IDebugEvent2` インターフェイスにアクセスします)。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 DE は、ソース ファイルを開く必要があるときに、このイベント オブジェクトを作成して送信します。 このイベントは、SDM がデバッグ対象のプログラムにアタッチされたときに提供される [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md) コールバック関数を使用して送信されます。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に、`IDebugActivateDocumentEvent2` のメソッドを示します。

|メソッド|説明|
|-------------|-----------------|
|[GetDocument](../../../extensibility/debugger/reference/idebugactivatedocumentevent2-getdocument.md)|アクティブにするドキュメントを取得します。|
|[GetDocumentContext](../../../extensibility/debugger/reference/idebugactivatedocumentevent2-getdocumentcontext.md)|ドキュメント内の位置を記述するドキュメント コンテキストを取得します。|

## <a name="remarks"></a>解説
 このインターフェイスが使用される一般的なシナリオでは、HTML ページのスクリプト コードで解析エラーが発生した場合に、スクリプト DE がこのインターフェイスを SDM に送信して、解析エラーのあるドキュメントを表示できるようにします。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [IDebugDocument2](../../../extensibility/debugger/reference/idebugdocument2.md)
- [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)
- [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)
