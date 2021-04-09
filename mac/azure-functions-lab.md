---
title: 'チュートリアル: Azure Functions'
description: Visual Studio for Mac での Azure Functions の使用に関する詳しいチュートリアル。
author: jmatthiesen
ms.author: jomatthi
ms.date: 11/06/2020
ms.technology: vs-ide-install
ms.assetid: 38FD2070-5151-482E-B0A9-993715128736
ms.topic: tutorial
ms.openlocfilehash: 3fa653a1acaae0f9b58d17f86d6e2e0feeb027a6
ms.sourcegitcommit: 2cf3a03044592367191b836b9d19028768141470
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/11/2020
ms.locfileid: "94493024"
---
# <a name="tutorial-getting-started-with-azure-functions"></a>チュートリアル: Azure Functions の概要

このラボでは、Visual Studio for Mac を使用して Azure Functions のビルドを開始する方法を学習します。 Azure Functions 開発者が使用できるバインドとトリガーの多くの種類の 1 つを表す、Azure ストレージ テーブルとの統合も行います。

## <a name="objectives"></a>目的

> [!div class="checklist"]
> * ローカルの Azure Functions を作成およびデバッグする
> * Web および Azure ストレージ リソースを統合する
> * 複数の Azure Functions に関連するワークフローを編成する

## <a name="requirements"></a>必要条件

