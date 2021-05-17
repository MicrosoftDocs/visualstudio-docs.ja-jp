---
title: デバッガーのコンポーネント | Microsoft Docs
description: デバッグ セッションの構成要素について説明します。このセッションは、VSPackage として実装されている Visual Studio デバッガーによって管理されます。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Visual Studio], components
- components [Visual Studio SDK], debugging
- debugging [Debugging SDK], components
ms.assetid: 8b8ab77f-a134-495c-be42-3bc51aa62dfb
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: b7c558d20d24acd65ece4c4df43eb8f474c20447
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105094953"
---
# <a name="debugger-components"></a>デバッガーのコンポーネント
[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] デバッガーは VSPackage として実装され、デバッグ セッション全体を管理します。 デバッグ セッションは、次の要素で構成されています。

- **デバッグ パッケージ:** [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] デバッガーでは、デバッグする内容に関係なく、同じユーザー インターフェイスが提供されます。

- **セッション デバッグ マネージャー (SDM):** さまざまなデバッグ エンジンを管理するための、一貫性のあるプログラム インターフェイスが [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] デバッガーに提供されます。 これは、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] によって実装されます。

- **プロセス デバッグ マネージャー (PDM):** [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] の実行中の全インスタンスについて、デバッグ可能な、またはデバッグ対象のすべてのプログラムの一覧が管理されます。 これは、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] によって実装されます。

- **デバッグ エンジン (DE):** デバッグ中のプログラムが監視され、実行中のプログラムの状態が SDM と PDM に通知されます。また、式エバリュエーターおよびシンボル プロバイダーと対話して、プログラムのメモリと変数の状態がリアルタイムに分析されます。 これは、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] (サポートされている言語) と独自の実行時間をサポートしたいサードパーティ ベンダーよって実装されます。

- **式エバリュエーター (EE):** 特定の時点でプログラムが停止した際に、ユーザーが指定した変数と式が動的に評価されます。 これは、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] (サポートされている言語)と独自の言語をサポートしたいサードパーティ ベンダーよって実装されます。

- **シンボル プロバイダー (SP):** シンボル ハンドラーとも呼ばれます。プログラムのデバッグ シンボルをプログラムの実行中のインスタンスにマップして、意味のある情報が提供されるようにします (ソースコードレベルのデバッグや式の評価など)。 これは、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] (共通言語ランタイム [CLR] シンボルとプログラム データベース [PDB] のシンボル ファイル形式)、および独自の専用メソッドを使用してデバッグ情報を格納するサードパーティ ベンダーによって実装されます。

  次の図は、Visual Studio デバッガーのこれらの要素間の関係を示しています。

  ![デバッグ コンポーネントの概要](../../extensibility/debugger/media/dbugcompovrview.gif "DBugCompOvrview")

## <a name="in-this-section"></a>このセクションの内容
 [デバッグ パッケージ](../../extensibility/debugger/debug-package.md) - [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] シェルで実行され、すべての UI を処理するデバッグ パッケージについて説明します。

 [プロセス デバッグ マネージャー](../../extensibility/debugger/process-debug-manager.md) - PDM の機能の概要を示します。これは、デバッグ可能なプロセスのマネージャーです。

 [セッション デバッグ マネージャー](../../extensibility/debugger/session-debug-manager.md) - IDE にデバッグ セッションの統合ビューを提供する SDM を定義します。 SDM では、DE が管理されます。

 [デバッグ エンジン](../../extensibility/debugger/debug-engine.md) - DE によって提供されるデバッグ サービスについて説明します。

 [操作モード](../../extensibility/debugger/operational-modes.md) - IDE が動作する 3 つのモード (デザイン モード、実行モード、中断モード) の概要を示します。 また、移行メカニズムについても説明します。

 [式エバリュエーター](../../extensibility/debugger/expression-evaluator.md) - 実行時の EE の目的について説明します。

 [シンボル プロバイダー](../../extensibility/debugger/symbol-provider.md) - 実装時に、シンボル プロバイダーによって変数と式がどのように評価されるかについて説明します。

 [型ビジュアライザーとカスタム ビューアー](../../extensibility/debugger/type-visualizer-and-custom-viewer.md) - 型ビジュアライザーとカスタム ビューアーの概要、およびこれら両方をサポートする上での式エバリュエーターの役割について説明します。

## <a name="related-sections"></a>関連項目
 [デバッガーの概念](../../extensibility/debugger/debugger-concepts.md) 主要なデバッグ アーキテクチャの概念について説明します。

 [デバッガー コンテキスト](../../extensibility/debugger/debugger-contexts.md) コード、ドキュメント、式の評価コンテキスト内で DE がどのように同時操作されるかについて説明します。 場所、位置、それに関連する評価の 3 つのコンテキストそれぞれについて説明します。

 [タスクをデバッグする](../../extensibility/debugger/debugging-tasks.md) プログラムの起動や式の評価といった、さまざまなデバッグ タスクへのリンクが含まれています。

## <a name="see-also"></a>関連項目
- [開始するには](../../extensibility/debugger/getting-started-with-debugger-extensibility.md)
