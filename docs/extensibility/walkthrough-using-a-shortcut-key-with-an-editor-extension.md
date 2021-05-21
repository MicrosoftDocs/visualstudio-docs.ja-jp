---
title: エディター拡張機能でショートカット キーを使用する
description: ショートカット キーを使用して、ビューの修飾をテキスト ビューに追加する方法について説明します。 このチュートリアルは、ビューポート修飾エディター テンプレートに基づいています。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- editors [Visual Studio SDK], new - link keystrokes to commands
ms.assetid: cf6cc6c6-5a65-4f90-8f14-663decf74672
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: c2d49fa9e858d65529e466f6ed960835ab8c2324
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105061954"
---
# <a name="walkthrough-use-a-shortcut-key-with-an-editor-extension"></a>チュートリアル: エディター拡張機能でショートカット キーを使用する
エディター拡張機能でショートカット キーに応答することができます。 次のチュートリアルでは、ショートカット キーを使用してテキスト ビューにビュー修飾を追加する方法について説明します。 このチュートリアルは、ビューポート修飾エディター テンプレートに基づいており、+ 文字を使用して修飾を追加できます。

## <a name="prerequisites"></a>前提条件
 Visual Studio 2015 以降では、ダウンロード センターから Visual Studio SDK をインストールしません。 これは、Visual Studio セットアップにオプション機能として含まれています。 VS SDK は、後でインストールすることもできます。 詳細については、「[Visual Studio SDK のインストール](../extensibility/installing-the-visual-studio-sdk.md)」を参照してください。

## <a name="create-a-managed-extensibility-framework-mef-project"></a>Managed Extensibility Framework (MEF) プロジェクトを作成する

1. C# VSIX プロジェクトを作成します。 ( **[新しいプロジェクト]** ダイアログで、 **[Visual C#]、[拡張機能]** 、 **[VSIX プロジェクト]** の順に選択します)。ソリューションに `KeyBindingTest` という名前を付けます。

2. Editor Text Adornment 項目テンプレートをプロジェクトに追加し、`KeyBindingTest` という名前を付けます。 詳細については、「[エディター項目テンプレートを使用して拡張機能を作成する](../extensibility/creating-an-extension-with-an-editor-item-template.md)」を参照してください。

3. 次の参照を追加し、**CopyLocal** を `false` に設定します。

    Microsoft.VisualStudio.Editor

    Microsoft.VisualStudio.OLE.Interop

    Microsoft.VisualStudio.Shell.14.0

    Microsoft.VisualStudio.TextManager.Interop

   KeyBindingTest クラス ファイルで、クラス名を PurpleCornerBox に変更します。 左余白に表示される電球を使用して、その他の適切な変更を行います。 コンストラクター内で、修飾レイヤーの名前を **KeyBindingTest** から **PurpleCornerBox** に変更します。

```csharp
this.layer = view.GetAdornmentLayer("PurpleCornerBox");
```

KeyBindingTestTextViewCreationListener.cs クラス ファイルで、AdornmentLayer の名前を **KeyBindingTest** から **PurpleCornerBox** に変更します。

```csharp
[Export(typeof(AdornmentLayerDefinition))]
[Name("PurpleCornerBox")]
[Order(After = PredefinedAdornmentLayers.Selection, Before = PredefinedAdornmentLayers.Text)]
public AdornmentLayerDefinition editorAdornmentLayer;
```

## <a name="handle-typechar-command"></a>TYPECHAR コマンドを処理する
Visual Studio 2017 バージョン 15.6 より前では、エディター拡張機能でコマンドを処理する唯一の方法は、<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> ベースのコマンド フィルターを実装することでした。 Visual Studio 2017 バージョン 15.6 では、エディター コマンド ハンドラーに基づく最新の簡略化されたアプローチが導入されました。 次の 2 つのセクションでは、従来のアプローチと最新のアプローチの両方を使用してコマンドを処理する方法について説明します。

## <a name="define-the-command-filter-prior-to-visual-studio-2017-version-156"></a>コマンド フィルターを定義する (Visual Studio 2017 バージョン 15.6 より前)

 コマンド フィルターは、修飾をインスタンス化することによってコマンドを処理する <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> の実装です。

1. クラス ファイルを追加し、その名前を `KeyBindingCommandFilter`にします。

2. ディレクティブを使用して以下を追加します。

    ```csharp
    using System;
    using System.Runtime.InteropServices;
    using Microsoft.VisualStudio.OLE.Interop;
    using Microsoft.VisualStudio;
    using Microsoft.VisualStudio.Text.Editor;

    ```

3. KeyBindingCommandFilter という名前のクラスは、<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> から継承する必要があります。

    ```csharp
    internal class KeyBindingCommandFilter : IOleCommandTarget
    ```

4. テキスト ビュー、コマンド チェーンの次のコマンド、およびコマンド フィルターが既に追加されているかどうかを表すフラグの非公開フィールドを追加します。

    ```csharp
    private IWpfTextView m_textView;
    internal IOleCommandTarget m_nextTarget;
    internal bool m_added;
    internal bool m_adorned;
    ```

