---
title: Access データベース内のデータに接続する
description: Visual Studio で Access データベース (.mdb ファイルまたは .accdb ファイル) のデータに接続する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 07/18/2019
ms.topic: how-to
helpviewer_keywords:
- data [Visual Studio], connecting
- connecting to data, Access databases
- Access databases, connecting
ms.assetid: 4159e815-d430-4ad0-a234-e4125fcbef18
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
- data-storage
ms.openlocfilehash: eeaafdca1a3a4d6fb73ca275c4fc97ce67094d8e
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99867270"
---
# <a name="connect-to-data-in-an-access-database"></a>Access データベース内のデータに接続する

Visual Studio を使用して、Access データベース ( *.mdb* ファイルまたは *.accdb* ファイル) に接続できます。 接続を定義すると、**[データ ソース ウィンドウ]** にデータが表示されます。 そこから、テーブルまたはビューをデザイン サーフェイスにドラッグできます。

## <a name="prerequisites"></a>必須コンポーネント

これらの手順を使用するには、Windows フォームまたは WPF プロジェクトと、Access データベース ( *.accdb* ファイル) または Access 2000 - 2003 データベース ( *.mdb* ファイル) が必要です。 ファイルの種類に対応する手順に従ってください。

## <a name="create-a-dataset-for-an-accdb-file"></a>.accdb ファイルのデータセットを作成する

次の手順を使用して、Microsoft 365、Access 2013、Access 2010、または Access 2007 で作成されたデータベースに接続します。

1. Visual Studio で、Windows フォームまたは WPF アプリケーション プロジェクトを開きます。

2. **[データ ソース]** ウィンドウを開くには、 **[表示]** メニューで **[その他のウィンドウ]**  >  **[データ ソース]** の順に選択します。

   ![[表示]、[その他のウィンドウ]、[データ ソース]](../data-tools/media/viewdatasources.png)

3. **[データ ソース]** ウィンドウで、 **[新しいデータ ソースの追加]** をクリックします。

   **データ ソース構成ウィザード** が開きます。

4. **[データ ソースの種類の選択]** ページで、 **[データベース]** を選択し、 **[次へ]** を選択します。

5. **[データベース モデルの選択]** ページで、 **[データセット]** を選択し、 **[次へ]** を選択します。

6. **[データ接続の選択]** ページで、**[新しい接続]** を選択して新しいデータ接続を構成します。

   **[接続の追加]** ダイアログ ボックスが表示されます。

7. **[データ ソース]** が **[Microsoft Access データベース ファイル]** に設定されていない場合は、 **[変更]** ボタンを選択します。

   **[データ ソースの変更]** ダイアログ ボックスが開きます。 データ ソースの一覧で、 **[Microsoft Access データベース ファイル]** を選択します。 **[データ プロバイダー]** ドロップダウンで、 **[.NET Framework OLE DB 用データ プロバイダー]** を選択し、 **[OK]** を選択します。

8. **[データベース ファイル名]** の横の **[参照]** を選択し、 *.accdb* ファイルに移動して、 **[開く]** を選択します。

9. ユーザー名とパスワードを入力し (必要な場合)、 **[OK]** を選択します。

10. **[データ接続の選択]** ページで、 **[次へ]** を選択します。

    データ ファイルが現在のプロジェクトに含まれていないことを示すダイアログ ボックスが表示される場合があります。 **[はい]** または **[いいえ]** をクリックします。

11. **[アプリケーション構成ファイルに接続文字列を保存]** ページで、 **[次へ]** を選択します。

12. **[データベース オブジェクトの選択]** ページの **[テーブル]** ノードを展開します。

13. データセットに含めるテーブルまたはビューを選択し、 **[完了]** を選択します。

    プロジェクトにデータセットが追加され、テーブルとビューが **[データ ソース]** ウィンドウに表示されます。

## <a name="create-a-dataset-for-an-mdb-file"></a>.mdb ファイルのデータセットを作成する

次の手順を使用して、Access 2000 - 2003 で作成されたデータベースに接続します。

1. Visual Studio で、Windows フォームまたは WPF アプリケーション プロジェクトを開きます。

2. **[表示]** メニューで、 **[その他のウィンドウ]**  >  **[データ ソース]** の順に選択します。

   ![[表示]、[その他のウィンドウ]、[データ ソース]](../data-tools/media/viewdatasources.png)

3. **[データ ソース]** ウィンドウで、 **[新しいデータ ソースの追加]** をクリックします。

    **データ ソース構成ウィザード** が開きます。

4. **[データ ソースの種類の選択]** ページで、 **[データベース]** を選択し、 **[次へ]** を選択します。

5. **[データベース モデルの選択]** ページで、 **[データセット]** を選択し、 **[次へ]** を選択します。

6. **[データ接続の選択]** ページで、**[新しい接続]** を選択して新しいデータ接続を構成します。

7. データ ソースが **[Microsoft Access データベース ファイル (OLE DB)]** でない場合は、 **[変更]** を選択して **[データ ソースの変更]** ダイアログ ボックスを開き、 **[Microsoft Access データベース ファイル]** を選択して、 **[OK]** を選択します。

8. **[データベース ファイル名]** で、接続先となる *.mdb* ファイルのパスと名前を指定し、 **[OK]** を選択します。

   ![Access データベース ファイルへの接続を追加](../data-tools/media/add-connection-access-db.png)

9. **[データ接続の選択]** ページで、 **[次へ]** を選択します。

10. **[アプリケーション構成ファイルに接続文字列を保存]** ページで、 **[次へ]** を選択します。

11. **[データベース オブジェクトの選択]** ページの **[テーブル]** ノードを展開します。

12. データセットに必要なテーブルまたはビューを選択し、 **[完了]** を選択します。

    プロジェクトにデータセットが追加され、テーブルとビューが **[データ ソース]** ウィンドウに表示されます。

## <a name="next-steps"></a>次のステップ

作成したデータセットは、 **[データ ソース]** ウィンドウで使用できます。 これで、以下のタスクをどれでも実行できます。

- **[データ ソース]** ウィンドウで項目を選択し、フォームまたはデザイン サーフェイスにドラッグします (「[Visual Studio でのデータへの Windows フォーム コントロールのバインド](../data-tools/bind-windows-forms-controls-to-data-in-visual-studio.md)」または [WPF データ バインディングの概要](/dotnet/desktop-wpf/data/data-binding-overview)に関する記事を参照してください)。

- **データセット デザイナー** でデータ ソースを開き、データセットを構成しているオブジェクトを追加または編集します。

- データセット内のデータ テーブルの <xref:System.Data.DataTable.ColumnChanging> または <xref:System.Data.DataTable.RowChanging> イベントに検証ロジックを追加します (「[データセットのデータの検証](../data-tools/validate-data-in-datasets.md)」を参照してください)。

## <a name="see-also"></a>関連項目

- [接続を追加する](../data-tools/add-new-connections.md)
- [WPF データ バインディングの概要](/dotnet/framework/wpf/data/data-binding-overview)
- [Windows フォームでのデータ バインディング](/dotnet/framework/winforms/data-binding-and-windows-forms)
