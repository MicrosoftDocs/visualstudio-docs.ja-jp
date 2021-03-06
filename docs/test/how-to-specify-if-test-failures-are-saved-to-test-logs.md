---
title: 失敗したテストのロード テスト ログを保存する
description: '[テストの失敗時にログを保存] プロパティを変更することにより、ロード テストでテストが失敗した場合にテスト ログを保存するかどうかを指定する方法について説明します。'
ms.custom: SEO-VS-2020
ms.date: 10/19/2016
ms.topic: how-to
helpviewer_keywords:
- load tests, scenarios
- load tests, logging
ms.assetid: 08a7fe98-a7f7-4b8d-94a3-ec82b65a2aaf
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.openlocfilehash: 2f4c81a364bdbe12bb3f780fe17c077ab04a615b
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99889435"
---
# <a name="how-to-specify-if-test-failures-are-saved-to-test-logs-using-the-load-test-editor"></a>方法: ロード テスト エディターを使用してテスト ログにテストの失敗を記録するかどうかを指定する

**新しいロード テスト ウィザード** でロード テストを作成した後で、**ロード テスト エディター** を使用して、ロード テストのプロパティをテストのニーズおよび目標に合わせて変更できます。 「[Walkthrough: Create and Run a Load Test that contains Unit Tests](../test/walkthrough-create-and-run-a-load-test.md)」(チュートリアル: ロード テストの作成と実行) を参照してください。 **[テストの失敗時にログを保存]** プロパティを変更することにより、ロード テストでテストが失敗した場合にログを保存するかどうかを指定できます。

> [!NOTE]
> 実行設定の各プロパティとその説明の一覧については、「[ロード テストの実行設定のプロパティ](../test/load-test-run-settings-properties.md)」を参照してください。

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

## <a name="to-specify-if-the-test-log-is-saved-when-a-test-fails-in-a-scenario"></a>シナリオでテストが失敗した場合にテスト ログを保存するには

1. ロード テストを開きます。

     **ロード テスト エディター** が表示されます。 ロード テスト ツリーが表示されます。

2. ロード テスト ツリーの **[実行設定]** フォルダーで、テスト イテレーションの最大数を指定する実行設定ノードを選択します。

3. **[表示]** メニューの **[プロパティ ウィンドウ]** をクリックします。

     **[プロパティ]** ウィンドウに、実行設定のカテゴリおよびプロパティが表示されます。

4. **[テストの失敗時にログを保存]** プロパティで、 **[True]** または **[False]** を選択して、シナリオでテストが失敗した場合にテスト ログを保存するかどうかを指定します。

     プロパティを変更したら、 **[ファイル]** メニューの **[保存]** を選択します。

     ロード テスト アナライザーのテーブル ビューを使用すると、ログに保存したデータを表示できます。 詳細については、[テーブル ビューでのロード テスト結果とエラーの分析](../test/analyze-load-test-results-and-errors-in-the-tables-view.md)に関するページを参照してください。

## <a name="see-also"></a>参照

- [ロード テスト シナリオの編集](../test/edit-load-test-scenarios.md)
- [チュートリアル: ロード テストの作成および実行](../test/walkthrough-create-and-run-a-load-test.md)