5. テキスト ビューを設定するコンストラクターを追加します。

    ```csharp
    public KeyBindingCommandFilter(IWpfTextView textView)
    {
        m_textView = textView;
        m_adorned = false;
    }
    ```

6. `QueryStatus()` メソッドを次のように実装します。

    ```csharp
    int IOleCommandTarget.QueryStatus(ref Guid pguidCmdGroup, uint cCmds, OLECMD[] prgCmds, IntPtr pCmdText)
    {
        return m_nextTarget.QueryStatus(ref pguidCmdGroup, cCmds, prgCmds, pCmdText);
    }
    ```

7. プラス記号 ( **+** ) 文字が入力された場合にビューに紫色のボックスが追加されるように `Exec()` メソッドを実装します。

    ```csharp
    int IOleCommandTarget.Exec(ref Guid pguidCmdGroup, uint nCmdID, uint nCmdexecopt, IntPtr pvaIn, IntPtr pvaOut)
    {
        if (m_adorned == false)
        {
            char typedChar = char.MinValue;

            if (pguidCmdGroup == VSConstants.VSStd2K && nCmdID == (uint)VSConstants.VSStd2KCmdID.TYPECHAR)
            {
                typedChar = (char)(ushort)Marshal.GetObjectForNativeVariant(pvaIn);
                if (typedChar.Equals('+'))
                {
                    new PurpleCornerBox(m_textView);
                    m_adorned = true;
                }
            }
        }
        return m_nextTarget.Exec(ref pguidCmdGroup, nCmdID, nCmdexecopt, pvaIn, pvaOut);
    }

    ```

## <a name="add-the-command-filter-prior-to-visual-studio-2017-version-156"></a>コマンド フィルターを追加する (Visual Studio 2017 バージョン 15.6 より前)
 修飾プロバイダーにより、テキスト ビューにコマンド フィルターを追加する必要があります。 この例では、テキスト ビューの作成イベントをリッスンする <xref:Microsoft.VisualStudio.Editor.IVsTextViewCreationListener> をプロバイダーに実装しています。 また、この修飾プロバイダーから、修飾の Z オーダーを定義する修飾レイヤーもエクスポートされます。

1. KeyBindingTestTextViewCreationListener ファイルに、次の using ディレクティブを追加します。

    ```csharp
    using System;
    using System.Collections.Generic;
    using System.ComponentModel.Composition;
    using Microsoft.VisualStudio;
    using Microsoft.VisualStudio.OLE.Interop;
    using Microsoft.VisualStudio.Utilities;
    using Microsoft.VisualStudio.Editor;
    using Microsoft.VisualStudio.Text.Editor;
    using Microsoft.VisualStudio.TextManager.Interop;

    ```

2. テキスト ビュー アダプターを取得するには、<xref:Microsoft.VisualStudio.Editor.IVsEditorAdaptersFactoryService> をインポートする必要があります。

    ```csharp
    [Import(typeof(IVsEditorAdaptersFactoryService))]
    internal IVsEditorAdaptersFactoryService editorFactory = null;

    ```

3. `KeyBindingCommandFilter` を追加するように <xref:Microsoft.VisualStudio.Text.Editor.IWpfTextViewCreationListener.TextViewCreated%2A> メソッドを変更します。

    ```csharp
    public void TextViewCreated(IWpfTextView textView)
    {
        AddCommandFilter(textView, new KeyBindingCommandFilter(textView));
    }
    ```

4. `AddCommandFilter` ハンドラーにより、テキスト ビュー アダプターが取得され、コマンド フィルターが追加されます。

    ```csharp
    void AddCommandFilter(IWpfTextView textView, KeyBindingCommandFilter commandFilter)
    {
        if (commandFilter.m_added == false)
        {
            //get the view adapter from the editor factory
            IOleCommandTarget next;
            IVsTextView view = editorFactory.GetViewAdapter(textView);

            int hr = view.AddCommandFilter(commandFilter, out next);

            if (hr == VSConstants.S_OK)
            {
                commandFilter.m_added = true;
                 //you'll need the next target for Exec and QueryStatus
                if (next != null)
                commandFilter.m_nextTarget = next;
            }
        }
    }
    ```

## <a name="implement-a-command-handler-starting-in-visual-studio-2017-version-156"></a>コマンド ハンドラーを実装する (Visual Studio 2017 バージョン 15.6 以降)

まず、最新のエディター API を参照するようにプロジェクトの Nuget 参照を更新します。

1. プロジェクトを右クリックし、 **[NuGet パッケージの管理]** を選択します。

2. **Nuget パッケージ マネージャー** で、 **[更新]** タブを選択し、 **[すべてのパッケージを選択]** チェックボックスをオンにしてから、 **[更新]** を選択します。

コマンド ハンドラーは、修飾をインスタンス化することによってコマンドを処理する <xref:Microsoft.VisualStudio.Commanding.ICommandHandler%601> の実装です。

1. クラス ファイルを追加し、その名前を `KeyBindingCommandHandler`にします。

