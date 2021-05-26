---
title: 設定カテゴリの作成 | Microsoft Docs
description: Visual Studio の設定カテゴリを作成し、それを使用して設定ファイルの値を保存および復元する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- profile settings, creating categories
ms.assetid: 97c88693-05ff-499e-8c43-352ee073dcb7
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 1e3ef6dbfc58c67ce8e4dd7ff26634e4dbce2218
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105089343"
---
# <a name="create-a-settings-category"></a>設定カテゴリの作成

このチュートリアルでは、Visual Studio の設定カテゴリを作成し、それを使用して設定ファイルの値を保存および復元します。 設定カテゴリは、"カスタム設定ポイント"、つまり、**設定のインポートとエクスポート** ウィザードのチェック ボックスとして表示される関連プロパティのグループです (このウィザードは **[ツール]** メニューにあります)。設定はカテゴリとして保存または復元されます。また、個々の設定はウィザードに表示されません。 詳細については、[環境設定](../ide/environment-settings.md)に関するページを参照してください。

設定カテゴリは、<xref:Microsoft.VisualStudio.Shell.DialogPage> クラスから派生させて作成します。

このチュートリアルを開始するには、まず、「[オプション ページを作成する](../extensibility/creating-an-options-page.md)」の最初のセクションを完了する必要があります。 結果のオプションのプロパティ グリッドを使用すると、カテゴリ内のプロパティを確認および変更できます。 プロパティ カテゴリを設定ファイルに保存した後、ファイルを調べて、プロパティ値がどのように格納されているかを確認します。

## <a name="prerequisites"></a>必須コンポーネント
 Visual Studio 2015 以降では、ダウンロード センターからの Visual Studio SDK のインストールは行いません。 これは、Visual Studio セットアップにオプション機能として含まれています。 VS SDK は、後でインストールすることもできます。 詳細については、「[Visual Studio SDK のインストール](../extensibility/installing-the-visual-studio-sdk.md)」を参照してください。

## <a name="create-a-settings-category"></a>設定カテゴリの作成
 このセクションでは、カスタム設定ポイントを使用して、設定カテゴリの値を保存および復元します。

### <a name="to-create-a-settings-category"></a>設定カテゴリを作成するには

1. 「[オプション ページを作成する](../extensibility/creating-an-options-page.md)」を完了します。

2. *VSPackage.resx* ファイルを開き、次の 3 つの文字列リソースを追加します。

    |名前|値|
    |----------|-----------|
    |106|My Category|
    |107|[個人の設定]|
    |108|OptionInteger and OptionFloat|

     これにより、カテゴリ名が "My Category"、オブジェクト名が "My Settings"、カテゴリの説明が "OptionInteger and OptionFloat" であるリソースが作成されます。

    > [!NOTE]
    > これら 3 つのうち、カテゴリ名だけが、**設定のインポートとエクスポート** ウィザードに表示されません。

3. *MyToolsOptionsPackage.cs* で、次の例に示すように、`OptionFloat` という名前の `float` プロパティを `OptionPageGrid` クラスに追加します。

    ```csharp
    public class OptionPageGrid : DialogPage
    {
        private int optionInt = 256;
        private float optionFloat = 3.14F;

        [Category("My Options")]
        [DisplayName("My Integer option")]
        [Description("My integer option")]
        public int OptionInteger
        {
            get { return optionInt; }
            set { optionInt = value; }
        }
        [Category("My Options")]
        [DisplayName("My Float option")]
        [Description("My float option")]
        public float OptionFloat
        {
            get { return optionFloat; }
            set { optionFloat = value; }
        }
    }
    ```

    > [!NOTE]
    > "My Category" という名前の `OptionPageGrid` カテゴリは、`OptionInteger` と `OptionFloat` という 2 つのプロパティで構成されるようになりました。

4. <xref:Microsoft.VisualStudio.Shell.ProvideProfileAttribute> を `MyToolsOptionsPackage` クラスに追加し、CategoryName に "My Category"、ObjectName に "My Settings" を指定し、isToolsOptionPage を true に設定します。 categoryResourceID、objectNameResourceID、DescriptionResourceID を、前に作成した対応する文字列リソース ID に設定します。

    ```csharp
    [ProvideProfileAttribute(typeof(OptionPageGrid),
        "My Category", "My Settings", 106, 107, isToolsOptionPage:true, DescriptionResourceID = 108)]
    ```

