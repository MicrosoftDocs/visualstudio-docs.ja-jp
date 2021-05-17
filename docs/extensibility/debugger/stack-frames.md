---
title: スタック フレーム | Microsoft Docs
description: この記事では、Visual Studio のデバッガー アーキテクチャにおけるスタック フレームの定義と役割について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- stack frames, debugging
- debugging [Debugging SDK], stack frames
- stack frames
ms.assetid: b5e439d4-1e9d-4e13-9cad-bb8b136d4ca8
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: b0c54292d79b119fc36c9eff3f0f3519c92a4205
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105079396"
---
# <a name="stack-frames"></a>スタック フレーム
デバッガー アーキテクチャでは、"*スタック フレーム*" は次のようなものです。

- スレッドの実行コンテキストを提供するスタックを抽象化したものです。 スレッドは、常に関数内で実行されます。 スタック フレームには、関数のローカル変数とそれに対する引数が保持されます。 Visual Studio でデバッグするには、デバッグ対象の言語または環境でスタック フレームがサポートされている必要があります。

- 自身を識別して記述することができ、関連付けられているスレッドを返すことができます。 スタック フレームでは、現在の命令ポインターを表すコード コンテキストと、関連付けられているドキュメントおよび式の評価のコンテキストを返すこともできます。

- ローカル変数と引数の名前、型、および値を記述するプロパティがあり、さまざまな IDE デバッグ ウィンドウに表示されます。

- [IDebugStackFrame2](../../extensibility/debugger/reference/idebugstackframe2.md) インターフェイスによって表されます。このインターフェイスは、通常は、プログラムを実行した結果として、デバッグ エンジン (DE) または仮想マシンによって作成されます。

## <a name="see-also"></a>関連項目
- [デバッガー コンテキスト](../../extensibility/debugger/debugger-contexts.md)
- [デバッガーの概念](../../extensibility/debugger/debugger-concepts.md)
- [デバッグ エンジン](../../extensibility/debugger/debug-engine.md)
- [IDebugStackFrame2](../../extensibility/debugger/reference/idebugstackframe2.md)
