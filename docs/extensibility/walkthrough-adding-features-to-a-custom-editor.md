---
title: 'チュートリアル: カスタム エディターに機能を追加する | Microsoft Docs'
description: このチュートリアルを使用してエディターを作成した後に、カスタム エディターに機能を追加する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- editors [Visual Studio SDK], custom - add features
ms.assetid: bfe083b6-3e35-4b9c-ad4f-b30b9ff412a5
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: a19808e76714e0435bd5bb638aea0fbc7eaba929
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105062058"
---
# <a name="walkthrough-add-features-to-a-custom-editor"></a>チュートリアル: カスタム エディターに機能を追加する
カスタム エディターを作成した後に、機能を追加することができます。

## <a name="to-create-an-editor-for-a-vspackage"></a>VSPackage のエディターを作成するには

1. Visual Studio パッケージ プロジェクト テンプレートを使用してカスタム エディターを作成します。

     詳細については、「[チュートリアル: カスタム エディターを作成する](../extensibility/walkthrough-creating-a-custom-editor.md)」を参照してください。

2. エディターで 1 つのビューと複数のビューのどちらをサポートするかを決定します。

     **[新しいウィンドウ]** コマンドをサポートするエディター、またはフォーム ビューとコード ビューがあるエディターには、ドキュメント データ オブジェクトとドキュメント ビュー オブジェクトを別々に用意する必要があります。 1 つのビューのみをサポートするエディターの場合、ドキュメント データ オブジェクトとドキュメント ビュー オブジェクトを同じオブジェクトに実装できます。

     複数のビューの例については、「[複数のドキュメント ビューのサポート](../extensibility/supporting-multiple-document-views.md)」を参照してください。

3. <xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory> インターフェイスを設定して、エディター ファクトリを実装します。

     詳細については、「[エディター ファクトリ](/previous-versions/visualstudio/visual-studio-2015/extensibility/editor-factories?preserve-view=true&view=vs-2015)」を参照してください。

4. エディターで、ドキュメント ビュー オブジェクト ウィンドウを管理するためにインプレース アクティブ化と簡易埋め込みのどちらを使用するかを決定します。

     簡易埋め込みエディター ウィンドウは標準のドキュメント ビューをホストし、インプレース アクティブ化エディター ウィンドウは ActiveX コントロールまたはその他のアクティブ オブジェクトをドキュメント ビューとしてホストします。 詳細については、「[簡易埋め込み](../extensibility/simplified-embedding.md)」と「[インプレース アクティブ化](/previous-versions/visualstudio/visual-studio-2015/misc/in-place-activation?preserve-view=true&view=vs-2015)」を参照してください。

5. コマンドを処理する <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> インターフェイスを実装します。

6. ドキュメントの保持機能と外部ファイルの変更への応答機能を用意します。

    1. ファイルを保持するには、エディターのドキュメント データ オブジェクトに <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData2> と <xref:Microsoft.VisualStudio.Shell.Interop.IPersistFileFormat> を実装します。

    2. 外部ファイルの変更に応答するには、エディターのドキュメント データ オブジェクトに <xref:Microsoft.VisualStudio.Shell.Interop.IVsFileChangeEx> と <xref:Microsoft.VisualStudio.Shell.Interop.IVsDocDataFileChangeControl> を実装します。

        > [!NOTE]
        > <xref:Microsoft.VisualStudio.Shell.Interop.SVsFileChangeEx> に対して `QueryService` を呼び出し、`IVsFileChangeEx` へのポインターを取得します。

7. ソース コード管理を使用してドキュメント編集イベントを調整します。 次の手順に従います。

    1. <xref:Microsoft.VisualStudio.Shell.Interop.SVsQueryEditQuerySave> に対して `QueryService` を呼び出し、`IVsQueryEditQuerySave2` へのポインターを取得します。

    2. 最初の編集イベントが発生したら、<xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QueryEditFiles%2A> メソッドを呼び出します。

         このメソッドは、ファイルがまだチェックアウトされていない場合にファイルをチェックアウトするようにユーザーに促すものです。エラーを回避するために、必ず "ファイルがチェックアウトされていない" 条件を処理してください。

    3. 同様に、ファイルを保存する前に、<xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QuerySaveFile%2A> メソッドを呼び出します。

         このメソッドは、ファイルが保存されていない場合、または最後の保存以降に変更された場合に、ファイルを保存するようにユーザーに促すものです。

