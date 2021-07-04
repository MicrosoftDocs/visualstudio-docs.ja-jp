---
title: Visual Basic でビジュアライザーを記述する | Microsoft Docs
description: チュートリアルに従って、Visual Basic で簡単なビジュアライザーを作成します。 また、ビジュアライザーをテストするテスト ハーネスも作成します。
ms.custom: SEO-VS-2020
ms.date: 05/27/2020
ms.topic: conceptual
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- visualizers, writing
- walkthroughs [Visual Studio], visualizers
ms.assetid: c93bf5a1-3e5e-422f-894e-bd72c9bc1b57
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: b1a4fc7d6f33d1bdfd469ec352674b08dd2495e6
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/19/2021
ms.locfileid: "112385007"
---
# <a name="walkthrough-writing-a-visualizer-in-visual-basic"></a>チュートリアル: Visual Basic でビジュアライザーを記述する

このチュートリアルでは、[!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)] を使用して簡単なビジュアライザーを作成する方法を説明します。 このチュートリアルで作成するビジュアライザーは、Windows フォーム メッセージ ボックスを使用して文字列の内容を表示します。 この単純な文字列のビジュアライザーは基本的な例で、プロジェクトに合わせて他のデータ型向けのビジュアライザーを作成するときに参考になります。

> [!NOTE]
> 使用している設定またはエディションによっては、ヘルプの記載と異なるダイアログ ボックスやメニュー コマンドが表示される場合があります。 設定を変更するには、 **[ツール]** メニューの **[設定のインポートとエクスポート]** をクリックします。 詳細については、「[リセット設定](../ide/environment-settings.md#reset-settings)」を参照してください。

ビジュアライザー コードは、デバッガーによって読み取られる DLL に配置する必要があります。 最初の手順として、DLL のクラス ライブラリ プロジェクトを作成します。

## <a name="create-and-prepare-a-class-library-project"></a>クラス ライブラリ プロジェクトの作成と準備

### <a name="to-create-a-class-library-project"></a>クラス ライブラリ プロジェクトを作成するには

1. 新しいクラス ライブラリ プロジェクトを作成します。

    ::: moniker range=">=vs-2019"
    **Esc** キーを押してスタート ウィンドウを閉じます。 **Ctrl + Q** キーを押して検索ボックスを開き、「**visual basic**」と入力し、 **[テンプレート]** を選択して、 **[Create a new Class Library (.NET Framework)]\(新しいクラス ライブラリの作成 (.NET Framework)\)** を選択します。 表示されたダイアログ ボックスで、 **[作成]** を選択します。
    ::: moniker-end
    ::: moniker range="vs-2017"
    上部のメニュー バーから、 **[ファイル]**  >  **[新規作成]**  >  **[プロジェクト]** の順に選択します。 **[新しいプロジェクト]** ダイアログ ボックスの左側のウィンドウで、 **[Visual Basic]** の下にある **[.NET Standard]** を選択し、次に真ん中のウィンドウで **[クラス ライブラリ (.NET Standard)]** を選択します。
    ::: moniker-end

2. クラス ライブラリの適切な名前 (`MyFirstVisualizer` など) を入力し、 **[作成]** または **[OK]** をクリックします。

   クラス ライブラリを作成したら、Microsoft.VisualStudio.DebuggerVisualizers.DLL への参照を追加することによって、この DLL で定義されているクラスを使用できるようにします。 ただし、最初にプロジェクトにわかりやすい名前を付けます。

### <a name="to-rename-class1vb-and-add-microsoftvisualstudiodebuggervisualizers"></a>Class1.vb の名前を変更して Microsoft.VisualStudio.DebuggerVisualizers に追加するには

1. **ソリューション エクスプローラー** で **Class1.vb** を右クリックし、ショートカット メニューの **[名前の変更]** をクリックします。

2. Class1.vb の名前を、DebuggerSide.vb などのわかりやすい名前に変更します。

   > [!NOTE]
   > [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] によって、新しいファイル名に合わせて DebuggerSide.vb のクラス宣言が自動的に変更されます。

3. **ソリューション エクスプローラー** で、 **[My First Visualizer]** を右クリックし、ショートカット メニューの **[参照の追加]** をクリックします。

4. **[参照の追加]** ダイアログ ボックスの **[参照]** タブで **[参照]** を選択し、Microsoft.VisualStudio.DebuggerVisualizers.DLL を探します。

    この DLL は、Visual Studio のインストール ディレクトリの *\<Visual Studio Install Directory>\Common7\IDE\PublicAssemblies* サブディレクトリにあります。

5. **[OK]** をクリックします。

6. DebuggerSide.vb の `Imports` ステートメントに次のステートメントを追加します。

   ```vb
   Imports Microsoft.VisualStudio.DebuggerVisualizers
   ```

## <a name="add-the-debugger-side-code"></a>デバッガー側のコードの追加
 これで、デバッガー側のコードを作成する準備が整いました。 これは、視覚化を要する情報を表示するためにデバッガー内で実行されるコードです。 最初に、`DebuggerSide` オブジェクトの宣言を変更して、`DialogDebuggerVisualizer` 基底クラスを継承するようにする必要があります。

### <a name="to-inherit-from-dialogdebuggervisualizer"></a>DialogDebuggerVisualizer から継承するには

1. DebuggerSide.vb で、次のコード行に移動します。

   ```vb
   Public Class DebuggerSide
   ```

2. 次のようにコードを編集します。

   ```vb
   Public Class DebuggerSide
   Inherits DialogDebuggerVisualizer
   ```

   `DialogDebuggerVisualizer` には、オーバーライドする必要がある抽象メソッドが 1 つ (`Show`) あります。

### <a name="to-override-the-dialogdebuggervisualizershow-method"></a>DialogDebuggerVisualizer.Show メソッドをオーバーライドするには

- `public class DebuggerSide` に、次のメソッドを追加します。

  ```vb
  Protected Overrides Sub Show(ByVal windowService As Microsoft.VisualStudio.DebuggerVisualizers.IDialogVisualizerService, ByVal objectProvider As Microsoft.VisualStudio.DebuggerVisualizers.IVisualizerObjectProvider)

      End Sub
  ```

  `Show` メソッドには、ビジュアライザーのダイアログ ボックス、または他のユーザー インターフェイスを実際に作成し、デバッガーからビジュアライザーに渡された情報を表示するコードを記述します。 したがって、このダイアログ ボックスを作成し、情報を表示するコードを追加する必要があります。 このチュートリアルでは、Windows フォーム メッセージ ボックスを使用します。 最初に、`Imports` の参照と <xref:System.Windows.Forms> ステートメントを追加する必要があります。

### <a name="to-add-systemwindowsforms"></a>System.Windows.Forms を追加するには

1. **ソリューション エクスプローラー** で、 **[参照]** を右クリックし、ショートカット メニューの **[参照の追加]** をクリックします。

2. **[参照の追加]** ダイアログ ボックスの **[参照]** タブで **[参照]** System.Windows.Forms.DLL を探します。

    この DLL は、*C:\Windows\Microsoft.NET\Framework\v4.0.30319* で見つけることができます。

3. **[OK]** をクリックします。

4. DebuggerSide.cs の `Imports` ステートメントに次のステートメントを追加します。

    ```vb
    Imports System.Windows.Forms
    ```

## <a name="create-your-visualizers-user-interface"></a>ビジュアライザーのユーザー インターフェイスの作成
 次に、ビジュアライザーのユーザー インターフェイスを作成および表示するためのコードを追加します。 初めて作成するビジュアライザーであるため、ユーザー インターフェイスを簡素にし、メッセージ ボックスを使用します。

### <a name="to-show-the-visualizer-output-in-a-dialog-box"></a>ビジュアライザーの出力をダイアログ ボックスに表示するには

1. `Show` メソッドに次のコード行を追加します。

    ```vb
    MessageBox.Show(objectProvider.GetObject().ToString())
    ```

     このコード例には、エラー処理が含まれていません。 実際に使用するビジュアライザーなど、どのようなアプリケーションにも、エラー処理を追加する必要があります。

2. **[ビルド]** メニューの **[MyFirstVisualizer のビルド]** をクリックします。 プロジェクトが構築されます。 ビルド エラーを修正してから次の作業に進みます。

## <a name="add-the-necessary-attribute"></a>必要な属性の追加
 これで、デバッガー側のコードは終わりです。 ただし、もう 1 つ追加するものがあります。それは、ビジュアライザーを構成しているクラスのコレクションをデバッグ対象側に通知する属性です。

### <a name="to-add-the-type-to-visualize-for-the-debuggee-side-code"></a>デバッグ対象側のコードで視覚化する型を追加するには

デバッガー側のコードで <xref:System.Diagnostics.DebuggerVisualizerAttribute> 属性を使用して、視覚化する型 (オブジェクト ソース) を指定します。 `Target` プロパティに視覚化する型が設定されます。

1. DebuggerSide.vb の `Imports` ステートメントと `namespace MyFirstVisualizer` の間に次の属性コードを追加します。

    ```vb
    <Assembly: System.Diagnostics.DebuggerVisualizer(GetType(MyFirstVisualizer.DebuggerSide), GetType(VisualizerObjectSource), Target:=GetType(System.String), Description:="My First Visualizer")>
    ```

2. **[ビルド]** メニューの **[MyFirstVisualizer のビルド]** をクリックします。 プロジェクトが構築されます。 ビルド エラーを修正してから次の作業に進みます。

## <a name="create-a-test-harness"></a>テスト ハーネスの作成
 これで、最初のビジュアライザーが完成しました。 手順どおりに作業を行ってきた場合は、ビジュアライザーを構築し、[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] にインストールできます。 ただし、ビジュアライザーを [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] にインストールする前にテストを行い、ビジュアライザーが正しく動作することを確認する必要があります。 そこで、[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] にインストールしないでビジュアライザーを実行する、テスト ハーネスを作成します。

### <a name="to-add-a-test-method-to-show-the-visualizer"></a>ビジュアライザーを表示するテスト メソッドを追加するには

1. 次のメソッドを `public DebuggerSide` クラスに追加します。

   ```vb
   Shared Public Sub TestShowVisualizer(ByVal objectToVisualize As Object)
       Dim visualizerHost As New VisualizerDevelopmentHost(objectToVisualize, GetType(DebuggerSide))
   visualizerHost.ShowVisualizer()
   End Sub
   ```

2. **[ビルド]** メニューの **[MyFirstVisualizer のビルド]** をクリックします。 プロジェクトが構築されます。 ビルド エラーを修正してから次の作業に進みます。

   次に、ビジュアライザー DLL を呼び出す実行可能プロジェクトを作成する必要があります。 簡易にするために、コンソール アプリケーション プロジェクトを使用します。

### <a name="to-add-a-console-application-project-to-the-solution"></a>ソリューションにコンソール アプリケーション プロジェクトを追加するには

1. ソリューション エクスプローラーでソリューションを右クリックして **[追加]** を選択し、 **[新しいプロジェクト]** をクリックします。

    ::: moniker range=">=vs-2019"
    検索ボックスに「**visual basic**」と入力し、 **[テンプレート]** を選択して、 **[Create a new Console App (.NET Framework)]\(新しいコンソール アプリの作成 (.NET Framework)\)** を選択します。 表示されたダイアログ ボックスで、 **[作成]** を選択します。
    ::: moniker-end
    ::: moniker range="vs-2017"
    上部のメニュー バーから、 **[ファイル]**  >  **[新規作成]**  >  **[プロジェクト]** の順に選択します。 **[新しいプロジェクト]** ダイアログ ボックスの左側のウィンドウで、 **[Visual Basic]** の下にある **[Windows デスクトップ]** を選択し、次に真ん中のウィンドウで **[コンソール アプリ (.NET Framework)]** を選択します。
    ::: moniker-end

2. クラス ライブラリの適切な名前 (`MyTestConsole` など) を入力し、 **[作成]** または **[OK]** をクリックします。

   次に、必要な参照を追加して、MyTestConsole が MyFirstVisualizer を呼び出すことができるようにします。

### <a name="to-add-necessary-references-to-mytestconsole"></a>必要な参照を MyTestConsole に追加するには

1. **ソリューション エクスプローラー** で、**MyTestConsole** を右クリックし、ショートカット メニューの **[参照の追加]** をクリックします。

2. **[参照の追加]** ダイアログ ボックスの **[参照]** タブで、Microsoft.VisualStudio.DebuggerVisualizers をクリックします。

3. **[OK]** をクリックします。

4. **MyTestConsole** を右クリックし、再度 **[参照の追加]** をクリックします。

5. **[参照の追加]** ダイアログ ボックスの **[プロジェクト]** タブをクリックし、MyFirstVisualizer をクリックします。

6. **[OK]** をクリックします。

## <a name="finish-your-test-harness-and-test-your-visualizer"></a>テスト ハーネスの終了とビジュアライザーのテスト
 次に、コードを追加してテスト ハーネスを完成させます。

### <a name="to-add-code-to-mytestconsole"></a>コードを MyTestConsole に追加するには

1. **ソリューション エクスプローラー** で **Program.vb** を右クリックし、ショートカット メニューの **[名前の変更]** をクリックします。

2. Module1.vb の名前を、**TestConsole.vb** などの適切な名前に変更します。

    [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] によって、新しいファイル名に合わせて TestConsole.vb のクラス宣言が自動的に変更されることに注意してください。

3. TestConsole. vb で、次の `Imports` ステートメントを追加します。

   ```vb
   Imports MyFirstVisualizer
   ```

4. `Main` メソッドに、次のコードを追加します。

   ```vb
   Dim myString As String = "Hello, World"
   DebuggerSide.TestShowVisualizer(myString)
   ```

   これで、作成したビジュアライザーをテストする準備が整いました。

### <a name="to-test-the-visualizer"></a>ビジュアライザーをテストするには

1. **ソリューション エクスプローラー** で **MyTestConsole** を右クリックし、ショートカット メニューの **[スタートアップ プロジェクトに設定]** をクリックします。

2. **[デバッグ]** メニューの **[開始]** をクリックします。

    コンソール アプリケーションが起動します。 ビジュアライザーが表示され、「Hello, World」という文字列が表示されます。

   テストは成功です。 これで、最初のビジュアライザーの作成とテストが完了しました。

   作成したビジュアライザーをテスト ハーネスから呼び出すのではなく、[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] で使用する場合は、ビジュアライザーをインストールする必要があります。 詳細については、[ビジュアライザーをインストールする](../debugger/how-to-install-a-visualizer.md)」を参照してください。

## <a name="see-also"></a>関連項目

- [ビジュアライザーのアーキテクチャ](../debugger/visualizer-architecture.md)
- [方法: ビジュアライザーをインストールする](../debugger/how-to-install-a-visualizer.md)
- [カスタム ビジュアライザーを作成する](../debugger/create-custom-visualizers-of-data.md)