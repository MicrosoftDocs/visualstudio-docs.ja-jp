---
title: プロパティ ウィンドウにプロパティを表示する | Microsoft Docs
description: オブジェクトのパブリック プロパティについて説明します。 これらのプロパティに加えた変更は、[プロパティ] ウィンドウに反映されます。
ms.custom: SEO-VS-2020
ms.date: 3/16/2019
ms.topic: conceptual
helpviewer_keywords:
- properties [Visual Studio SDK], exposing in Property Browser
- properties [Visual Studio SDK]
- Property Browser, exposing properties
ms.assetid: 47f295b5-1ca5-4e7b-bb52-7b926b136622
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: b9de86e956fe6a4d7841d519d7252b75ae216229
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105075251"
---
# <a name="expose-properties-to-the-properties-window"></a>[プロパティ] ウィンドウにプロパティを表示する

このチュートリアルでは、オブジェクトのパブリック プロパティを **[プロパティ]** ウィンドウに表示します。 これらのプロパティに加えた変更は、 **[プロパティ]** ウィンドウに反映されます。

## <a name="prerequisites"></a>必須コンポーネント

Visual Studio 2015 以降では、ダウンロード センターから Visual Studio SDK をインストールしません。 これは、Visual Studio のセットアップにオプション機能として含まれています。 VS SDK は、後でインストールすることもできます。 詳細については、「[Visual Studio SDK のインストール](../extensibility/installing-the-visual-studio-sdk.md)」を参照してください。

## <a name="expose-properties-to-the-properties-window"></a>[プロパティ] ウィンドウにプロパティを表示する

このセクションでは、カスタム ツール ウィンドウを作成し、関連付けられているウィンドウ ペイン オブジェクトのパブリック プロパティを **[プロパティ]** ウィンドウに表示します。

### <a name="to-expose-properties-to-the-properties-window"></a>[プロパティ] ウィンドウにプロパティを表示するには

1. すべての Visual Studio 拡張機能は、拡張機能アセットを格納する VSIX デプロイ プロジェクトから始まります。 `MyObjectPropertiesExtension` という名前の [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] VSIX プロジェクトを作成します。 VSIX プロジェクト テンプレートは、 **[新しいプロジェクト]** ダイアログで「vsix」と検索すると見つかります。