8. エディターで選択したテキストのプロパティを表示するには、 **[プロパティ]** ウィンドウを有効にします。 次の手順に従います。

    1. テキストの選択が変更されるたびに <xref:Microsoft.VisualStudio.Shell.Interop.ITrackSelection.OnSelectChange%2A> を呼び出し、<xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer> の実装を渡します。

    2. <xref:Microsoft.VisualStudio.Shell.Interop.STrackSelection> サービスに対して `QueryService` を呼び出し、<xref:Microsoft.VisualStudio.Shell.Interop.ITrackSelection> へのポインターを取得します。

9. ユーザーがエディターと **ツールボックス** の間、または外部エディター (Microsoft Word など) と **ツールボックス** の間で項目をドラッグ アンド ドロップできるようにします。 次の手順に従います。

    1. エディターに `IDropTarget` を実装し、エディターがドロップ ターゲットであることを IDE に警告します。

    2. エディターで **ツールボックス** の項目を有効または無効にできるように、ビューに <xref:Microsoft.VisualStudio.Shell.Interop.IVsToolboxUser> インターフェイスを実装します。

    3. <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.ResetDefaults%2A> を実装し、<xref:Microsoft.VisualStudio.Shell.Interop.SVsToolbox> サービスに対して `QueryService` を呼び出し、<xref:Microsoft.VisualStudio.Shell.Interop.IVsToolbox2> と <xref:Microsoft.VisualStudio.Shell.Interop.IVsToolbox3> のインターフェイスへのポインターを取得します。

         以上の手順で、VSPackage から新しい項目を **ツールボックス** に追加できるようになります。

10. エディターに他のオプション機能が必要かどうかを決定します。

    - エディターで検索と置換のコマンドをサポートする場合は、<xref:Microsoft.VisualStudio.TextManager.Interop.IVsFindTarget> を実装します。

    - エディターでドキュメント アウトライン ツール ウィンドウを使用する場合は、`IVsDocOutlineProvider` を実装します。

    - エディターでステータス バーを使用する場合は、<xref:Microsoft.VisualStudio.Shell.Interop.IVsStatusbarUser> を実装し、<xref:Microsoft.VisualStudio.Shell.Interop.SVsStatusbar> に対して `QueryService` を呼び出し、`IVsStatusBar` へのポインターを取得します。

         たとえば、エディターには、行と列の情報、選択モード (ストリームとボックス)、挿入モード (挿入と上書き) を表示できます。

    - エディターで `Undo` コマンドをサポートする場合は、OLE の元に戻すマネージャー モデルを使用することをお勧めします。 また、エディターで `Undo` コマンドを直接処理する方法もあります。

11. VSPackage、メニュー、エディター、その他の機能の GUID を含むレジストリ情報を作成します。

     エディターを適切に登録する方法を示すために、 *.rgs* ファイル スクリプトに配置するコードの一般的な例を次に示します。

    ```csharp
    NoRemove Editors
    {
          ForceRemove {...guidEditor...} = s 'RTF Editor'
          {
             val Package = s '{...guidVsPackage...}'
             ForceRemove Extensions
             {
                val rtf = d 50
             }
          }
    }
    NoRemove Menus
    {
          val {...guidVsPackage...} = s ',203,11'
    }
    ```

12. 状況依存のヘルプのサポートを実装します。

     この手順を実行すると、エディター内の項目に F1 ヘルプと動的ヘルプ ウィンドウをサポートできるようになります。 詳細については、「[方法: エディターにコンテキストを提供する](/previous-versions/visualstudio/visual-studio-2015/extensibility/how-to-provide-context-for-editors?preserve-view=true&view=vs-2015)」を参照してください。

