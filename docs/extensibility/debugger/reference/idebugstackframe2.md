---
description: このインターフェイスは、特定のスレッドの呼び出し履歴に含まれる 1 つのスタック フレームを表します。
title: IDebugStackFrame2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugStackFrame2
helpviewer_keywords:
- IDebugStackFrame2 interface
ms.assetid: bd212a6a-dcc6-4756-a77a-e8dfda38b104
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: f9675627bf3044258a532ca91768619f2c6de3ba
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105053257"
---
# <a name="idebugstackframe2"></a>IDebugStackFrame2
このインターフェイスは、特定のスレッドの呼び出し履歴に含まれる 1 つのスタック フレームを表します。

## <a name="syntax"></a>構文

```
IDebugStackFrame2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 デバッグ エンジン (DE) では、スタック フレームを表すために、このインターフェイスを実装します。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 [IEnumDebugFrameInfo2](../../../extensibility/debugger/reference/ienumdebugframeinfo2.md) インターフェイスを取得するには、[EnumFrameInfo](../../../extensibility/debugger/reference/idebugthread2-enumframeinfo.md) を呼び出します。 `IDebugStackFrame2` インターフェイスを含む [FRAMEINFO](../../../extensibility/debugger/reference/frameinfo.md) 構造体を取得するには、[Next](../../../extensibility/debugger/reference/ienumdebugframeinfo2-next.md) を呼び出します。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に、`IDebugStackFrame2` のメソッドを示します。

|メソッド|説明|
|------------|-----------------|
|[GetCodeContext](../../../extensibility/debugger/reference/idebugstackframe2-getcodecontext.md)|このスタック フレームのコード コンテキストを取得します。|
|[GetDocumentContext](../../../extensibility/debugger/reference/idebugstackframe2-getdocumentcontext.md)|このスタック フレームのドキュメント コンテキストを取得します。|
|[GetName](../../../extensibility/debugger/reference/idebugstackframe2-getname.md)|スタック フレームの名前を取得します。|
|[GetInfo](../../../extensibility/debugger/reference/idebugstackframe2-getinfo.md)|スタック フレームの説明を取得します。|
|[GetPhysicalStackRange](../../../extensibility/debugger/reference/idebugstackframe2-getphysicalstackrange.md)|スタック フレームに関連付けられている物理アドレスの範囲の、コンピューターに依存する表現を取得します。|
|[GetExpressionContext](../../../extensibility/debugger/reference/idebugstackframe2-getexpressioncontext.md)|スタック フレームとスレッドの現在のコンテキスト内で式の評価を実行するための評価コンテキストを取得します。|
|[GetLanguageInfo](../../../extensibility/debugger/reference/idebugstackframe2-getlanguageinfo.md)|スタック フレームに関連付けられている言語を取得します。|
|[GetDebugProperty](../../../extensibility/debugger/reference/idebugstackframe2-getdebugproperty.md)|スタック フレームに関連付けられているプロパティの説明を取得します。|
|[EnumProperties](../../../extensibility/debugger/reference/idebugstackframe2-enumproperties.md)|スタック フレーム プロパティの列挙子を作成します。|
|[GetThread](../../../extensibility/debugger/reference/idebugstackframe2-getthread.md)|スタック フレームに関連付けられているスレッドを取得します。|

## <a name="remarks"></a>解説
 このインターフェイスは、デバッグ中のプログラムがブレークポイントで停止された場合にのみ取得されます (ユーザー設定のブレークポイントまたは例外によって発生します)。 このインターフェイスから式のコンテキストを取得して、式の評価、レジスタのリストの返却、または呼び出し履歴の取得と検査を行うことができます。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [コア インターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
