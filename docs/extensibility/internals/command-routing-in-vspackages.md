---
title: VSPackage のコマンド ルーティング | Microsoft Docs
description: VSPackage のコマンド ルーティングと、Visual Studio で実行されるコンテキストに基づいてコマンドがどのようにルーティングされるかについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- commands, routing
- command routing, Visual Studio SDK
ms.assetid: a9c7f9ae-3594-4557-a314-8cf76f5f8772
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 35ab5e7989fdeb46592f38cb7e55854885e076d1
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105057300"
---
# <a name="command-routing-in-vspackages"></a>Vspackage のコマンド ルーティング
コマンドは、実行されるコンテキストに基づいて [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 内でルーティングされます。 これは初期コンテキストからグローバル コンテキストにルーティングされます。

## <a name="in-this-section"></a>このセクションの内容
- [コマンド ルーティング アルゴリズム](../../extensibility/internals/command-routing-algorithm.md)

 コマンド ルーティングの解決順序について説明します。

- [コマンドの可用性](../../extensibility/internals/command-availability.md)

 コマンド ルーティングについて説明します。

- [相互運用機能アセンブリを使用するコマンドとメニュー](../../extensibility/internals/commands-and-menus-that-use-interop-assemblies.md)

 マネージド コードと COM 間でコマンドをルーティングする際の考慮事項について説明します。

## <a name="related-sections"></a>関連項目
- [選択コンテキスト オブジェクト](../../extensibility/internals/selection-context-objects.md)

 ウィンドウ上のユーザーの選択コンテキストのフォーカスを決定する方法のモデルについて説明します。

- [コマンド、メニュー、およびツール バー](../../extensibility/internals/commands-menus-and-toolbars.md)

 メニュー、ツール バー、およびコマンド コンボ ボックスが含まれている UI を作成する方法について説明します。
