---
title: Windows フォームで簡単な WCF サービスを作成する
description: このチュートリアルでは、Visual Studio で Windows Communication Foundation (WCF) サービスを作成し、テストしてから、Windows フォーム アプリケーションからアクセスします。
ms.date: 11/04/2016
ms.custom: SEO-VS-2020
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- WCF, walkthrough [Visual Studio]
- WCF, Visual Studio tools for
- WCF services
- WCF services, walkthrough
ms.assetid: 5fef1a64-27a4-4f10-aa57-29023e28a2d6
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
- data-storage
ms.openlocfilehash: 5352ad4724e7c54e72dbaa52573c814657fa041e
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/02/2021
ms.locfileid: "106216099"
---
# <a name="walkthrough-create-a-simple-wcf-service-in-windows-forms"></a>チュートリアル: Windows フォームでの簡単な WCF サービスの作成

このチュートリアルでは、簡単な Windows Communication Foundation (WCF) サービスを作成し、テストして、Windows フォーム アプリケーションからアクセスする方法を例示しています。

[!INCLUDE[note_settings_general](../data-tools/includes/note_settings_general_md.md)]

## <a name="create-a-service"></a>サービスの作成

1. Visual Studio を開きます。

::: moniker range="vs-2017"

2. **[ファイル]** メニューで、 **[新規]** > **[プロジェクト]** を選択します。

