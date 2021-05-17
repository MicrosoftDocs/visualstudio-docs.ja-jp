---
description: このリファレンス セクションには、API の概念の概要、API のすべての要素の構文と使用法を示すガイド、およびさまざまなコード例が含まれています。
title: API リファレンス (Visual Studio のデバッグ) | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- debugging [Debugging SDK], API reference
ms.assetid: e4e429da-3667-41f7-9158-a8207d13e91a
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: a8a43e4bae5afce98e07b196f5a01c33d44c72ca
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105085547"
---
# <a name="api-reference-visual-studio-debugging"></a>API 参照 (Visual Studio のデバッグ)
このリファレンス セクションには、API の概念の概要、API のすべての要素の構文と使用法を示すガイド、およびさまざまなコード例が含まれています。 すべてのリファレンスは、カテゴリ別にアルファベット順に一覧表示されています。

 次の表は、メソッドによって返される一般的な `HRESULT` 値を示しています。

|名前|説明|値|
|----------|-----------------|-----------|
|S_OK|正常終了しました。|0x00000000|
|E_UNEXPECTED|予期しないエラーです。|0x8000FFFF|
|E_NOTIMPL|実装されていません。|0x80004001|
|E_OUTOFMEMORY|操作を完了させるための十分なメモリがありません。|0x8007000E|
|E_INVALIDARG|1 つ以上の引数が無効です。|0x80070057|
|E_NOINTERFACE|そのようなインターフェイスはサポートされていません。|0x80004002|
|E_POINTER|ポインターが無効です。|0x80004003|
|E_HANDLE|ハンドルが無効です。|0x80070006|
|E_ABORT|操作は中止されました。|0x80004004|
|E_FAIL|予期しないエラーです。|0x80004005|
|E_ACCESSDENIED|一般的なアクセス拒否エラーが発生しました。|0x80070005|

> [!NOTE]
> [!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)] のデバッグ メソッドから `S_OK` が戻される場合、すべての出力パラメーターのポインターが有効であることが想定されています。つまり、`S_OK` が返されるときに、出力パラメーターのポインターに対して検証は実行されません。
>
> [!NOTE]
> 無効または `NULL` の [出力] パラメーターがある場合は、IDE がクラッシュすることがあります。

## <a name="see-also"></a>関連項目
- [インターフェイス](../../../extensibility/debugger/reference/interfaces-visual-studio-debugging.md)
- [列挙型](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [構造体と共用体](../../../extensibility/debugger/reference/structures-and-unions.md)
- [デバッグ用 SDK ヘルパー](../../../extensibility/debugger/reference/sdk-helpers-for-debugging.md)
- [Visual Studio デバッガーの機能拡張](../../../extensibility/debugger/visual-studio-debugger-extensibility.md)