13. `IDispatch` インターフェイスを実装することで、エディターからオートメーション オブジェクト モデルを公開します。

     詳細については、「 [Contributing to the Automation Model](../extensibility/internals/contributing-to-the-automation-model.md)」を参照してください。

## <a name="robust-programming"></a>信頼性の高いプログラミング

- エディター インスタンスは、IDE から <xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory.CreateEditorInstance%2A> メソッドが呼び出されたときに作成されます。 エディターが複数のビューをサポートしている場合、`CreateEditorInstance` により、ドキュメント データとドキュメント ビューのオブジェクトが両方作成されます。 ドキュメント データ オブジェクトが既に開かれている場合は、null ではない `punkDocDataExisting` 値が `IVsEditorFactory::CreateEditorInstance` に渡されます。 エディター ファクトリの実装の場合、既存のドキュメント データ オブジェクトに適切なインターフェイスのクエリを実行して、互換性があるかどうかを判断する必要があります。 詳細については、「[複数のドキュメント ビューのサポート](../extensibility/supporting-multiple-document-views.md)」を参照してください。

- 簡易埋め込みアプローチを使用する場合は、<xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowPane> インターフェイスを実装します。

- インプレース アクティブ化を使用する場合は、次のインターフェイスを実装します。

   <xref:Microsoft.VisualStudio.OLE.Interop.IOleObject>

   <xref:Microsoft.VisualStudio.OLE.Interop.IOleInPlaceActiveObject>

   <xref:Microsoft.VisualStudio.Shell.Interop.IOleInPlaceComponent>

  > [!NOTE]
  > `IOleInPlaceComponent` インターフェイスは、OLE 2 メニューのマージを回避するために使用されます。

   `IOleCommandTarget` の実装により、**切り取り**、**コピー**、**貼り付け** などのコマンドを処理します。 `IOleCommandTarget` を実装する場合は、独自のコマンド メニュー構造を定義するために独自の *.vsct* ファイルがエディターに必要か、それとも [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] に定義されている標準のコマンドを実装できるかを決定します。 通常、エディターに IDE のメニューを使用して拡張し、独自のツールバーを定義します。 ただし、エディターに IDE の標準のコマンド セットを使用するだけでなく、独自の特定のコマンドを定義する必要があることがよくあります。 エディターにより、使用する標準のコマンドを宣言してから、新しいコマンド、コンテキスト メニュー、トップレベル メニュー、およびツールバーを *.vsct* ファイルで定義する必要があります。 インプレース アクティブ化エディターを作成する場合は、OLE 2 メニューのマージを使用するのではなく、<xref:Microsoft.VisualStudio.Shell.Interop.IOleInPlaceComponent> を実装し、エディターのメニューとツールバーを *.vsct* ファイルで定義します。

- UI でメニュー コマンドが煩雑になるのを防ぐには、新しいコマンドを作成する前に、IDE の既存のコマンドを使用するようにします。 共有コマンドは、*SharedCmdDef.vsct* と *ShellCmdDef.vsct* で定義されています。 これらのファイルは、既定で [!INCLUDE[vsipsdk](../extensibility/includes/vsipsdk_md.md)] インストールの VisualStudioIntegration\Common\Inc サブディレクトリにインストールされています。

- `ISelectionContainer` を使用して、1 つの選択と複数の選択の両方を表すことができます。 選択された各オブジェクトは、`IDispatch` オブジェクトとして実装されます。

- IDE には、<xref:Microsoft.VisualStudio.Shell.Interop.ILocalRegistry2.CreateInstance%2A> からアクセス可能なサービスとして、または <xref:Microsoft.VisualStudio.Shell.Interop.ILocalRegistry2.CreateInstance%2A> を介してインスタンス化できるオブジェクトとして `IOleUndoManager` が実装されています。 このエディターには、`Undo` アクションごとに `IOleUndoUnit` インターフェイスが実装されています。

- カスタム エディターからオートメーション オブジェクトを公開できる場所は 2 つあります。

  - `Document.Object`

  - `Window.Object`

## <a name="see-also"></a>こちらもご覧ください

- [オートメーション モデルへの投稿](../extensibility/internals/contributing-to-the-automation-model.md)