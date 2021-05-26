---
title: 'チュートリアル: スタート ページへのカスタム XAML の追加 | Microsoft Docs'
description: このチュートリアルを使用して、Web ブラウザーを含む Visual Studio のカスタム スタート ページを作成する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- custom start page
- xaml start page
ms.assetid: 9af4d5f9-1cfc-4221-aea7-c8cd3f7571a6
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
monikerRange: vs-2017
ms.openlocfilehash: 972f8c477a62078b14d16ff61d3f6b8c7978616d
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105062032"
---
# <a name="walkthrough-add-custom-xaml-to-the-start-page"></a>チュートリアル: カスタム XAML をスタート ページに追加する

このチュートリアルでは、Web ブラウザーを含む Visual Studio のカスタム スタート ページを作成する方法について説明します。

## <a name="add-custom-xaml"></a>カスタム XAML を追加する

1. 「[カスタム スタート ページを作成する](../extensibility/creating-a-custom-start-page.md)」の手順に従って、スタート ページを作成します。

2. *MainWindow.xaml* ファイルで、\<Grid> セクションを見つけます。

3. 次の例に示すように、\< Grid> 要素内に \<TabControl> 要素と \<TabItem> を追加します。

    ```xml
    <Grid>
        <TabControl>
            <TabItem Header="Bing" Height="Auto">
                <Frame Source="http://www.bing.com" />
            </TabItem>
        </TabControl>
    </Grid>
    ```

4. 新しいプロジェクトを開く \<Button> 要素を含む 2 つ目の \<TabItem> を追加します。

    ```xml
    <Grid>
        <TabControl>
            <TabItem Header="MyButton" Height="Auto">
                <Button Name="btnNewProj" Content="New Project"
                    Command="{x:Static vscom:VSCommands.ExecuteCommand}"
                    CommandParameter="File.NewProject" >
                </Button>
            </TabItem>
            <TabItem Header="Bing" Height="Auto">
                <Frame Source="http://www.bing.com" />
            </TabItem>
        </TabControl>
    </Grid>
    ```

## <a name="test-the-custom-start-page"></a>カスタム スタート ページをテストする

1. **F5** キーを押します。

     Visual Studio の実験用インスタンスが開き、カスタム スタート ページがインストールされますが、選択されていません。

2. Visual Studio の実験用インスタンスで、 **[ツール] > [オプション] > [環境]** ページを開きます。

3. **[スタートアップ]** を選択します。 **[スタート ページのカスタマイズ]** の一覧で、 *.xaml* ファイルを選択して **[OK]** をクリックします。

4. **[表示]** メニューの **[スタート ページ]** をクリックします。

5. **[Bing]** タブをクリックします。

     Bing の Web ページが表示されます。

6. **[MyButton]** タブをクリックします。

     **[新しいプロジェクト]** ダイアログを開く **[MyProject]** ボタンが表示されます。

7. 実験用インスタンスを閉じます。

カスタム スタート ページを適用するには、 **[ツール]**  >  **[オプション]**  >  **[環境]** で **[スタートアップ]** を選択します。 **[スタート ページのカスタマイズ]** の一覧で、 *.xaml* ファイルを選択して **[OK]** をクリックします。

## <a name="next-steps"></a>次のステップ

これで、Visual Studio のスタート ページに [Web ブラウザー] タブと [MyButton] タブを表示するタブが含まれるようになりました。他の機能を持つカスタム スタート ページを作成するには、「[スタート ページへのユーザー コントロールの追加](../extensibility/adding-user-control-to-the-start-page.md)」の説明に従って、*分離コード* モデルを使用してカスタム .dll を追加します。 作成された .vsix ファイルを [Visual Studio Marketplace](https://marketplace.visualstudio.com/) Web サイト、または別の Web サイトやネットワーク共有に発行すると、カスタム スタート ページを他のユーザーと共有できます。 詳細については、「 [Deploying Custom Start Pages](../extensibility/deploying-custom-start-pages.md)」を参照してください。

## <a name="see-also"></a>関連項目

- [スタート ページのカスタマイズ](../ide/customizing-the-start-page-for-visual-studio.md)
- [WPF コンテナー コントロール](/previous-versions/bb675291(v=vs.110))