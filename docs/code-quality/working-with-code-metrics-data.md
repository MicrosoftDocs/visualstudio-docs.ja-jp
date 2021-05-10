---
title: コード メトリック ウィンドウ
ms.date: 12/12/2017
description: Visual Studio のコード メトリック分析データを表示、フィルター処理、再配置、およびエクスポートする方法について説明します。 コード メトリックの結果に基づいて作業項目を作成する方法をご覧ください。
ms.custom: SEO-VS-2020
ms.topic: reference
f1_keywords:
- vs.codemetrics.output
helpviewer_keywords:
- code metrics results
- code metrics results window
- results window, code metrics
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: c02f5a3b5175be4517a51a6dc477d6e59b38a762
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99859568"
---
# <a name="use-the-code-metrics-results-window"></a>[コード メトリックの結果] ウィンドウを使用する

**[コード メトリックの結果]** ウィンドウには、コード メトリック分析によって生成されるデータが表示されます。 コード メトリックのデータ値の詳細については、「[コード メトリックの値](../code-quality/code-metrics-values.md)」を参照してください。

## <a name="display-code-metrics-results"></a>コード メトリックの結果を表示する

コード メトリックの結果を生成すると、 **[コード メトリックの結果]** ウィンドウが自動的に表示されます。 また、いつでも手動でウィンドウを表示することができます。

[コード メトリックの結果] ウィンドウは、次のいずれかのメニュー シーケンスを使用して表示できます。

- **[分析]** メニューの **[Windows** > **コード メトリックの結果]** を選択します。

- **[表示]** メニューの **[その他 Windows** > **コード メトリックの結果]** を選択します。

結果が含まれていない場合でも、 **[コード メトリックの結果]** ウィンドウが開きます。

### <a name="to-view-code-metrics-details"></a>コード メトリックの詳細を表示する方法

コード メトリックの結果が生成されている場合は、 **[階層]** 列のツリーを展開します。

## <a name="filter-code-metrics-results"></a>コード メトリックの結果をフィルター処理する

上部にあるツール バーを使用して、 **[コード メトリックの結果]** ウィンドウに表示される結果をフィルター処理できます。 たとえば、保守容易性指数が 65 未満の結果のみを表示することができます。

**[フィルター]** ドロップダウン ボックスには、結果列の名前が表示されます。 フィルターが定義されると、一覧の一番下にインデントと共に追加されます。 一覧には、定義された最後の 10 個のフィルターを含めることができます。

### <a name="to-filter-the-code-metrics-results"></a>コード メトリックの結果をフィルター処理する方法

1. **[フィルター]** リストから列名を選択します。

2. **[最小]** では、表示する最小値を入力します。

3. **[最大]** では、表示する最大値を入力します。

4. **[フィルターの適用]** ボタンをクリックします。

5. 結果の詳細を表示するには、階層ツリーを展開します。

## <a name="add-remove-and-rearrange-data-columns"></a>データ列の追加、削除、および再配置

**[コード メトリックの結果]** ウィンドウで結果列を追加または削除できます。 また、結果列を求める順序で表示されるように再配置することもできます。

### <a name="add-or-remove-a-column"></a>列を追加または削除する

1. **[列の追加または削除]** ボタンをクリックするか、任意の列見出しを右クリックして、 **[列の追加と削除]** をクリックします。

1. **[列の追加または削除]** ダイアログ ボックスで、追加または削除する列のチェック ボックスをオンまたはオフにし、 **[OK]** を選択します。

### <a name="rearrange-columns"></a>列を再配置する

1. **[列の追加または削除]** ボタンをクリックします。

1. **[列の追加または削除]** ダイアログ ボックスで、移動する列を選択し、上矢印または下矢印を選択します。

1. 列が必要な位置に配置されたら、 **[OK]** をクリックします。

## <a name="copy-data-to-the-clipboard-or-excel"></a>クリップボードまたは Excel にデータをコピーする

各データ列の名前と値の 1 行を含むテキスト文字列として、選択した行のコード メトリック データをクリップボードにコピーできます。 また、 **[Microsoft Excel 選択項目を開く]** をクリックして、すべてのコード メトリックの結果を Excel スプレッドシートにエクスポートすることもできます。

## <a name="create-a-work-item-based-on-code-metric-results"></a>コード メトリックの結果に基づいて作業項目を作成する

**[コード メトリックの結果]** ウィンドウの結果に基づいて、[Azure Boards](/azure/devops/boards/index?view=vsts&preserve-view=true) 作業項目を作成できます。 作業項目が作成されると、Visual Studio によって **[タイトル]** フィールドにタイトルと **[履歴]** タブにコード メトリック データが自動的に入力されます。

Azure Boards の作業項目の詳細については、[作業項目](/azure/devops/boards/work-items/index?view=vsts&preserve-view=true)に関するページを参照してください。

### <a name="to-create-a-work-item-based-on-a-result"></a>結果に基づいて作業項目を作成する方法

1. 結果を右クリックします。

2. **[作業項目の作成]** をポイントし、作成する作業項目の種類 (**バグ**、**タスク** など) をクリックします。

3. すべての必須フィールドに入力して、作業項目フォームを完成させます。

4. **[ファイル]** メニューの **[すべて保存]** をクリックして、作業項目を保存します。

### <a name="to-create-a-bug-based-on-a-result"></a>結果に基づいてバグを作成する方法

1. 結果をクリックして選択します。

2. **[作業項目の作成]** ボタンをクリックします。

3. すべての必須フィールドに入力して、作業項目フォームを完成させます。

4. **[ファイル]** メニューの **[すべて保存]** をクリックして、作業項目を保存します。

## <a name="see-also"></a>関連項目

- [コード メトリック値](../code-quality/code-metrics-values.md)
- [方法 : コード メトリック データを生成する](../code-quality/how-to-generate-code-metrics-data.md)
