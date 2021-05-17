---
title: 共通言語ランタイムの式エバリュエーターの書き込み | Microsoft Docs
description: デバッグ対象のコード言語で式を評価する、共通言語ランタイムの式エバリュエーターの記述について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- expression evaluators, tutorial
- expression evaluation, samples
- debugging [Debugging SDK], expression evaluators tutorial
ms.assetid: bd79d57f-8e0a-4e14-a417-0b1de28fa1b2
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 658158785d8f8a9376f5357ae2b869f6ad2e2271
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105091397"
---
# <a name="writing-a-common-language-runtime-expression-evaluator"></a>共通言語ランタイム式のエバリュエーターを記述する
> [!IMPORTANT]
> Visual Studio 2015 では、この方法での式エバリュエーターの実装は非推奨です。 CLR 式エバリュエーターの実装については、[CLR 式エバリュエーター](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)に関する記事と[マネージド式エバリュエーターのサンプル](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)に関する記事をご覧ください。

 式エバリュエーター (EE) はデバッグ エンジン (DE) の一部であり、デバッグ対象のコードを生成したプログラミング言語の構文とセマンティクスを処理します。 式は、プログラミング言語のコンテキスト内で評価される必要があります。 たとえば、一部の言語では、"A + B" という式は "A と B の合計" を意味します。 他の言語では、同じ式が "A または B" を意味する場合があります。 そのため、Visual Studio IDE でデバッグするオブジェクト コードを生成するプログラミング言語ごとに、別個の EE を記述する必要があります。

 Visual Studio デバッグ パッケージの一部の側面では、プログラミング言語のコンテキストでコードを解釈する必要があります。 たとえば、ブレークポイントで実行が停止した場合、ユーザーが **[ウォッチ]** ウィンドウに入力したすべての式が評価され、表示される必要があります。 ユーザーは、 **[ウォッチ]** ウィンドウまたは **[イミディエイト]** ウィンドウに式を入力することによって、ローカル変数の値を変更することができます。

## <a name="in-this-section"></a>このセクションの内容
 [共通言語ランタイムおよび式の評価](../../extensibility/debugger/common-language-runtime-and-expression-evaluation.md) 独自のプログラミング言語を Visual Studio IDE に統合する場合、独自の言語のコンテキスト内で式を評価できる EE を記述することで、デバッグ エンジンを記述せずに Microsoft Intermediate Language (MSIL) にコンパイルできることについて説明します。

 [式エバリュエーターのアーキテクチャ](../../extensibility/debugger/expression-evaluator-architecture.md) 必須の EE インターフェイスを実装し、共通言語ランタイムのシンボル プロバイダー (SP) とバインダー インターフェイスを呼び出す方法について説明します。

 [式エバリュエーターを登録する](../../extensibility/debugger/registering-an-expression-evaluator.md) EE は、それ自体を共通言語ランタイム環境と Visual Studio ランタイム環境の両方にクラス ファクトリとして登録する必要があることに注目しています。

 [式エバリュエーターを実装する](../../extensibility/debugger/implementing-an-expression-evaluator.md) 式を評価するプロセスに、デバッグ エンジン (DE)、シンボル プロバイダー (SP)、バインダー オブジェクト、および式エバリュエーター (EE) がどのように含まれるかについて説明します。

 [ローカルの表示](../../extensibility/debugger/displaying-locals.md) 実行が一時停止したときに、デバッグ パッケージがローカル変数と引数の一覧を取得するために、どのように DE を呼び出すかについて説明します。

 [ウォッチ ウィンドウの式の評価](../../extensibility/debugger/evaluating-a-watch-window-expression.md) Visual Studio のデバッグ パッケージが、ウォッチ リスト内の各式の現在の値を確認するために DE を呼び出す方法について説明します。

 [ローカルの値を変更する](../../extensibility/debugger/changing-the-value-of-a-local.md) ローカルの値を変更するときに、[ローカル] ウィンドウの各行に、ローカルの名前、型、および現在の値を提供するオブジェクトが関連付けられていることについて説明します。

 [型のビジュアライザーとカスタム ビューアーの実装](../../extensibility/debugger/implementing-type-visualizers-and-custom-viewers.md) 型のビジュアライザーとカスタム ビューアーをサポートするために、コンポーネントによって実装する必要があるインターフェイスについて説明します。

## <a name="see-also"></a>関連項目
 [Visual Studio デバッガーの機能拡張](../../extensibility/debugger/visual-studio-debugger-extensibility.md)
