---
title: コマンド ラインから Visual Studio ロード テストの実行設定を指定する
ms.date: 10/19/2016
ms.topic: conceptual
helpviewer_keywords:
- load tests, command line
- load tests, run settings, selecting
ms.assetid: 175d1d58-f09a-4449-b132-a29a394a7c8e
author: gewarren
ms.author: gewarren
manager: douge
ms.prod: visual-studio-dev15
ms.technology: vs-ide-test
ms.openlocfilehash: 40186bde515c95638ae0bdd90b9cace92b8da4a5
ms.sourcegitcommit: e13e61ddea6032a8282abe16131d9e136a927984
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2018
ms.locfileid: "31965389"
---
# <a name="how-to-select-a-load-test-run-setting-to-use-from-the-command-line"></a>方法: コマンド ラインから使用するロード テストの実行設定を選択する

ロード テストには、1 つ以上の*実行設定* を含めることができます。実行設定は、ロード テストの実行方法に影響を与えるプロパティのセットです。 実行設定は、[プロパティ] ウィンドウでカテゴリ別に整理されています。 ロード テストの実行時には、現在アクティブとして設定されている実行設定が使用されます。

 ロード テストに実行設定が 1 つだけ含まれる場合は、その実行設定は常にアクティブ ノードになります。 ロード テストに複数の実行設定ノードが含まれている場合は、コマンド ラインからロード テストを実行する際に使用するノードを 1 つ選択します。 「[方法: ロード テストに追加の実行設定を追加する](../test/how-to-add-additional-run-settings-to-a-load-test.md)」を参照してください。

## <a name="to-change-the-run-setting-from-the-command-line"></a>実行設定をコマンド ラインから変更するには

1.  コンテキスト パラメーターの手法を活用するためにコマンド ラインから別の実行設定を使用する場合は、次のコマンドを使用します。

    `Set Test.UseRunSetting= CorporateStagingWebServer`

2.  mstest を使用してロード テストを実行します。

    `mstest /testcontainer:loadtest1.loadtest`

## <a name="see-also"></a>関連項目

- [ロード テストの実行設定の構成](../test/configure-load-test-run-settings.md)
- [ロード テストでのコンピューターのカウンター セットとしきい値規則の指定](../test/specify-counter-sets-and-threshold-rules-for-load-testing.md)
- [方法: ロード テストに追加の実行設定を追加する](../test/how-to-add-additional-run-settings-to-a-load-test.md)
- [方法: ロード テストのアクティブな実行設定を選択する](../test/how-to-select-the-active-run-setting-for-a-load-test.md)