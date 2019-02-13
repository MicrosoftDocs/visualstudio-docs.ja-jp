---
title: 失敗したテストのロード テスト ログを保存する
ms.date: 10/19/2016
ms.topic: conceptual
helpviewer_keywords:
- load tests, scenarios
- load tests, logging
ms.assetid: 08a7fe98-a7f7-4b8d-94a3-ec82b65a2aaf
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: de19f24040d285392c2ed2a69776c8ecf39c9f36
ms.sourcegitcommit: 21d667104199c2493accec20c2388cf674b195c3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2019
ms.locfileid: "55910793"
---
# <a name="how-to-specify-if-test-failures-are-saved-to-test-logs-using-the-load-test-editor"></a>方法:ロード テスト エディターを使用してテスト ログにテストの失敗を記録するかどうかを指定する

**新しいロード テスト ウィザード**でロード テストを作成した後で、**ロード テスト エディター**を使用して、ロード テストのプロパティをテストのニーズおよび目標に合わせて変更できます。 「[チュートリアル:ロード テストの作成および実行](../test/walkthrough-create-and-run-a-load-test.md)」を参照してください。 **[テストの失敗時にログを保存]** プロパティを変更することにより、ロード テストでテストが失敗した場合にログを保存するかどうかを指定できます。

> [!NOTE]
> 実行設定の各プロパティとその説明の一覧については、「[ロード テストの実行設定のプロパティ](../test/load-test-run-settings-properties.md)」を参照してください。

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

## <a name="to-specify-if-the-test-log-is-saved-when-a-test-fails-in-a-scenario"></a>シナリオでテストが失敗した場合にテスト ログを保存するには

1.  ロード テストを開きます。

     **ロード テスト エディター**が表示されます。 ロード テスト ツリーが表示されます。

2.  ロード テスト ツリーの **[実行設定]** フォルダーで、テスト イテレーションの最大数を指定する実行設定ノードを選択します。

3.  **[表示]** メニューの **[プロパティ ウィンドウ]** をクリックします。

     **[プロパティ]** ウィンドウに、実行設定のカテゴリおよびプロパティが表示されます。

4.  **[テストの失敗時にログを保存]** プロパティで、**[True]** または **[False]** を選択して、シナリオでテストが失敗した場合にテスト ログを保存するかどうかを指定します。

     プロパティを変更したら、**[ファイル]** メニューの **[保存]** を選択します。

     ロード テスト アナライザーのテーブル ビューを使用すると、ログに保存したデータを表示できます。 詳細については、[テーブル ビューでのロード テスト結果とエラーの分析](../test/analyze-load-test-results-and-errors-in-the-tables-view.md)に関するページを参照してください。

## <a name="see-also"></a>関連項目

- [ロード テスト シナリオの編集](../test/edit-load-test-scenarios.md)
- [チュートリアル: ロード テストの作成および実行](../test/walkthrough-create-and-run-a-load-test.md)