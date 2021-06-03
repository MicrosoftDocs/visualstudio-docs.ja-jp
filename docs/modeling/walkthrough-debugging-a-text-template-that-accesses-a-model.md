---
title: 'チュートリアル: モデルにアクセスするテキスト テンプレートのデバッグ'
description: モデルにアクセスするテキスト テンプレートをデバッグする方法について説明します。
ms.date: 11/04/2016
ms.topic: how-to
author: JoshuaPartlow
ms.author: joshuapa
manager: jmartens
ms.custom: SEO-VS-2020
ms.workload:
- multiple
ms.openlocfilehash: 394fe7b1a368d3d4c6a47fd4350ac6644112aa57
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99924111"
---
# <a name="walkthrough-debugging-a-text-template-that-accesses-a-model"></a>チュートリアル: モデルにアクセスするテキスト テンプレートのデバッグ
ドメイン固有言語ソリューションでテキスト テンプレートを変更または追加すると、エンジンがテンプレートをソース コードに変換したとき、または生成されたコードをコンパイルしたときに、エラーが発生することがあります。 次のチュートリアルでは、テキスト テンプレートをデバッグするために実行できるいくつかの操作について説明します。

> [!NOTE]
> 一般的なテキスト テンプレートの詳細については、「[コード生成と T4 テキスト テンプレート](../modeling/code-generation-and-t4-text-templates.md)」を参照してください。 テキスト テンプレートのデバッグの詳細については、「[チュートリアル: テキスト テンプレートのデバッグ](debugging-a-t4-text-template.md)」を参照してください。

## <a name="creating-a-domain-specific-language-solution"></a>ドメイン固有言語ソリューションの作成
 この手順では、次の特性を持つドメイン固有言語ソリューションを作成します。

- 名前: DebuggingTestLanguage

- ソリューション テンプレート: 最小言語

- ファイル拡張子: .ddd

- 会社名: Fabrikam

  ドメイン固有言語ソリューションの作成の詳細については、「[方法: ドメイン固有言語ソリューションを作成する](../modeling/how-to-create-a-domain-specific-language-solution.md)」を参照してください。

## <a name="creating-a-text-template"></a>テキスト テンプレートの作成
 ソリューションにテキスト テンプレートを追加します。

#### <a name="to-create-a-text-template"></a>テキスト テンプレートを作成するには

1. ソリューションをビルドし、デバッガーで実行を開始します ( **[ビルド]** メニューの **[ソリューションのリビルド]** をクリックし、 **[デバッグ]** メニューの **[デバッグの開始]** をクリックします)。Visual Studio の新しいインスタンスでデバッグ プロジェクトが開きます。

2. `DebugTest.tt` という名前のテキスト ファイルをデバッグ プロジェクトに追加します。

3. DebugTest.tt の **[カスタム ツール]** プロパティが `TextTemplatingFileGenerator` に設定されていることを確認します。

## <a name="debugging-directives-that-access-a-model-from-a-text-template"></a>テキスト テンプレートからモデルにアクセスするディレクティブのデバッグ
 テキスト テンプレート内のステートメントと式からモデルにアクセスするには、最初に生成されたディレクティブ プロセッサを呼び出す必要があります。 生成されたディレクティブ プロセッサを呼び出すと、モデル内のクラスがプロパティとしてテキスト テンプレート コードで使用できるようになります。 詳細については、「[テキスト テンプレートからモデルへのアクセス](../modeling/accessing-models-from-text-templates.md)」を参照してください。

 次の手順では、不適切なディレクティブ名とプロパティ名をデバッグします。

#### <a name="to-debug-an-incorrect-directive-name"></a>不適切なディレクティブ名をデバッグするには

1. DebugTest.tt 内のコードを次のコードに置き換えます。

    > [!NOTE]
    > コードにはエラーが含まれています。 デバッグするためにエラーを取り込んでいます。

    ```csharp
    <#@ template language="C#" inherits="Microsoft.VisualStudio.TextTemplating.VSHost.ModelingTextTransformation"#>
    <#@ output extension=".txt" #>
    <#@ modelRoot processor="DebuggingTestLanguageDirectiveProcessor" requires="fileName='Sample.ddd'" provides="ExampleModel=ExampleModel" #>

    Model: <#= this.ExampleModel #>
    <#
    foreach (ExampleElement element in this.ExampleModel.Elements)
    {
    #>
        Element: <#= element.Name #>
    <#
    }
    #>
    ```

    ```vb
    <#@ template language="VB" inherits="Microsoft.VisualStudio.TextTemplating.VSHost.ModelingTextTransformation"#>
    <#@ output extension=".txt" #>
    <#@ modelRoot processor="DebuggingTestLanguageDirectiveProcessor" requires="fileName='Sample.ddd'" provides="ExampleModel=ExampleModel" #>

    Model: <#= Me.ExampleModel #>
    <#
    For Each element as ExampleElement in Me.ExampleModel.Elements
    #>
        Element: <#= element.Name #>
    <#
    Next
    #>
    ```

2. **ソリューション エクスプローラー** で、DebugTest.tt を右クリックし、 **[カスタム ツールの実行]** をクリックします。

     **[エラー一覧]** ウィンドウに次のエラーが表示されます。

     **プロセッサ 'DebuggingTestLanguageDirectiveProcessor' はディレクティブ 'modelRoot' をサポートしません。変換は実行されません。**

     この場合、ディレクティブ呼び出しに無効なディレクティブ名が含まれています。 ディレクティブ名として `modelRoot` を指定しましたが、正しいディレクティブ名は `DebuggingTestLanguage` です。

