---
title: Visual Studio デバッガーの拡張性 | Microsoft Docs
description: この記事では、Visual Studio デバッガーの拡張性について説明し、Visual Studio のデバッグに関する記事へのリンクを示します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Visual Studio], Debugging SDK
- Debugging SDK
ms.assetid: c088b6a2-c3ad-446b-830d-9c6f41b2934b
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: dbc44da3f98555774dd62c2b061bbf3a0799926e
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105057729"
---
# <a name="visual-studio-debugger-extensibility"></a>Visual Studio デバッガーの拡張性
Visual Studio には、完全にインタラクティブなソース コード デバッガーが含まれており、プログラムのバグを追跡するための強力で使いやすいツールを提供します。 デバッガーは、Visual Basic、C#、C/C++、および JavaScript を完全にサポートしています。 ただし、[Microsoft ダウンロード センター](https://www.microsoft.com/download/details.aspx?id=21835)から入手できる [!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)] を使用すると、同じ豊富な機能を備えたデバッガーで他のプログラミング言語をサポートできます。

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] デバッガーは、デバッグ対象の言語に固有の、デバッグ コンポーネントへの共通のフロントエンド (つまり、ユーザー インターフェイス) です。 新しい言語では、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] デバッガーによるサポートに必要なのは、デバッグ エンジン (DE) などの必要なバックエンド コンポーネントを作成することだけです。 このようなときに [!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)] が役に立ちます。

 [!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)] には、新しい DE を作成するために必要なすべての [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 要素への完全な参照が含まれています。 また、作業を開始するためのサンプルとチュートリアルも用意されています。

 デバッグをサポートする言語プロジェクト システムの完全なサンプルについては、[IronPython サンプル](https://www.microsoft.com/download/details.aspx?id=55984)を参照してください。

 次のセクションでは、[!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)] を使用してデバッガーを拡張する方法について説明します。

## <a name="in-this-section"></a>このセクションの内容
 [概要](../../extensibility/debugger/getting-started-with-debugger-extensibility.md)では、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] デバッグの機能と SDK をインストールする方法について説明します。

 [カスタム デバッグ エンジンを作成する](../../extensibility/debugger/creating-a-custom-debug-engine.md)では、DE のためのプログラムの準備から DE のデタッチまで、カスタム DE プロセスについて説明します。

 [CLR 式エバリュエーターを記述する](../../extensibility/debugger/writing-a-common-language-runtime-expression-evaluator.md)では、式エバリュエーターを記述する必要があるかどうかについて説明します。

 [デバッグ エンジンの実装方法を選択する](../../extensibility/debugger/choosing-a-debug-engine-implementation-strategy.md)では、DE を実装する方法について説明します。

 [参照](../../extensibility/debugger/reference/reference-visual-studio-debugging-apis.md)では、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] デバッグ API について説明します。

 [サンプル](../../extensibility/debugger/visual-studio-debugging-samples.md)には、共通言語ランタイムの式エバリュエーター サンプルとデバッグ エンジン サンプルへのリンクが含まれています。
