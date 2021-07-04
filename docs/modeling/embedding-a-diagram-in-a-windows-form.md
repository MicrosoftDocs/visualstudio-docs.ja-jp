---
title: Windows フォームでのダイアグラムの埋め込み
description: Visual Studio ウィンドウに表示される Windows コントロールに DSL 図を埋め込む方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 4db60267b835882a69a08c990af644b902697bad
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/19/2021
ms.locfileid: "112388985"
---
# <a name="embed-a-diagram-in-a-windows-form"></a>Windows フォームにダイアグラムを埋め込む

Visual Studio ウィンドウに表示される Windows コントロールに DSL 図を埋め込むことができます。

## <a name="embed-a-dsl-diagram-in-a-windows-control"></a>Windows コントロールに DSL 図を埋め込む

1. 新しい **ユーザー コントロール** ファイルを DslPackage プロジェクトに追加します。

2. Panel コントロールをユーザー コントロールに追加します。 このパネルに、DSL の図が表示されます。

     必要なその他のコントロールを追加します。

     コントロールのアンカー プロパティを設定します。

3. ソリューション エクスプローラーでユーザー コントロール ファイルを右クリックし、 **[コードの表示]** をクリックします。 次のコンストラクターと変数をコードに追加します。

    ```csharp
    internal UserControl1(MyDSLDocView docView, Control content)
      : this()
    {
      panel1.Controls.Add(content);
      this.docView = docView;
    }
    private MyDSLDocView docView;
    ```

4. 次の内容の新しいファイルを、DslPackage プロジェクトに追加します。

    ```csharp
    using System.Windows.Forms;
    namespace Company.MyDSL
    {
      partial class MyDSLDocView
      {
        private UserControl1 container;
        public override IWin32Window Window
        {
          get
          {
            if (container == null)
            {
              // Put our own form inside the DSL window:
              container = new UserControl1(this,
                (Control)base.Window);
            }
            return container;
    } } } }
    ```

5. DSL をテストするために、**F5** キーを押してサンプル モデル ファイルを開きます。 コントロール内に図が表示されます。 ツールボックスとその他の機能は、通常どおり動作します。

## <a name="update-the-form-using-store-events"></a>ストア イベントを使用してフォームを更新する

1. フォーム デザイナーで、`listBox1` という名前の **ListBox** を追加します。 これにより、モデル内の要素の一覧が表示されます。 それは、*ストア イベント* を使用してモデルと同期されます。 詳細については、「[イベント ハンドラーによって変更がモデル外に反映される](../modeling/event-handlers-propagate-changes-outside-the-model.md)」を参照してください。

2. カスタム コード ファイルで、他のメソッドを DocView クラスにオーバーライドします。

    ```csharp
    partial class MyDSLDocView
    {
     /// <summary>
     /// Register store event listeners.
     /// This method is called when the model and diagram
     /// have completed loading.
     /// </summary>
     protected override bool LoadView()
      {
        bool result = base.LoadView();
        Store store = this.DocData.Store;
        EventManagerDirectory emd = store.EventManagerDirectory;
        DomainClassInfo componentClass = store.DomainDataDirectory.FindDomainClass(typeof(ExampleElement));
        emd.ElementAdded.Add(componentClass, new EventHandler<ElementAddedEventArgs>(AddElement));
        emd.ElementDeleted.Add(componentClass, new EventHandler<ElementDeletedEventArgs>(RemoveElement));

        // Do the initial parts list:
        container.SetUpFormFromModel();
        return result;
      }
     /// <summary>
     /// Listener method called on creation of each instance of
     /// the ExampleElement class or its subclasses.
     /// </summary>
     private void AddElement(object sender, ElementAddedEventArgs e)
     {
       container.Add(e.ModelElement as ExampleElement);
     }
     /// <summary>
     /// Listener method called after deletion of each instance of
     /// the ExampleElement class or its subclasses.
     /// </summary>
     private void RemoveElement(object sender, ElementDeletedEventArgs e)
     {
       container.Remove(e.ModelElement as ExampleElement);
     }
    ```

3. ユーザー コントロールの分離コードに、追加および削除された要素をリッスンするメソッドを挿入します。

    ```csharp
    public partial class UserControl1 : UserControl { ...

    private ExampleModel modelRoot;

    internal void Add(ExampleElement e) { UpdatePartsList(); }
    internal void Remove(ExampleElement e) { UpdatePartsList(); }

    internal void SetUpFormFromModel()
    {
      modelRoot = this.docView.CurrentDiagram.ModelElement as ExampleModel;
      UpdatePartsList();
    }

    private void UpdatePartsList()
    {
      StringBuilder builder = new StringBuilder();
      listBox1.Items.Clear();
      foreach (ExampleElement c in modelRoot.Elements)
      {
        listBox1.Items.Add(c.Name);
      }
    }
    ```

4. DSL をテストするために、**F5** キーを押し、Visual Studio の実験用インスタンスでサンプル モデル ファイルを開きます。

     リスト ボックスには、モデル内の要素の一覧が表示され、追加、削除、元に戻す、およびやり直す操作を行った後でも適切であることに注目してください。

## <a name="see-also"></a>こちらもご覧ください

- [プログラム コードにおけるモデル内の移動およびモデルの更新](../modeling/navigating-and-updating-a-model-in-program-code.md)
- [ドメイン固有言語をカスタマイズするコードの記述](../modeling/writing-code-to-customise-a-domain-specific-language.md)