3. **[エラー一覧]** ウィンドウでエラーをダブルクリックすると、そのコードに移動します。

4. コードを修正するには、ディレクティブ名を `DebuggingTestLanguage` に変更します。

     変更が強調表示されます。

    ```csharp
    <#@ DebuggingTestLanguage processor="DebuggingTestLanguageDirectiveProcessor" requires="fileName='Sample.ddd'" provides="ExampleModel=ExampleModel" #>
    ```

    ```vb
    <#@ DebuggingTestLanguage processor="DebuggingTestLanguageDirectiveProcessor" requires="fileName='Sample.ddd'" provides="ExampleModel=ExampleModel" #>
    ```

5. **ソリューション エクスプローラー** で、DebugTest.tt を右クリックし、 **[カスタム ツールの実行]** をクリックします。

     これで、システムによってテキスト テンプレートが変換され、対応する出力ファイルが生成されます。 **[エラー一覧]** ウィンドウにエラーは表示されません。

#### <a name="to-debug-an-incorrect-property-name"></a>不適切なプロパティ名をデバッグするには

1. DebugTest.tt 内のコードを次のコードに置き換えます。

    > [!NOTE]
    > コードにはエラーが含まれています。 デバッグするためにエラーを取り込んでいます。

    ```csharp
    <#@ template language="C#" inherits="Microsoft.VisualStudio.TextTemplating.VSHost.ModelingTextTransformation"#>
    <#@ output extension=".txt" #>
    <#@ DebuggingTestLanguage processor="DebuggingTestLanguageDirectiveProcessor" requires="fileName='Sample.ddd'" provides="ExampleModel=LibraryModel" #>

    Model: <#= this.ExampleModel #>
    <#
    foreach (ExampleElement element in this.ExampleModel.Elements)
    {
    #>
        Element: <#= element.Name #>
    <#
    }
    #>
    ```

    ```vb
    <#@ template language="VB" inherits="Microsoft.VisualStudio.TextTemplating.VSHost.ModelingTextTransformation"#>
    <#@ output extension=".txt" #>
    <#@ DebuggingTestLanguage processor="DebuggingTestLanguageDirectiveProcessor" requires="fileName='Sample.ddd'" provides="ExampleModel=LibraryModel" #>

    Model: <#= Me.ExampleModel #>
    <#
    For Each element as ExampleElement in Me.ExampleModel.Elements
    #>
        Element: <#= element.Name #>
    <#
    Next
    #>
    ```

2. **ソリューション エクスプローラー** で、DebugTest.tt を右クリックし、 **[カスタム ツールの実行]** をクリックします。

     **[エラー一覧]** ウィンドウに、次のいずれかのエラーが表示されます。

     (C#)

     **変換をコンパイルしています: Microsoft.VisualStudio.TextTemplating\<GUID>. GeneratedTextTransformation' に 'ExampleModel' の定義がありません**

     (Visual Basic)

     **変換をコンパイルしています: 'ExampleModel' は 'Microsoft.VisualStudio.TextTemplating\<GUID>.GeneratedTextTransformation' のメンバーではありません。**

     この場合、テキスト テンプレート コードに無効なプロパティ名が含まれています。 プロパティ名として `ExampleModel` が指定されていますが、正しいプロパティ名は `LibraryModel` です。 次のコードに示すように、provides パラメーターで正しいプロパティ名を見つけることができます。

    ```
    <#@ DebuggingTestLanguage processor="DebuggingTestLanguageDirectiveProcessor" requires="fileName='Sample.ddd'" provides="ExampleModel=LibraryModel" #>
    ```

3. [エラー一覧] ウィンドウでエラーをダブルクリックすると、そのコードに移動します。

4. コードを修正するには、テキスト テンプレート コードでプロパティ名を `LibraryModel` に変更します。

     変更が強調表示されます。

    ```csharp
    <#@ template language="C#" inherits="Microsoft.VisualStudio.TextTemplating.VSHost.ModelingTextTransformation"#>
    <#@ output extension=".txt" #>
    <#@ DebuggingTestLanguage processor="DebuggingTestLanguageDirectiveProcessor" requires="fileName='Sample.ddd'" provides="ExampleModel=LibraryModel" #>

    Model: <#= this.LibraryModel #>
    <#
    foreach (ExampleElement element in this.LibraryModel.Elements)
    {
    #>
        Element: <#= element.Name #>
    <#
    }
    #>
    ```

    ```vb
    <#@ template language="VB" inherits="Microsoft.VisualStudio.TextTemplating.VSHost.ModelingTextTransformation"#>
    <#@ output extension=".txt" #>
    <#@ DebuggingTestLanguage processor="DebuggingTestLanguageDirectiveProcessor" requires="fileName='Sample.ddd'" provides="ExampleModel=LibraryModel" #>

    Model: <#= Me.LibraryModel #>
    <#
    For Each element as ExampleElement in Me.LibraryModel.Elements
    #>
        Element: <#= element.Name #>
    <#
    Next
    #>
    ```

5. **ソリューション エクスプローラー** で、DebugTest.tt を右クリックし、 **[カスタム ツールの実行]** をクリックします。

     これで、システムによってテキスト テンプレートが変換され、対応する出力ファイルが生成されます。 **[エラー一覧]** ウィンドウにエラーは表示されません。
