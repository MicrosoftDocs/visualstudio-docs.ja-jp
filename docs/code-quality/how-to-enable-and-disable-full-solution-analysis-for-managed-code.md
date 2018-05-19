---
title: '方法: マネージ コードの完全ソリューション分析を有効または無効にします'
ms.date: 03/23/2018
ms.topic: conceptual
helpviewer_keywords:
- full solution analysis
author: gewarren
ms.author: gewarren
manager: douge
ms.prod: visual-studio-dev15
ms.technology: vs-ide-code-analysis
ms.workload:
- dotnet
ms.openlocfilehash: d227360be39455662d3d2ebe822810debd655dac
ms.sourcegitcommit: e13e61ddea6032a8282abe16131d9e136a927984
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2018
---
# <a name="how-to-enable-and-disable-full-solution-analysis-for-managed-code"></a>方法: マネージ コードの完全ソリューション分析を有効または無効にします

*完全ソリューション分析*は、Visual Studio の機能の 1 つで、ソリューション内で開いている Visual C# または Visual Basic ファイルのみのコード分析の問題を見ることができるようになります。また閉じられたファイルのコードでも有効です。既定では、完全ソリューション解析は Visual basic で *有効* で、Visual C# では *無効* になっています。

すべてのファイルのすべての問題を表示できるのは便利なことでもありますが、場合によっては無駄にもなります。 Visual Studio ソリューションが非常に大きくまたは多くのファイルが含まれる場合、この機能は Visual Studio を遅くさせます。 表示する問題の数を制限して、Visual Studio のパフォーマンスを向上させるために、完全なソリューション分析を無効にすることもできます。 必要に応じて、この機能を簡単に再有効化することができます。

## <a name="to-toggle-full-solution-analysis"></a>完全なソリューション分析を切り替える

1. 開くには、**オプション**ダイアログ ボックスで、Visual Studio のメニュー バーで選択**ツール** > **オプション**です。

1. **オプション** ダイアログ ボックスで、選択**テキスト エディター** > **c#** または**基本** >  **高度な**します。

1. 選択、**完全ソリューション解析を有効にする**完全なソリューション分析を有効または無効にするボックスをオフにする チェック ボックスです。 選択**OK**終了するとします。

    ![完全なソリューション分析 チェック ボックスを有効にします。](../code-quality/media/options-enable-full-solution-analysis.png)

## <a name="results-of-enabling-and-disabling-full-solution-analysis"></a>結果を有効にして、完全なソリューション分析を無効にします。

次のスクリーン ショットでは、完全なソリューション分析を有効にすると、結果を確認できます。 すべてのエラーとコード分析の問題で*すべて*ソリューション内のファイルの表示、かどうか、ファイルが開いているかに関係なく。

![完全ソリューション解析を有効にします。](../code-quality/media/fsa_enabled.png)

次のスクリーン ショットは、完全なソリューション分析を無効にした後、同じソリューションからの結果を示します。 エラーと開いているソリューション ファイルでコード分析の問題のみに表示されます、**エラー一覧**です。

![完全ソリューション解析を無効になっています。](../code-quality/media/fsa_disabled.png)

## <a name="automatically-disable-full-solution-analysis"></a>完全なソリューション分析を自動的に無効にします。

Visual Studio を検出する場合は、200 MB または少ないシステム メモリに使用できる場合に自動的に無効に完全なソリューション分析 (およびその他のいくつかの機能) が有効な場合です。 このような場合は、Visual Studio が一部の機能を無効になっていることを通知するアラートが表示されます。 ボタンを使用する場合は、完全なソリューション分析を再度有効にすることができます。

![完全ソリューション解析を中断する警告テキスト](../code-quality/media/fsa_alert.png)
