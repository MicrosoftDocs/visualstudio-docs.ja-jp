---
title: Creating a Settings Category |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- profile settings, creating categories
ms.assetid: 97c88693-05ff-499e-8c43-352ee073dcb7
caps.latest.revision: 40
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: d14e60ec28fb5f8ba80f9986c4316058539b35e6
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/15/2019
ms.locfileid: "65695022"
---
# <a name="creating-a-settings-category"></a>設定カテゴリの作成
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

このチュートリアルでは、Visual Studio の設定のカテゴリを作成し、使用する値を保存し、値の設定ファイルから復元します。 設定のカテゴリは「カスタム設定ポイント」; として表示される関連するプロパティのグループです。つまりのチェック ボックスと、**インポートおよびエクスポート設定**ウィザード。 (で検索することができます、**ツール**メニュー)。設定の保存や、カテゴリとして復元し、個々 の設定は、ウィザードに表示されません。 詳細については、「 [Visual Studio での開発設定のカスタマイズ](https://msdn.microsoft.com/22c4debb-4e31-47a8-8f19-16f328d7dcd3)」を参照してください。  
  
 派生することによって設定のカテゴリを作成する、<xref:Microsoft.VisualStudio.Shell.DialogPage>クラス。  
  
 このチュートリアルを開始するの最初のセクションを完了する必要がありますまず[オプション ページの作成](../extensibility/creating-an-options-page.md)です。 結果として得られるオプションのプロパティ グリッドを確認し、カテゴリのプロパティを変更できます。 プロパティのカテゴリの設定ファイルを保存した後は、プロパティ値を格納する方法を参照してください。 ファイルを確認します。  
  
## <a name="prerequisites"></a>必須コンポーネント  
 Visual Studio 2015 以降、ダウンロード センターから Visual Studio SDK をインストールすることはできません。 これは Visual Studio のセットアップにオプション機能として含まれるようになりました。 また、後から VS SDK をインストールすることもできます。 より詳細な情報については 、[Visual Studio SDK のインストール](../extensibility/installing-the-visual-studio-sdk.md) に関する記事を参照してください。  
  
## <a name="creating-a-settings-category"></a>設定カテゴリの作成  
 このセクションでは、カスタム設定ポイントを使用して保存し、設定カテゴリの値を復元します。  
  
#### <a name="to-create-a-settings-category"></a>設定カテゴリを作成するには  
  
1. 完了、[オプション ページの作成](../extensibility/creating-an-options-page.md)です。  
  
2. VSPackage.resx ファイルを開き、次の 3 つの文字列リソースを追加します。  
  
    |名前|値|  
    |----------|-----------|  
    |106|私のカテゴリ|  
    |107|設定|  
    |108|OptionInteger と OptionFloat|  
  
     これにより、その名前は"My Category"のカテゴリや、オブジェクト"My Settings"、"OptionInteger と OptionFloat"カテゴリの説明、リソースを作成します。  
  
    > [!NOTE]
    > これらの 3 つのカテゴリの名前だけは、インポートとエクスポートの設定ウィザードでは表示されません。  
  
3. MyToolsOptionsPackage.cs で追加、`float`という名前のプロパティ`OptionFloat`を`OptionPageGrid`クラスに、次の例に示すようにします。  
  
    ```csharp  
    public class OptionPageGrid : DialogPage  
    {  
        private int optionInt = 256;  
        private float optionFloat = 3.14F;  
  
        [Category("My Options")]  
        [DisplayName("My Integer option")]  
        [Description("My integer option")]  
        public int OptionInteger  
        {  
            get { return optionInt; }  
            set { optionInt = value; }  
        }  
        [Category("My Options")]  
        [DisplayName("My Float option")]  
        [Description("My float option")]  
        public float OptionFloat  
        {  
            get { return optionFloat; }  
            set { optionFloat = value; }  
        }  
    }  
    ```  
  
    > [!NOTE]
    > `OptionPageGrid` "My Category"を今すぐという名前のカテゴリには 2 つのプロパティの`OptionInteger`と`OptionFloat`します。  
  
4. 追加、<xref:Microsoft.VisualStudio.Shell.ProvideProfileAttribute>を`MyToolsOptionsPackage`クラスし CategoryName"My Category"を付けます、ObjectName"My Settings"を付けますおよび isToolsOptionPage を true に設定します。 対応する文字列リソース Id が前に作成する categoryResourceID、objectNameResourceID、および DescriptionResourceID を設定します。  
  
    ```csharp  
    [ProvideProfileAttribute(typeof(OptionPageGrid),   
        "My Category", "My Settings", 106, 107, isToolsOptionPage:true, DescriptionResourceID = 108)]  
    ```  
  
5. プロジェクトをビルドし、デバッグを開始します。 実験用インスタンスを参照する必要があります**マイのグリッド ページ**整数と浮動小数点数の両方の値になりました。  
  
## <a name="examining-the-settings-file"></a>設定ファイルの確認  
 このセクションでは、プロパティのカテゴリの値を設定ファイルにエクスポートします。 ファイルを確認し、プロパティのカテゴリに値をインポートします。  
  
1. F5 キーを押してデバッグ モードで、プロジェクトを起動します。 これは、実験用インスタンスを起動します。  
  
2. 開く、**ツール/オプション**ダイアログ。  
  
3. 左側のウィンドウで、ツリー ビューで、展開**My Category**  をクリックし、**マイのグリッド ページ**します。  
  
4. 値を変更**OptionFloat** 3.1416 へと**OptionInteger** 12 にします。 **[OK]** をクリックします。  
  
5. **[ツール]** メニューの **[設定のインポートとエクスポート]** を選択します。  
  
     **インポートおよびエクスポート設定**ウィザードが表示されます。  
  
6. 確認します**選択された環境設定のエクスポート**が選択されているし、をクリックし、**次**します。  
  
     **エクスポートする設定**ページが表示されます。  
  
7. クリックして**My Settings**します。  
  
     **説明**変更**OptionInteger と OptionFloat**します。  
  
8. 確認します**My Settings**唯一のカテゴリを選択し、**次**します。  
  
     **名前、設定ファイル**ページが表示されます。  
  
9. 新しい設定ファイルの名前を付けます`MySettings.vssettings`し、適切なディレクトリに保存します。 **[完了]** をクリックします。  
  
     **エクスポートの完了**の設定が正常にエクスポートされたページに表示します。  
  
10. **ファイル**メニューで、**オープン**、をクリックし、**ファイル**。 検索`MySettings.vssettings`を開きます。  
  
     (、Guid は異なります)、ファイルの次のセクションでエクスポートしたプロパティのカテゴリが表示されます。  
  
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
  
     カテゴリ名の後に、オブジェクト名にアンダー スコアの追加により、完全なカテゴリ名を生成することに注意してください。 OptionFloat と OptionInteger は、そのエクスポート値と共に、カテゴリに表示されます。  
  
11. これを変更することがなく、設定ファイルを閉じます。  
  
12. **ツール** メニューのをクリックして**オプション**、展開**My Category**、 をクリックして**マイのグリッド ページ**しの値変更**OptionFloat** 1.0 と**OptionInteger**を 1 にします。 **[OK]** をクリックします。  
  
13. **ツール** メニューのをクリックして**インポートおよびエクスポート設定**を選択します**選択された環境設定のインポート**、順にクリックします**次**。  
  
     **現在の設定の保存**ページが表示されます。  
  
14. 選択**いいえ、新しい設定をインポート**順にクリックします**次**します。  
  
     **インポートする設定コレクションの選択**ページが表示されます。  
  
15. 選択、`MySettings.vssettings`ファイル、 **My Settings**ツリー ビューのノード。 ツリー ビューで、ファイルが表示されない場合はクリックして**参照**だとします。 **[次へ]** をクリックします。  
  
     **[設定のインポートに**] ダイアログ ボックスが表示されます。  
  
16. 確認します**My Settings**が選択されているし、をクリックし、**完了**します。 ときに、**インポートの完了**ページが表示されたら、をクリックして**閉じる**します。  
  
17. **ツール** メニューのをクリックして**オプション**、展開**My Category**、 をクリックして**マイのグリッド ページ**プロパティ カテゴリの値があることを確認します復元されました。
