---
title: デバッグのための言語サービスのサポート | Microsoft Docs
description: Visual Studio でのデバッグのサポートを提供する IVsLanguageDebugInfo インターフェイスの言語サービス機能について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugger, language support
- language services, debugging support
ms.assetid: 7a44067f-a410-4a6a-84d2-bda5184140bc
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 2c00d0af21d5d165b7733267e0a97ae71ca6e573
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105074575"
---
# <a name="language-service-support-for-debugging"></a>デバッグのための言語サービスのサポート
言語サービスは、<xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageDebugInfo> インターフェイスを介してデバッガーをサポートする機能を提供できます。 これらの機能には、ブレークポイントの検証や、 **[自動変数]** ウィンドウへの式の一覧の指定が含まれます。

 ただし、言語をデバッグするには、式エバリュエーターが必要です。 式エバリュエーターは、デバッグ中に値を生成する式を評価します。 CLR 式エバリュエーターの実装の詳細については、以下を参照してください。

- [CLR 式エバリュエーター](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)

- [マネージド式エバリュエーターのサンプル](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)

## <a name="compiler-output"></a>コンパイラの出力
 コンパイラの種類によって、言語のデバッグを実装するために何をする必要があるかが決まります。 コンパイラが Windows オペレーティング システムを対象としていて、.pdb ファイルを記述する場合は、Visual Studio に統合されているネイティブ コードのデバッグ エンジンを使用してプログラムをデバッグすることができます。 コンパイラが Microsoft 中間言語 (MSIL) を生成する場合は、マネージド コードのデバッグ エンジン (これも Visual Studio に統合されています) でプログラムをデバッグすることができます。 コンパイラが独自のオペレーティング システムまたは別のランタイム環境を対象としている場合は、独自のデバッグ エンジンを作成する必要があります。

 言語のデバッグの実装の詳細については、Visual Studio Debugging SDK の[概要](../../extensibility/debugger/getting-started-with-debugger-extensibility.md)に関するページを参照してください。