2. ディレクティブを使用して以下を追加します。

   ```csharp
   using Microsoft.VisualStudio.Commanding;
   using Microsoft.VisualStudio.Text.Editor;
   using Microsoft.VisualStudio.Text.Editor.Commanding.Commands;
   using Microsoft.VisualStudio.Utilities;
   using System.ComponentModel.Composition;
   ```

3. KeyBindingCommandHandler という名前のクラスにより、`ICommandHandler<TypeCharCommandArgs>` から継承し、<xref:Microsoft.VisualStudio.Commanding.ICommandHandler> としてエクスポートする必要があります。

   ```csharp
   [Export(typeof(ICommandHandler))]
   [ContentType("text")]
   [Name("KeyBindingTest")]
   internal class KeyBindingCommandHandler : ICommandHandler<TypeCharCommandArgs>
   ```

4. コマンド ハンドラーの表示名を追加します。

   ```csharp
   public string DisplayName => "KeyBindingTest";
   ```

5. `GetCommandState()` メソッドを次のように実装します。 このコマンド ハンドラーにより、コア エディターの TYPECHAR コマンドが処理されるため、コマンドの有効化をコア エディターに委任できます。

   ```csharp
   public CommandState GetCommandState(TypeCharCommandArgs args)
   {
       return CommandState.Unspecified;
   }
   ```

6. プラス記号 ( **+** ) 文字が入力された場合にビューに紫色のボックスが追加されるように `ExecuteCommand()` メソッドを実装します。

   ```csharp
   public bool ExecuteCommand(TypeCharCommandArgs args, CommandExecutionContext executionContext)
   {
       if (args.TypedChar == '+')
       {
           bool alreadyAdorned = args.TextView.Properties.TryGetProperty(
               "KeyBindingTextAdorned", out bool adorned) && adorned;
           if (!alreadyAdorned)
           {
               new PurpleCornerBox((IWpfTextView)args.TextView);
               args.TextView.Properties.AddProperty("KeyBindingTextAdorned", true);
           }
       }

       return false;
   }
   ```

   7. 修飾レイヤーの定義を *KeyBindingTestTextViewCreationListener.cs* ファイルから *KeyBindingCommandHandler.cs* にコピーしてから、*KeyBindingTestTextViewCreationListener.cs* ファイルを削除します。

   ```csharp
   /// <summary>
   /// Defines the adornment layer for the adornment. This layer is ordered
   /// after the selection layer in the Z-order.
   /// </summary>
   [Export(typeof(AdornmentLayerDefinition))]
   [Name("PurpleCornerBox")]
   [Order(After = PredefinedAdornmentLayers.Selection, Before = PredefinedAdornmentLayers.Text)]
   private AdornmentLayerDefinition editorAdornmentLayer;
   ```

## <a name="make-the-adornment-appear-on-every-line"></a>すべての行に修飾を表示する

元の修飾は、テキスト ファイルのすべての文字 "a" に表示されていました。 **+** 文字に応答して修飾を追加するようにコードを変更したので、 **+** 文字が入力された行にのみ修飾が追加されます。 すべての "a" に修飾がもう一度表示されるように修飾コードを変更することができます。

*KeyBindingTest.cs* ファイルで、ビュー内のすべての行を反復処理し、"a" 文字を修飾するように `CreateVisuals()` メソッドを変更します。

```csharp
private void CreateVisuals(ITextViewLine line)
{
    IWpfTextViewLineCollection textViewLines = this.view.TextViewLines;

    foreach (ITextViewLine textViewLine in textViewLines)
    {
        if (textViewLine.ToString().Contains("a"))
        {
            // Loop through each character, and place a box around any 'a'
            for (int charIndex = textViewLine.Start; charIndex < textViewLine.End; charIndex++)
            {
                if (this.view.TextSnapshot[charIndex] == 'a')
                {
                    SnapshotSpan span = new SnapshotSpan(this.view.TextSnapshot, Span.FromBounds(charIndex, charIndex + 1));
                    Geometry geometry = textViewLines.GetMarkerGeometry(span);
                    if (geometry != null)
                    {
                        var drawing = new GeometryDrawing(this.brush, this.pen, geometry);
                        drawing.Freeze();

                        var drawingImage = new DrawingImage(drawing);
                        drawingImage.Freeze();

                        var image = new Image
                        {
                            Source = drawingImage,
                        };

                        // Align the image with the top of the bounds of the text geometry
                        Canvas.SetLeft(image, geometry.Bounds.Left);
                        Canvas.SetTop(image, geometry.Bounds.Top);

                        this.layer.AddAdornment(AdornmentPositioningBehavior.TextRelative, span, null, image, null);
                    }
                }
            }
        }
    }
}
```

## <a name="build-and-test-the-code"></a>コードのビルドとテスト

1. KeyBindingTest ソリューションをビルドし、実験用インスタンスで実行します。

2. テキスト ファイルを作成するか、開きます。 文字 "a" を含む単語をいくつか入力してから、テキスト ビューの任意の場所に **+** と入力します。

     ファイル内のすべての "a" 文字に紫色の四角形が表示されます。