2. `MyToolWindow` という名前のカスタム ツール ウィンドウ項目テンプレートを追加して、ツール ウィンドウを追加します。 **ソリューション エクスプローラー** で、プロジェクト ノードを右クリックして、 **[追加]**  >  **[新しい項目]** の順に選択します。 **[新しい項目の追加]** ダイアログで、 **[Visual C# 項目]**  >  **[機能拡張]** の順にアクセスし、 **[カスタム ツール ウィンドウ]** を選択します。 ダイアログの下部にある **[名前]** フィールドで、ファイル名を *MyToolWindow.cs* に変更します。 カスタム ツール ウィンドウの作成方法の詳細については、「[ツール ウィンドウで拡張機能を作成する](../extensibility/creating-an-extension-with-a-tool-window.md)」を参照してください。

3. *MyToolWindow.cs* を開いて、次の using ステートメントを追加します。

   ```csharp
   using System.Collections;
   using System.ComponentModel;
   using Microsoft.VisualStudio.Shell.Interop;
   ```

4. `MyToolWindow` クラスに次のフィールドを追加します。

   ```csharp
   private ITrackSelection trackSel;
   private SelectionContainer selContainer;

   ```

5. 次のコードを `MyToolWindow` クラスに追加します。

   ```csharp
   private ITrackSelection TrackSelection
   {
       get
       {
           if (trackSel == null)
               trackSel =
                  GetService(typeof(STrackSelection)) as ITrackSelection;
           return trackSel;
       }
   }

   public void UpdateSelection()
   {
       ITrackSelection track = TrackSelection;
       if (track != null)
           track.OnSelectChange((ISelectionContainer)selContainer);
   }

   public void SelectList(ArrayList list)
   {
       selContainer = new SelectionContainer(true, false);
       selContainer.SelectableObjects = list;
       selContainer.SelectedObjects = list;
       UpdateSelection();
   }

   public override void OnToolWindowCreated()
   {
       ArrayList listObjects = new ArrayList();
       listObjects.Add(this);
       SelectList(listObjects);
   }
   ```

    `TrackSelection` プロパティでは、`GetService` を使用して `STrackSelection` サービスを取得します。これによって、<xref:Microsoft.VisualStudio.Shell.Interop.ITrackSelection> インターフェイスが提供されます。 `OnToolWindowCreated` イベント ハンドラーと `SelectList` メソッドを一緒に使用すると、ツール ウィンドウ ペイン オブジェクト自体だけが含まれる、選択したオブジェクトのリストが作成されます。 `UpdateSelection` メソッドによって、ツール ウィンドウ ペインのパブリック プロパティを表示するように、 **[プロパティ]** ウィンドウに通知されます。

6. プロジェクトをビルドし、デバッグを開始します。 Visual Studio の実験用インスタンスが表示されます。

7. **[プロパティ]** ウィンドウが表示されない場合は、**F4** キーを押して開きます。

8. **[MyToolWindow]** ウィンドウを開きます。 **[ビュー]**  >  **[その他のウィンドウ]** で見つけることができます。

    ウィンドウが開き、 **[プロパティ]** ウィンドウにウィンドウ ペインのパブリック プロパティが表示されます。

9. **[プロパティ]** ウィンドウの **[キャプション]** プロパティを **[マイ オブジェクトのプロパティ**] に変更します。

     [MyToolWindow] ウィンドウのキャプションが、それに応じて変更されます。

## <a name="expose-tool-window-properties"></a>ツール ウィンドウのプロパティを表示する

このセクションでは、ツール ウィンドウを追加し、そのプロパティを表示します。 プロパティに加えた変更は、 **[プロパティ]** ウィンドウに反映されます。

### <a name="to-expose-tool-window-properties"></a>ツール ウィンドウのプロパティを表示するには

1. *MyToolWindow.cs* を開き、パブリック ブール型プロパティ IsChecked を `MyToolWindow` クラスに追加します。

    ```csharp
    [Category("My Properties")]
    [Description("MyToolWindowControl properties")]
    public bool IsChecked
    {
        get {
            if (base.Content == null)  return false;
            return (bool)(( MyToolWindowControl) base.Content).checkBox.IsChecked;
        }
        set {
            ((MyToolWindowControl) base.Content).checkBox.IsChecked = value;
        }
    }
    ```

     このプロパティでは、後で作成する WPF チェック ボックスから状態を取得します。

2. *MyToolWindowControl.xaml.cs* を開き、MyToolWindowControl コンストラクターを次のコードに置き換えます。

    ```vb
    private MyToolWindow pane;
    public MyToolWindowControl(MyToolWindow pane)
    {
        InitializeComponent();
        this.pane = pane;
        checkBox.IsChecked = false;
    }
    ```

     これにより、`MyToolWindowControl` で `MyToolWindow` ペインにアクセスできるようになります。

3. *MyToolWindow.cs* で、次のように `MyToolWindow` コンストラクターを変更します。

    ```csharp
    base.Content = new MyToolWindowControl(this);
    ```

4. MyToolWindowControl のデザイン ビューに変更します。

5. ボタンを削除し、**ツールボックス** から左上隅にチェック ボックスを追加します。

6. Checked および Unchecked イベントを追加します。 デザイン ビューでチェック ボックスをオンにします。 **[プロパティ]** ウィンドウで、イベント ハンドラー ボタン ( **[プロパティ]** ウィンドウの右上) をクリックします。 **[Checked]** を見つけて、テキスト ボックスに「**checkbox_Checked**」と入力し、 **[Unchecked]** を見つけて、テキスト ボックスに「**checkbox_Unchecked**」と入力します。

7. チェック ボックスのイベント ハンドラーを追加します。

    ```csharp
    private void checkbox_Checked(object sender, RoutedEventArgs e)
    {
        pane.IsChecked = true;
        pane.UpdateSelection();
    }
    private void checkbox_Unchecked(object sender, RoutedEventArgs e)
    {
        pane.IsChecked = false;
        pane.UpdateSelection();
    }
    ```

8. プロジェクトをビルドし、デバッグを開始します。

9. 実験用インスタンスで、 **[MyToolWindow]** ウィンドウを開きます。

     **[プロパティ]** ウィンドウで、ウィンドウのプロパティを探します。 **[IsChecked]** プロパティは、ウィンドウの下部の **[マイ プロパティ]** カテゴリの下に表示されます。

10. **[MyToolWindow]** ウィンドウのチェック ボックスをオンにします。 **[プロパティ]** ウィンドウの **[IsChecked]** が **True** に変更されます。 **[MyToolWindow]** ウィンドウのチェック ボックスをクリアします。 **[プロパティ]** ウィンドウの **[IsChecked]** が **False** に変更されます。 **[プロパティ]** ウィンドウの **[IsChecked]** の値を変更します。 **[MyToolWindow]** ウィンドウのチェック ボックスが、新しい値と一致するように変更されます。

    > [!NOTE]
    > **[プロパティ]** ウィンドウに表示されるオブジェクトを破棄する必要がある場合は、`null` 選択コンテナーを先頭にして `OnSelectChange` を呼び出します。 プロパティまたはオブジェクトを破棄したら、更新された <xref:Microsoft.VisualStudio.Shell.SelectionContainer.SelectableObjects%2A> および <xref:Microsoft.VisualStudio.Shell.SelectionContainer.SelectedObjects%2A> リストがある選択コンテナーに変更できます。

## <a name="change-selection-lists"></a>選択リストを変更する

 このセクションでは、基本プロパティ クラスの選択リストを追加し、ツール ウィンドウ インターフェイスを使用して、表示する選択リストを選択します。

### <a name="to-change-selection-lists"></a>選択リストを変更するには

1. *MyToolWindow.cs* を開いて、`Simple` という名前のパブリック クラスを追加します。

    ```csharp
    public class Simple
    {
        private string someText = "";

        [Category("My Properties")]
        [Description("Simple Properties")]
        [DisplayName("My Text")]
        public string SomeText
        {
            get { return someText; }
            set { someText = value; }
        }

        [Category("My Properties")]
        [Description("Read-only property")]
        public bool ReadOnly
        {
            get { return false; }
        }
    }
    ```

2. `MyToolWindow` クラスに `SimpleObject` プロパティと 2 つのメソッドを追加します。これらのメソッドでは、ウィンドウ ペインと `Simple` オブジェクトの間で **[プロパティ]** ウィンドウの選択を切り替えます。

    ```csharp
    private Simple simpleObject = null;
    public Simple SimpleObject
    {
        get
        {
            if (simpleObject == null) simpleObject = new Simple();
            return simpleObject;
        }
    }

    public void SelectSimpleList()
    {
        ArrayList listObjects = new ArrayList();
        listObjects.Add(SimpleObject);
        SelectList(listObjects);
    }

    public void SelectThisList()
    {
        ArrayList listObjects = new ArrayList();
        listObjects.Add(this);
        SelectList(listObjects);
    }
    ```

3. *MyToolWindowControl.cs* で、チェック ボックスのハンドラーを次のコード行に置き換えます。

    ```csharp
    private void checkbox_Checked(object sender, RoutedEventArgs e)
     {
        pane.IsChecked = true;
        pane.SelectSimpleList();
        pane.UpdateSelection();
    }
    private void checkbox_Unchecked(object sender, RoutedEventArgs e)
    {
        pane.IsChecked = false;
        pane.SelectThisList();
        pane.UpdateSelection();
    }
    ```

4. プロジェクトをビルドし、デバッグを開始します。

5. 実験用インスタンスで、 **[MyToolWindow]** ウィンドウを開きます。

6. **[MyToolWindow]** ウィンドウのチェック ボックスを選択します。 **[プロパティ]** ウィンドウには、`Simple` オブジェクトのプロパティ ( **[SomeText]** と **[ReadOnly]** ) が表示されます。 チェック ボックスをオフにする ウィンドウのパブリック プロパティが **[プロパティ]** ウィンドウに表示されます。

    > [!NOTE]
    > **[SomeText]** の表示名は **[My Text]** です。

## <a name="best-practice"></a>ベスト プラクティス

このチュートリアルでは、選択可能なオブジェクト コレクションと選択されたオブジェクト コレクションが同じコレクションになるように、<xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer> が実装されます。 選択されたオブジェクトのみが [プロパティ ブラウザー] の一覧に表示されます。 ISelectionContainer の実装の詳細については、Reference.ToolWindow のサンプルを参照してください。

Visual Studio のツール ウィンドウは、Visual Studio のセッション間で保持されます。 ツール ウィンドウの状態の保持の詳細については、<xref:Microsoft.VisualStudio.Shell.ProvideProfileAttribute> を参照してください。

## <a name="see-also"></a>関連項目

- [プロパティとプロパティ ウィンドウを拡張する](../extensibility/extending-properties-and-the-property-window.md)