5. プロジェクトをビルドし、デバッグを開始します。 実験用インスタンスでは、 **[My Grid Page]** に整数値と浮動小数点値の両方が指定されていることがわかります。

## <a name="examine-the-settings-file"></a>設定ファイルを確認する
 このセクションでは、プロパティ カテゴリの値を設定ファイルにエクスポートします。 ファイルを調べてから、プロパティ カテゴリに値をインポートします。

1. **F5** キーを押して、デバッグ モードでプロジェクトを開始します。 これにより、実験用インスタンスが開始されます。

2. **[ツール]**  >  **[オプション]** ダイアログを開きます。

3. 左側のペインのツリー ビューで、 **[My Category]** を展開し、 **[My Grid Page]** をクリックします。

4. **[OptionFloat]** の値を 3.1416 に、 **[OptionInteger]** を 12 に変更します。 **[OK]** をクリックします。

5. **[ツール]** メニューの **[設定のインポートとエクスポート]** を選択します。

     **設定のインポートとエクスポート** ウィザードが表示されます。

6. **[選択された環境設定をエクスポート]** が選択されていることを確認し、 **[次へ]** をクリックします。

     **[エクスポートする設定の選択]** ページが表示されます。

7. **[My Settings]** をクリックします。

     **[説明]** は、 **[OptionInteger and OptionFloat]** に変わります。

8. **[My Settings]** が選択されている唯一のカテゴリであることを確認し、 **[次へ]** をクリックします。

     **[設定ファイルの名前を指定してください]** ページが表示されます。

9. 新しい設定ファイルに「*MySettings.vssettings*」という名前を付け、適切なディレクトリに保存します。 **[完了]** をクリックします。

     **[エクスポートの完了]** ページに、設定が正常にエクスポートされたことが表示されます。

10. **[ファイル]** メニューの **[開く]** をポイントし、 **[ファイル]** をクリックします。 *MySettings.vssettings* を検索して開きます。

     エクスポートしたプロパティ カテゴリは、ファイルの次のセクションで確認できます (GUID は異なります)。

    ```
    <Category name="My Category_My Settings"
          Category="{4802bc3e-3d9d-4591-8201-23d1a05216a6}"
          Package="{6bb6942e-014c-489e-a612-a935680f703d}"
          RegisteredName="My Category_My Settings">
          PackageName="MyToolsOptionsPackage">
       <PropertyValue name="OptionFloat">3.1416</PropertyValue>
       <PropertyValue name="OptionInteger">12</PropertyValue>
    </Category>
    ```

     完全なカテゴリ名は、カテゴリ名にアンダースコアを付加し、その後にオブジェクト名が続いていることに注意してください。 OptionFloat と OptionInteger は、エクスポートされた値と共にカテゴリ内に出力されています。

11. 設定ファイルを変更せずに閉じます。

12. **[ツール]** メニューの **[オプション]** をクリックし、 **[My Category]** を展開して、 **[My Grid Page]** をクリックします。次に、 **[OptionFloat]** の値を 1.0 に変更し、 **[OptionInteger]** を 1 に変更します。 **[OK]** をクリックします。

13. **[ツール]** メニューで、 **[設定のインポートとエクスポート]** をクリックし、 **[選択された環境設定をインポート]** を選択し、 **[次へ]** をクリックします。

     **[現在の設定の保存]** ページが表示されます。

14. **[いいえ、新しい設定をインポートします]** を選択し、 **[次へ]** をクリックします。

     **[インポートする設定コレクションの選択]** ページが表示されます。

15. ツリー ビューの **[My Settings]** ノードで、*MySettings.vssettings* ファイルを選択します。 ファイルがツリー ビューに表示されない場合は、 **[参照]** をクリックして検索します。 **[次へ]** をクリックします。

     **[インポートする設定の選択]** ダイアログ ボックスが表示されます。

16. **[My Settings]** が選択されていることを確認し、 **[完了]** をクリックします。 **[インポートの完了]** ページが表示されたら、 **[閉じる]** をクリックします。

17. **[ツール]** メニューの **[オプション]** をクリックし、 **[My Category]** を展開し、 **[My Grid Page]** をクリックして、プロパティ カテゴリの値が復元されていることを確認します。
