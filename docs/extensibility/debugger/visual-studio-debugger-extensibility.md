---
title: Visual Studio デバッガーの機能拡張 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Visual Studio], Debugging SDK
- Debugging SDK
ms.assetid: c088b6a2-c3ad-446b-830d-9c6f41b2934b
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 58bfec6fa09f6450afb8170d60acad39edacd590
ms.sourcegitcommit: dcbb876a5dd598f2538e62e1eabd4dc98595b53a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/28/2019
ms.locfileid: "72982454"
---
# <a name="visual-studio-debugger-extensibility"></a>Visual Studio デバッガーの機能拡張
Visual Studio には、完全にインタラクティブなソースコードデバッガーが含まれており、プログラムのバグを追跡するための強力で使いやすいツールを提供します。 デバッガーは、Visual Basic、 C#、C/C++、および JavaScript を完全にサポートしています。 ただし、[!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)]では、 [Microsoft ダウンロードセンター](https://www.microsoft.com/download/details.aspx?id=21835)から入手できますが、他のプログラミング言語は、同じ豊富な機能を備えたデバッガーでサポートされています。

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] デバッガーは、デバッグコンポーネントに共通のフロントエンド (つまりユーザーインターフェイス) であり、デバッグ対象の言語に固有のものです。 新しい言語では、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] デバッガーによってサポートされる必要があるのは、デバッグエンジン (DE) などの必要なバックエンドコンポーネントを作成することだけです。 この時点で、[!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)] があります。

 [!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)] には、新しい DE を作成するために必要なすべての [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 要素への完全な参照が含まれています。 また、作業を開始するためのサンプルとチュートリアルも用意されています。

 デバッグをサポートする言語プロジェクトシステムの完全なサンプルについては、 [IronPython サンプル](https://www.microsoft.com/download/details.aspx?id=55984)を参照してください。

 次のセクションでは、[!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)]を使用してデバッガーを拡張する方法について説明します。

## <a name="in-this-section"></a>このセクションの内容
 [はじめ](../../extensibility/debugger/getting-started-with-debugger-extensibility.md)に[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] のデバッグプランと SDK のインストール方法について説明します。

 [カスタムデバッグエンジンを作成する](../../extensibility/debugger/creating-a-custom-debug-engine.md)De をデタッチするためのプログラムの準備から、カスタムの DE プロセスについて説明します。

 [CLR 式エバリュエーターを記述する](../../extensibility/debugger/writing-a-common-language-runtime-expression-evaluator.md)式エバリュエーターを記述する必要があるかどうかについて説明します。

 [デバッグエンジンの実装方法を選択する](../../extensibility/debugger/choosing-a-debug-engine-implementation-strategy.md)DE を実装する方法について説明します。

 [参照](../../extensibility/debugger/reference/reference-visual-studio-debugging-apis.md)[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] デバッグ API について説明します。

 [サンプル](../../extensibility/debugger/visual-studio-debugging-samples.md)共通言語ランタイムの式エバリュエーターサンプルとデバッグエンジンサンプルへのリンクが含まれています。
