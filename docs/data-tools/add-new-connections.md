---
title: 新しい接続を追加する
description: Visual Studio で DB またはサービスに接続を追加し、サーバー エクスプローラー、Cloud Explorer、または SQL Server オブジェクト エクスプローラーを使用して DB の内容とスキーマを探索します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
- data-storage
ms.openlocfilehash: ddcc5dd06a4e71d445c94c860b2a3ab92429ab2e
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99859386"
---
# <a name="add-new-connections"></a>新しい接続を追加する

データベースまたはサービスへの接続をテストし、**サーバー エクスプローラー**、**Cloud Explorer**、または **SQL Server オブジェクト エクスプローラー** を使用して、データベースの内容とスキーマを探索します。 これらのウィンドウの機能は、ある程度重複しています。 基本的な違いを次に示します。

- [サーバー エクスプローラー]

   Visual Studio にデフォルトでインストールされます。 これを使用すると、SQL Server データベース、ADO.NET プロバイダーがインストールされている他のデータベース、および一部の Azure サービスへの接続のテストと表示を行うことができます。 また、システム パフォーマンス カウンター、イベント ログ、メッセージ キューなどの下位レベルのオブジェクトも表示されます。 データ ソースに ADO.NET プロバイダーがない場合は、ここに表示されませんが、プログラムによって接続することで、Visual Studio から使用することができます。

- Cloud Explorer

   このウィンドウは、[Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.CloudExplorerForVS)から Visual Studio 拡張機能として手動でインストールします。 Azure サービスを探索して接続するための特別な機能を提供します。

- [SQL Server オブジェクト エクスプローラー]

   SQL Server Data Tools と共にインストールされ、 **[表示]** メニューに表示されます。 表示されない場合は、コントロールパネルの **プログラムと機能** に移動し、Visual Studio を探し、**変更** を選択して、SQL Server Data Tools のチェックボックスをオンにしてインストーラーを再実行します。 **[SQL Server オブジェクト エクスプローラー]** を使用すると、SQL データベース (ADO.NET プロバイダーがある場合) を表示したり、新しいデータベースを作成したり、スキーマを変更したり、ストアド プロシージャを作成したり、接続文字列を取得したり、データを表示したりすることができます。 ADO.NET プロバイダーがインストールされていない SQL データベースはここに表示されませんが、プログラムによってそれらに接続することはできます。

## <a name="add-a-connection-in-server-explorer"></a>サーバー エクスプローラーでの接続の追加

データベースへの接続を作成するには、 **[サーバー エクスプローラー]** の **[接続の追加]** アイコンをクリックするか、 **[データ接続]** ノードで **[サーバー エクスプローラー]** を右クリックして **[接続の追加]** を選択します。 ここでは、別のサーバー、SharePoint サービス、または Azure サービスのデータベースに接続することもできます。

![サーバー エクスプローラーの新しい接続アイコン](../data-tools/media/raddata-server-explorer-new-connection-icon.png)

**[接続の追加]** ダイアログ ボックスが表示されます。 ここでは、SQL Server LocalDB インスタンスの名前を入力しました。

![新しい接続を追加する](../data-tools/media/raddata-add-new-connection-dialog.png)

## <a name="change-the-provider"></a>プロバイダーの変更

データ ソースが不要な場合は、 **[変更]** ボタンをクリックして、新しいデータ ソースや新しい ADO.NET データ プロバイダーを選択します。 新しいプロバイダーは、構成方法に応じて、資格情報を要求する場合があります。

![ADO.NET データ プロバイダーの変更](../data-tools/media/raddata-change-ad0.net-data-provider.png)

## <a name="test-the-connection"></a>接続をテストする

データ ソースを選択し、 **[接続テスト]** をクリックします。 成功しない場合は、ベンダーのドキュメントに基づいてトラブルシューティングを行う必要があります。

![接続をテスト](../data-tools/media/raddata-test-connection.png)

テストが成功すると、*データ ソース* を作成する準備が整います。これは、基になるデータベースまたはサービスに基づく *データ モデル* を意味する Visual Studio の用語です。

## <a name="see-also"></a>関連項目

- [.NET 用の Visual Studio データ ツール](../data-tools/visual-studio-data-tools-for-dotnet.md)
