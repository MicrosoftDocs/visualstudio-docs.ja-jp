---
title: 呼び出し履歴の評価 | Microsoft Docs
description: EnumFrameInfo メソッドと、これを実装して中断モード中に呼び出し履歴のスタック フレームを表示する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- debugging [Debugging SDK], call stack evaluation
- call stacks, evaluation
ms.assetid: 373d6b49-0459-4cce-816e-05745a44fe49
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 059c42349c7f8e681709d69104cf65a6fc245206
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2021
ms.locfileid: "112898540"
---
# <a name="call-stack-evaluation"></a>呼び出し履歴の評価
中断モード中に呼び出し履歴のスタック フレームを表示するには、[EnumFrameInfo](../../extensibility/debugger/reference/idebugthread2-enumframeinfo.md) メソッドを実装する必要があります。

## <a name="methods-for-evaluation"></a>評価用のメソッド
 単純なデバッグ エンジン (DE) には、スタック フレームが 1 つしか存在しない可能性があります。 中断モード中にスタック フレームを調べるには、[IDebugStackFrame2](../../extensibility/debugger/reference/idebugstackframe2.md) の次のメソッドを実装する必要があります。

|メソッド|説明|
|------------|-----------------|
|[GetCodeContext](../../extensibility/debugger/reference/idebugstackframe2-getcodecontext.md)|このスタック フレームのコード コンテキストを取得します。 コード コンテキストは、スタック フレーム内の現在の命令ポインターを表します。|
|[GetDocumentContext](../../extensibility/debugger/reference/idebugstackframe2-getdocumentcontext.md)|このスタック フレームのドキュメント コンテキストを取得します。 ドキュメント コンテキストは、スタック フレームのソース コードにおける現在の場所を表します。 プログラム内で停止したときにソース コードを表示するために必要です。|

 これらのメソッドには、コンテキストに関するいくつかのインターフェイスとメソッドの実装が必要です。 したがって、[GetDocumentContext](../../extensibility/debugger/reference/idebugcodecontext2-getdocumentcontext.md) メソッドと [IDebugDocumentContext2](../../extensibility/debugger/reference/idebugdocumentcontext2.md) の次のメソッドを実装する必要があります。

|メソッド|説明|
|------------|-----------------|
|[GetStatementRange](../../extensibility/debugger/reference/idebugdocumentcontext2-getstatementrange.md)|ドキュメント コンテキストのファイル ステートメントの範囲を取得します。|

 コード コンテキストを列挙するには、[IEnumDebugCodeContexts2](../../extensibility/debugger/reference/ienumdebugcodecontexts2.md) のすべてのメソッドを実装する必要があります。

## <a name="see-also"></a>関連項目
- [実行の制御と状態の評価](../../extensibility/debugger/execution-control-and-state-evaluation.md)