3. **[新しいプロジェクト]** ダイアログ ボックスで、 **[Visual Basic]** または **[Visual C#]** ノードを展開し、 **[WCF]** を選択してから **[WCF サービス ライブラリ]** を選択します。

4. **[OK]** をクリックしてプロジェクトを作成します。

   ![WCF サービス ライブラリ プロジェクト](../data-tools/media/wcf1.png)

::: moniker-end

::: moniker range=">=vs-2019"

2. スタート ウィンドウで、 **[新しいプロジェクトの作成]** を選択します。

3. **[新しいプロジェクトの作成]** ページの [検索] ボックスに「**WCF サービス ライブラリ**」と入力します。 **[WCF サービス ライブラリ]** の C# または Visual Basic テンプレートを選択し、 **[次へ]** をクリックします。

   ![Visual Studio 2019 で新しい WCF サービス ライブラリ プロジェクトを作成する](media/vs-2019/create-new-wcf-service-library.png)

   > [!TIP]
   > テンプレートが表示されない場合は、Visual Studio の **Windows Communication Foundation** コンポーネントをインストールすることが必要な場合があります。 **[さらにツールと機能をインストールする]** を選択して Visual Studio インストーラーを開きます。 **[個々のコンポーネント]** タブを選択し、 **[開発作業]** まで下にスクロールして、 **[Windows Communication Foundation]** を選択します。 **[変更]** をクリックします。

4. **[新しいプロジェクトの構成]** ページで、 **[作成]** をクリックします。

::: moniker-end

   > [!NOTE]
   > これにより、テストしてアクセスすることが可能な機能するサービスが作成されます。 次の 2 つの手順は、別のデータ型を使用するように既定の方法を変更する方法を示しています。 実際のアプリケーションで、独自の関数をサービスに追加することもできます。

5. **ソリューション エクスプローラー** で、**IService1.vb** または **IService1.cs** をダブルクリックします。

   ![IService1 ファイル](../data-tools/media/wcf2.png)

   次の行を見つけます。

   :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/wcfwalkthrough/cs/iservice1_2.cs" id="Snippet4":::
   :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/wcfwalkthrough/vb/iservice1_2.vb" id="Snippet4":::

   `value` パラメーターの型を文字列に変更します。

   :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/wcfwalkthrough/cs/iservice1.cs" id="Snippet1":::
   :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/wcfwalkthrough/vb/iservice1.vb" id="Snippet1":::

   上記のコードで、`<OperationContract()>` または `[OperationContract]` 属性に注意してください。 これらの属性は、サービスによって公開されている任意のメソッドに必要です。

6. **ソリューション エクスプローラー** で、**Service1.vb** または **Service1.cs** をダブルクリックします。

   ![Service1 ファイル](../data-tools/media/wcf3.png)

   次の行を見つけます。

   :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/wcfwalkthrough/vb/service1_2.vb" id="Snippet5":::
   :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/wcfwalkthrough/cs/service1_2.cs" id="Snippet5":::

   `value` パラメーターの型を文字列に変更します。

   :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/wcfwalkthrough/cs/service1.cs" id="Snippet2":::
   :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/wcfwalkthrough/vb/service1.vb" id="Snippet2":::

## <a name="test-the-service"></a>サービスをテストする

1. **F5** キーを押してサービスを実行します。 **[WCF のテスト用クライアント]** フォームが表示され、サービスが読み込まれます。

2. **[WCF のテスト用クライアント]** フォームで、**IService1** の下の **GetData()** メソッドをダブルクリックします。 **[GetData]** タブが表示されます。

     ![GetData&#40;&#41; メソッド](../data-tools/media/wcf4.png)

3. **[要求]** ボックスで、**[値]** フィールドを選択して「`Hello`」と入力します。

     ![[値] フィールド](../data-tools/media/wcf5.png)

4. **[起動]** ボタンをクリックします。 **[セキュリティ警告]** ダイアログ ボックスが表示されたら、 **[OK]** をクリックします。 結果は **[応答]** ボックスに表示されます。

     ![[応答] ボックスに結果が表示される](../data-tools/media/wcf6.png)

5. **[ファイル]** メニューの **[終了]** をクリックして、テスト フォームを閉じます。

## <a name="access-the-service"></a>サービスにアクセスする

### <a name="reference-the-wcf-service"></a>WCF サービスを参照する

1. **[ファイル]** メニューの **[追加]** をポイントし、 **[新しいプロジェクト]** をクリックします。

2. **[新しいプロジェクト]** ダイアログ ボックスで、 **[Visual Basic]** ノードまたは **[Visual C#]** ノードを展開し、 **[Windows]** を選択して **[Windows フォーム アプリケーション]** を選択します。 **[OK]** をクリックして、プロジェクトを開きます。

     ![Windows フォーム アプリケーション プロジェクト](../data-tools/media/wcf7.png)

3. **[WindowsApplication1]** を右クリックして **[サービス参照の追加]** をクリックします。 [**サービス参照の追加**] ダイアログ ボックスが表示されます。

4. **[サービス参照の追加]** ダイアログ ボックスで、**[探索]** をクリックします。

     ![[サービス参照の追加] ダイアログ ボックス](../data-tools/media/wcf8.png)

     **Service1** が **[サービス]** ペインに表示されます。

5. **[OK]** をクリックしてサービス参照を追加します。

### <a name="build-a-client-application"></a>クライアント アプリケーションを構築します

1. **ソリューション エクスプローラー** で、**[Form1.vb]** または **[Form1.cs]** をダブルクリックして、Windows フォーム デザイナーを (まだ開いていない場合に) 開きます。

2. **ツールボックス** で、`TextBox` コントロール、`Label` コントロール、および `Button` コントロールをフォームにドラッグします。

     ![フォームへのコントロールの追加](../data-tools/media/wcf9.png)

3. `Button` をダブルクリックし、`Click` イベント ハンドラーに次のコードを追加します。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/wcfwalkthrough/cs/form1.cs" id="Snippet3":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/wcfwalkthrough/vb/form1.vb" id="Snippet3":::

4. **ソリューション エクスプローラー** で、**[WindowsApplication1]** を右クリックして **[スタートアップ プロジェクトに設定]** をクリックします。

5. **F5** キーを押してプロジェクトを実行します。 いくつかのテキストを入力し、ボタンをクリックします。 ラベルに「You entered:」と入力したテキストが表示されます。

     ![結果を表示するフォーム](../data-tools/media/wcf10.png)

## <a name="see-also"></a>関連項目

- [Visual Studio での Windows Communication Foundation サービスと WCF データ サービス](../data-tools/windows-communication-foundation-services-and-wcf-data-services-in-visual-studio.md)