- Visual Studio for Mac 7.5 以上。
- Azure サブスクリプション ([https://azure.com/free](https://azure.com/free?ref=visualstudio) から無料で入手可能)。

## <a name="exercise-1-creating-an-azure-functions-project"></a>演習 1:Azure Functions プロジェクトの作成

1. **Visual Studio for Mac** を起動します。

2. **[ファイル]、[新しいソリューション]** の順に選択します。

3. **[クラウド]、[全般]** カテゴリから、 **[Azure Functions]** テンプレートを選択します。 Azure Functions をホストする .NET クラス ライブラリを作成する場合は、C# を使用します。 **[次へ]** をクリックします。

    ![Azure Functions テンプレートの選択](media/azure-functions-lab-image1.png)

4. **[プロジェクト名]** を **"AzureFunctionsLab"** に設定して、 **[作成]** をクリックします。

    ![Azure Functions プロジェクトの名前付けと作成](media/azure-functions-lab-image2.png)

5. **[ソリューション] ウィンドウ** でノードを展開します。 既定のプロジェクト テンプレートには、さまざまな Azure WebJobs パッケージと、Newtonsoft.Json パッケージへの NuGet 参照が含まれています。

     次の 3 つのファイルもあります。- ホストのグローバル構成オプションを記述するための **host.json** - サービス設定を構成するための **local.settings.json**
        - プロジェクト テンプレートでは、既定の HttpTrigger も作成します。 このラボの目的上、プロジェクトから **HttpTrigger.cs** ファイルを削除する必要があります。

    **local.settings.json** を開きます。 既定では、2 つの空の接続文字列設定が示されます。

    ![local.settings.json ファイルが表示されている [ソリューション] ウィンドウ](media/azure-functions-lab-image3.png)

## <a name="exercise-2-creating-an-azure-storage-account"></a>演習 2:Azure ストレージ アカウントの作成

1. [https://portal.azure.com](https://portal.azure.com) で Azure アカウントにログオンします。

1. **[お気に入り]** セクションで、画面の左側にある **[ストレージ アカウント]** を選択します。

    ![ストレージ アカウント項目が表示されている、Azure Portal の [お気に入り] セクション](media/azure-functions-lab-image4.png)

1. 次のように、 **[追加]** を選択して新しいストレージ アカウントを作成します。

    ![新しいストレージ アカウントを追加するためのボタン](media/azure-functions-lab-image5.png)

1. **[名前]** にグローバルに一意の名前を入力し、それを **[リソース グループ]** で再利用します。 その他のすべての項目は既定値のままでかまいません。

    ![新しいストレージ アカウントの詳細](media/azure-functions-lab-image6.png)

1. **[作成]** をクリックします。 ストレージ アカウントの作成には数分かかる場合があります。 正常に作成された場合は、通知が表示されます。

    ![展開が成功したことを示す通知](media/azure-functions-lab-image7.png)

1. 通知の **[リソースに移動]** ボタンを選択します。

1. **[アクセス キー]** タブを選択します。

    ![アクセス キーの設定](media/azure-functions-lab-image8.png)

1. 最初の **[接続文字列]** をコピーします。 この文字列は、後で Azure Storage と Azure Functions を統合する際に使用されます。

    ![キー 1 の情報](media/azure-functions-lab-image9.png)

1. **Visual Studio for Mac** に戻り、**local.settings.json** で **AzureWebJobsStorage** 設定として完全な接続文字列を貼り付けます。 これで、リソースへのアクセスを必要とする、関数の属性の設定名を参照することができます。

    ![接続キーが入力されたローカル設定ファイル](media/azure-functions-lab-image10.png)

## <a name="example-3-creating-and-debugging-an-azure-function"></a>例 3:Azure Function の作成とデバッグ

1. これで、一部のコードの追加を開始する準備ができました。 .NET クラス ライブラリで作業を行う場合は、Azure Functions が静的メソッドとして追加されます。 **[ソリューション] ウィンドウ** で、 **[AzureFunctions]** プロジェクト ノードを右クリックし、 **[追加]、[関数の追加]** の順に選択します。

    ![[関数の追加] オプション](media/azure-functions-lab-image11.png)

1. [新しい Azure Functions] ダイアログで、Generic Webhook テンプレートを選択します。 次のように、**名前** を **Add** に設定し、 **[OK]** をクリックして関数を作成します。

    ![[新しい Azure Functions] ダイアログ](media/azure-functions-lab-image12.png)

1. 新しいファイルの先頭に、以下の **using** ディレクティブを追加します。

    ```csharp
    using Microsoft.Azure.WebJobs.Extensions.Http;
    using System.Web;
    using Microsoft.WindowsAzure.Storage.Table;
    ```

1. 既存の `Run` メソッドを削除し、Azure Function としてクラスに以下のメソッドを追加します。

    ```csharp
    [FunctionName("Add")]
    public static int Run(
    [HttpTrigger(AuthorizationLevel.Function, "get", Route = null)]
    HttpRequestMessage req,
    TraceWriter log)
    {
        int x = 1;
        int y = 2;

        return x + y;
    }
    ```

1. ここで、メソッドの定義を 1 つずつ説明していきます。

    最初に表示されるのは **FunctionName** 属性で、このメソッドを Azure Function としてマークします。 この属性は関数のパブリック名を指定します。 属性名が、実際のメソッド名と一致する必要はありません。

    ![FunctionName 属性が強調表示されている新しい run メソッド](media/azure-functions-lab-image13.png)

1. 次に、メソッドは、必須である **public static** メソッドとしてマークされます。 また、戻り値が **int** であることがわかります。メソッド属性を使用して特に指定されていない限り、Azure Function の非 void 戻り値はテキストとしてクライアントに返されます。 既定では、**XML** として返されますが、**JSON** に変更することができます。この操作は、ラボで後から行います。

    ![メソッドの初期化が強調表示されている新しい run メソッド](media/azure-functions-lab-image14.png)

1. 最初のパラメーターは **HttpTrigger** 属性でマークされています。これは、このメソッドが HTTP 要求で呼び出されることを示します。 この属性はメソッドの承認レベルと、サポートされる動詞 (ここでは **"GET"** のみ) も指定します。 必要に応じて、**Route** を定義することもできます。これにより、メソッドへのパスがオーバーライドされ、パスから自動的に変数を抽出する手段が提供されます。 ここでは **Route** が null であるため、このメソッドへのパスは既定で **/api/Add** になります。

    ![パラメーターが強調表示されている新しい run メソッド](media/azure-functions-lab-image15.png)

1. メソッドに対する最後のパラメーターは **TraceWriter** で、これを使用して診断とエラーのメッセージをログに記録できます。

    ![TraceWriter が強調表示されている新しい run メソッド](media/azure-functions-lab-image16.png)

1. 行の余白をクリックして、メソッドの **return** 行にブレークポイントを設定します。

    ![return 行に設定されたブレークポイント](media/azure-functions-lab-image17.png)

1. **F5** キーを押すか、 **[実行]、[デバッグの開始]** の順に選択して、デバッグ セッションでプロジェクトをビルドして実行します。 **[実行]** ボタンをクリックすることもできます。 これらのオプションではすべて同じタスクが実行されます。 このラボの残りの部分では **F5** キーを押しますが、一番使いやすい方法を使用できます。

    ![プロジェクトをビルドして実行する](media/azure-functions-lab-image18.png)

1. プロジェクトを実行すると、ターミナルアプリケーションが自動的に開きます。

1. このプロジェクトでは、メソッドの属性と、この記事の後半で説明するファイル規則に基づいて、Azure Functions の検出プロセスを実行します。 この場合、単一の Azure Function が検出され、1 つのジョブ関数が "生成" されます。

    ![ターミナルでの Azure Function の出力](media/azure-functions-lab-image19.png)

1. Azure Functions ホストは、スタートアップ メッセージの一番下に HTTP トリガー API の URL を出力します。 これは 1 つだけである必要があります。 その URL をコピーし、新しいブラウザー タブで貼り付けます。

    ![Azure Function API の URL](media/azure-functions-lab-image20.png)

1. ブレークポイントはすぐにトリガーされます。 Web 要求が関数にルーティングされ、デバッグできるようになりました。 **x** 変数にポインタを合わせると、その値が表示されます。

    ![トリガーされたブレークポイント](media/azure-functions-lab-image21.png)

1. 以前に追加するために使用したのと同じ方法を使って、ブレークポイントを削除します (余白をクリックするか、行を選択して **F9** キーを押す)。

1. **F5** キーを押して実行を続行します。

1. ブラウザーで、メソッドの XML 結果がレンダリングされます。 期待どおりに、ハードコーディングされた加算演算で妥当な合計が生成されます。 Safari で "3" のみが表示されている場合は、**Safari、[環境設定]、[詳細]** の順に移動し、 **[メニュー バーに開発メニューを表示]** チェック ボックスをオンにしてページを再度読み込みます。

1. **Visual Studio for Mac** で、 **[停止]** ボタンをクリックしてデバッグ セッションを終了します。 新しい変更が確実に選択されるように、必ずデバッグ セッションを再開 (停止してから実行) してください。

    ![デバッグの停止オプション](media/azure-functions-lab-image22.png)

1. **Run** メソッドで、**x** と **y** の定義を次のコードに置き換えます。 このコードは URL のクエリ文字列から値を抽出し、指定されたパラメーターに基づいて、加算演算を動的に実行できるようにします。

    ```csharp
    var query = HttpUtility.ParseQueryString(req.RequestUri.Query);

    int x = int.Parse(query["x"]);

    int y = int.Parse(query["y"]);

    return x + y;
    ```

1. アプリケーションを実行します。

1. ブラウザー ウィンドウに戻り、文字列 `/?x=2&y=3` を URL に追加します。 これで URL 全体は `http://localhost:7071/api/Add?x=2&y=3` になるはずです。 新しい URL に移動します。

1. この時点で、結果に新しいパラメーターが反映されるはずです。 プロジェクトを異なる値で自由に実行してください。 エラー チェックが行われていないため、パラメーターが無効であるか欠落している場合、エラーがスローされることに注意してください。

1. デバッグ セッションを停止します。

## <a name="exercise-4-working-with-functionjson"></a>演習 4:function.json の操作

1. 前の演習では、ライブラリに定義されている Azure Function のジョブ関数が Visual Studio for Mac で生成されたことを示しました。 これは、Azure Functions で実際に実行時にメソッド属性が使用されるのではなく、コンパイル時のファイル システム規則を使用して、Azure Functions を利用可能にする場所と方法を構成するためです。 **[ソリューション] ウィンドウ** で、プロジェクト ノードを右クリックし、 **[Finder で表示]** を選択します。

     ![[Finder で表示] メニュー オプション](media/azure-functions-lab-image23.png)

1. **bin/Debug/netstandard2.0** に到達するまで、ファイル システムを下に移動します。 **Add** という名前のフォルダーがあるはずです。 このフォルダーは、C# コードの関数名属性に対応するように作成されています。 Add フォルダーを展開して、単一の **function.json** ファイルを表示します。 このファイルは、Azure Function のホストと管理のためにランタイムによって使用されます。 コンパイル時サポートのないその他の言語モデル (C# スクリプトや JavaScript など) の場合は、これらのフォルダーを手動で作成して管理する必要があります。 C# 開発者向けには、ビルド時に属性メタデータから自動的に生成されます。 **function.json** を右クリックして選択し、Visual Studio で開きます。

    ![ファイル ディレクトリの function.json](media/azure-functions-lab-image24.png)

1. このチュートリアルの前の手順を実行している場合は、C# 属性の基本的な知識があるはずです。 それを考えれば、この JSON は見慣れたものです。 ただし、前の演習では説明されていない項目がいくつかあります。 たとえば、**binding** にはそれぞれ **direction** が設定されている必要があります。 お察しのとおり、 **"in"** はパラメーターが入力されていることを意味し、 **"out"** はパラメーターが戻り値 ( **$return** 経由)、またはメソッドに対する **out** パラメーターであることを示します。 アセンブリ内には、**scriptFile** (この最終的な場所に対して相対的) および **entryPoint** メソッド (パブリックまたは静的) を指定する必要もあります。 次のいくつかの手順では、このモデルを使用してカスタム関数パスを追加するため、このファイルの内容をクリップボードにコピーします。

    ![Visual Studio for Mac で開かれた function.json ファイル](media/azure-functions-lab-image25.png)

1. **[ソリューション] ウィンドウ** で、 **[AzureFunctionsLab]** プロジェクト ノードを右クリックし、 **[追加]** 、[新しいフォルダー] の順に選択します。 新しいフォルダーに **Adder** という名前を付けます。 既定の規則では、このフォルダーの名前で、**api/Adder** などの API へのパスが定義されます。

    ![[新しいフォルダー] オプション](media/azure-functions-lab-image26.png)

1. **Adder** フォルダーを右クリックし、 **[追加]、[新しいファイル]** の順に選択します。

    ![[新しいファイル] オプション](media/azure-functions-lab-image27.png)

1. **[Web]** カテゴリ、 **[空の JSON ファイル]** テンプレートの順に選択します。 **[名前]** を **function** に設定して、 **[新規]** をクリックします。

    ![[空の JSON ファイル] オプション](media/azure-functions-lab-image28.png)

1. (手順 3 の) その他の **function.json** の内容を、新しく作成されたファイルの既定の内容に貼り付けて置き換えます。

1. json ファイルの先頭から、次の行を削除します。

    ```json
    "configurationSource":"attributes",
    "generatedBy":"Microsoft.NET.Sdk.Functions-1.0.13",
    ```

1. 最初のバインドの末尾 ( **"name": "req"** 行の後) に、以下のプロパティを追加します。 前の行には必ずコンマを含めてください。 このプロパティによって既定のルートがオーバーライドされ、パスから **int** パラメーターが抽出され、**x** および **y** という名前のメソッド パラメーターに配置されるようになります。

    ```json
    "direction": "in",
    "route": "Adder/{x:int?}/{y:int?}"
    ```

1. 最初のバインドの下に別のバインドを追加します。 このバインドは関数の戻り値を処理します。 前の行には必ずコンマを含めてください。

    ```json
    {
    "name": "$return",
    "type": "http",
    "direction": "out"
    }
    ```

1. また、以下に示すように、 **"Add2"** というメソッドを使用するように、ファイルの末尾の **entryPoint** プロパティを更新します。 これは、**api/Adder...** というパスが、任意の名前 (ここでは **Add2**) を持つ適切なメソッドにマップできたことを示すためのもです。

    ```json
    "entryPoint": "<project-name>.<function-class-name>.Add2"
    ```

1. 最終的な **function.json** ファイルは、次の json のようになります。

    ```json
    {
    "bindings": [
        {
        "type": "httpTrigger",
        "methods": [
            "get"
        ],
        "authLevel": "function",
        "direction": "in",
        "name": "req",
        "route": "Adder/{x:int?}/{y:int?}"
        },
        {
        "name": "$return",
        "type": "http",
        "direction": "out"
        }
    ],
    "disabled": false,
    "scriptFile": "../bin/AzureFunctionsProject.dll",
    "entryPoint": "AzureFunctionsProject.Add.Add2"
    }
    ```

1. このすべての作業を完了するために必要な最後の 1 つの手順は、このファイルを、変更のたびに出力ディレクトリの同じ相対パスにコピーするよう Visual Studio for Mac に指示することです。 ファイルを選択した状態で、右側のバーから [プロパティ] タブを選び、 **[出力ディレクトリにコピー]** で **[新しい場合はコピーする]** を選択します。

    ![json ファイルの [プロパティ] オプション](media/azure-functions-lab-image30.png)

1. 予期される関数を実行するために、**Add.cs** で `Run` メソッド (属性を含む) を次のメソッドに置き換えます。 属性が使用されないことと、**x** と **y** の明示的なパラメーターを持つことを除けば、`Run` と非常に似ています。

    ```csharp
    public static int Add2(
        HttpRequestMessage req,
        int x,
        int y,
        TraceWriter log)
    {
        return x + y;
    }
    ```

1. **F5** キーを押し、プロジェクトをビルドして実行します。

1. ビルドが完了し、プラットフォームがスピンアップすると、新しく追加されたメソッドにマップされる要求に対して使用可能な 2 番目のルートがあることが示されます。

    ![http 関数の URL](media/azure-functions-lab-image31.png)

1. ブラウザー ウィンドウに戻り、 **http://localhost:7071/api/Adder/3/5** に移動します。

1. この時点でメソッドが再び動作し、パスからパラメーターがプルされ、合計が生成されます。

1. **Visual Studio for Mac** に戻り、デバッグ セッションを終了します。

## <a name="exercise-5-working-with-azure-storage-tables"></a>演習 5:Azure ストレージ テーブルの操作

多くの場合、ビルドするサービスは、これまでビルドしたものよりはるかに複雑で、実行にはかなりの時間またはインフラストラクチャが必要になることがあります。 その場合、リソースが利用可能になったときに処理のためキューに入れられた要求を受け入れることが効果的な場合があります。これは Azure Functions でサポートされています。 それ以外の場合は、一元的にデータを格納します。 Azure Storage のテーブルで、この操作をすばやく行うことができます。

1. 以下のクラスを **Add.cs** に追加します。 これは名前空間の中に記述すべきですが、ここでは既存のクラスの外に記述します。

    ```csharp
    public class TableRow : TableEntity
    {
        public int X { get; set; }
        public int Y { get; set; }
        public int Sum { get; set; }
    }
    ```

1. **Add** クラス内で、次のコードを追加して別の関数を導入します。 これは HTTP 応答を伴わないという点で、これまでとは異なることに注意してください。 最終行は、パラメーターと合計だけでなく、後で簡単に取得できるようにする一部のキー情報 (**PartitionKey** と **RowKey**) が入力された新しい **TableRow** を返します。 また、メソッド内のコードでは、関数がいつ実行されるかをより簡単に把握できるように **TraceWriter** が使用されます。

    ```csharp
    [FunctionName("Process")]
    [return: Table("Results")]
    public static TableRow Process(
        [HttpTrigger(AuthorizationLevel.Function, "get",
            Route = "Process/{x:int}/{y:int}")]
        HttpRequestMessage req,
        int x,
        int y,
        TraceWriter log)
    {
        log.Info($"Processing {x} + {y}");

        return new TableRow()
        {
            PartitionKey = "sums",
            RowKey = $"{x}_{y}",
            X = x,
            Y = y,
            Sum = x + y
        };
    }
    ```

1. **F5** キーを押し、プロジェクトをビルドして実行します。

1. ブラウザー タブで、 **http://localhost:7071/api/Process/4/6** に移動します。 これにより別のメッセージがキューに入れられ、最終的には別の行がテーブルに追加されます。

1. **ターミナル** に戻り、**4 + 6** の受信要求を監視します。

    ![追加要求を示すターミナル出力](media/azure-functions-lab-image32.png)

1. ブラウザーに戻り、同じ URL への要求を更新します。 この時点で、**Process** メソッドの後にエラーが表示されます。 これは、コードが、既に存在するパーティションと行キーの組み合わせを使用して、Azure Table Storage テーブルに行を追加しようとしているためです。

    ```
    System.Private.CoreLib: Exception while executing function: Process. Microsoft.Azure.WebJobs.Host: Error while handling parameter $return after function returned:. Microsoft.Azure.WebJobs.Host: The specified entity already exists.
    ```

1. デバッグ セッションを終了します。

1. エラーを軽減するには、**TraceWriter** パラメーターの直前のメソッド定義に次のパラメーターを追加します。 このパラメーターは、結果を格納するために使用していた **PartitionKey** の **Results** テーブルから **TableRow** の取得を試みるよう Azure Functions プラットフォームに指示します。 ただし、本当の魔法のいくつかは、まったく同じメソッドの他の **x** および **y** パラメーターに基づいて **RowKey** が動的に生成されていることに気付いたときに起こります。 その行が既に存在する場合、開発者に必要な追加作業が行われずにメソッドが開始されたときに、**tableRow** に含まれます。 行が存在しない場合は、null だけとなります。 このような効率性により、開発者はインフラストラクチャではなく、重要なビジネス ロジックに集中することができます。

    ```csharp
    [Table("Results", "sums", "{x}_{y}")]
    TableRow tableRow,
    ```

1. メソッドの先頭に次のコードを追加します。 **tableRow** が null でない場合、演算結果は既に要求されており、すぐに返すことができます。 それ以外の場合、関数は以前のとおりに続行します。 これはデータを返す最も堅牢な方法でないかもしれませんが、わずかなコードで複数のスケーラブル層にわたる非常に洗練された演算を編成できることを示しています。

    ```csharp
    if (tableRow != null)
    {
        log.Info($"{x} + {y} already exists");
        return null;
    }
    ```

1. **F5** キーを押し、プロジェクトをビルドして実行します。

1. ブラウザー タブで、 **http://localhost:7071/api/Process/4/6** の URL を更新します。 このレコードのテーブル行は存在するため、エラーなしですぐに返されます。 HTTP 出力はないため、ターミナルで出力を確認できます。

    ![テーブル行が既に存在することを示すターミナル出力](media/azure-functions-lab-image33.png)

1. URL を更新し、 **http://localhost:7071/api/Process/5/7** など、まだテストされていない組み合わせを反映させます。 テーブル行が (予期したとおりに) 見つからなかったことを示す、ターミナルのメッセージに注意してください。

    ![新しいプロセスを示すターミナル出力](media/azure-functions-lab-image34.png)

1. **Visual Studio for Mac** に戻り、デバッグ セッションを終了します。

<!--
1. Finally, let's take a look at what it's like to work with multiple input records. Rather than specify a specific **TableRow**, you can request an **IQueryable<TableRow>** using the same attributes, and the runtime will fill it with the appropriate resource you need. Add the code below to create a **List** function that lists all items that currently exist in the Azure table we've been working with. Also note that we're specifying that the MIME type of the response is **application/json**, so the runtime will automatically render as JSON.

    ```csharp
    [FunctionName("List")]
    public static HttpResponseMessage List(
        [HttpTrigger(AuthorizationLevel.Function, "get", Route = null)]
        HttpRequestMessage req,
        [Table("Results", "sums")]
        IQueryable<TableRow> table,
        TraceWriter log)
    {
        return req.CreateResponse(HttpStatusCode.OK, table, "application/json");
    }
    ```
1. Press **F5** to build and run the project.

1. In the browser tab, navigate to **http://localhost:7071/api/List**. This should pull down the list of all items in the Azure table and render it as JSON.

    ![](https://user-images.githubusercontent.com/3944468/29033725-be9d5a5e-7b4a-11e7-8b55-df0a200b6320.png)
-->

## <a name="summary"></a>まとめ

このラボでは、Visual Studio for Mac で Azure Functions のビルドを開始する方法を学習しました。
