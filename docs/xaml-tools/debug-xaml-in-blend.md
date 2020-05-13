---
title: Blend で XAML をデバッグする |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 29a37182-2a2c-47e4-a4a9-2d5412738fed
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.technology: vs-ide-debug
ms.workload:
- uwp
ms.openlocfilehash: 04bd4540de47ec8a9da86069acb33770f9c800b8
ms.sourcegitcommit: 9de7d25056da59df0941508c80c0b12766ba6580
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/27/2020
ms.locfileid: "82921257"
---
# <a name="debug-xaml-in-blend"></a>Blend での XAML のデバッグ

Blend for Visual Studio のツールを使用して、アプリで XAML をデバッグできます。 プロジェクトをビルドする場合、エラーは **[結果]** パネルに表示されます。 エラーをダブルクリックして、エラーに関連するマークアップを検索します。 作業領域を増やす必要がある場合は、 **F12**キーを押して [**結果**] パネルを非表示にすることができます。

## <a name="syntax-errors"></a>構文エラー

構文エラーは、XAML または分離コード ファイルが言語のフォーマット規則に従っていない場合に発生します。 エラーの説明を参照すると、エラーの解決に役立ちます。 一覧では、エラーの発生しているファイルの名前と行番号も確認できます。 XAML エラーは **[結果]** パネルの **[マークアップ]** タブに一覧されます。

> [!TIP]
> XAML は XML に基づくマークアップ言語で、XML 構文規則に従っています。

XAML 構文エラーのよくある原因は次のとおりです。

- キーワードのスペルまたは大文字の表記に誤りがある。

- 属性またはテキスト文字列の両側に引用符がない。

- XAML 要素に終了タグがない。

- XAML 要素が許可されていない場所にある。

共通 XAML 構文の詳細については、「[Basic XAML syntax guide](/windows/uwp/xaml-platform/xaml-syntax-guide)」 (基本的な XAML 構文のガイド) を参照してください。

Blend では、単純な分離コード構文エラー、コンパイルエラー、および実行時エラーを特定して解決することもできます。 ただし、分離コード エラーは Visual Studio で識別して解決する方が簡単です。

### <a name="debugging-sample-xaml-code"></a>サンプル XAML コードのデバッグ

次の例では、Blend における単純な XAML デバッグセッションについて説明します。

#### <a name="to-create-a-project"></a>プロジェクトを作成するには

1. Blend で、[**ファイル**] メニューを開き、[**新しいプロジェクト**] をクリックします。

    **[新しいプロジェクト]** ダイアログ ボックスの左側に、プロジェクトの種類の一覧が表示されます。 プロジェクトの種類をクリックすると、その種類に関連付けられているプロジェクト テンプレートが右側に表示されます。

2. プロジェクトの種類の一覧で、[ **Windows ユニバーサル**] をクリックします。

3. プロジェクトテンプレートの一覧で、[**空のアプリ (ユニバーサル Windows)**] をクリックします。

4. [**名前**] テキストボックスに「 `DebuggingSample`」と入力します。

5. **[場所]** ボックスでプロジェクトの場所を確認します。

6. **[言語]** ボックスの一覧で、**[Visual C#]** をクリックし、**[OK]** をクリックしてプロジェクトを作成します。

7. デザイン サーフェイスを右クリックし、**[ソースの表示]** をクリックして **[分割]** ビューに切り替えます。

8. コードの右上隅にある **[コピー]** リンクをクリックして、次のコードをコピーします。

   ```xml
   <Grid HorizontalAlignment="Left" Height="222" VerticalAlignment="Top>
        <Button content="Button" x:Mame="Home" HorizontalAlignment="Left" VerticalAlignment="Top"/>
        <Button Content="Button" HorizontalAlignment="Left" VerticalAlignment="Top" Margin="0,38,0,0">
        <Button Content="Button" HorizontalAlignment="Left" VerticalAlignment="Top" Margin="0,75,0,0"/>
        <Button Content="Button" HorizontalAlignment="Left" VerticalAlignment="Top" Margin="0,112,0,0"/>
        <Button Content="Button" HorizontalAlignment="Left" VerticalAlignment="Top Margin="0,149,0,0"/>
   </Grid>
   ```

9. 既定の**グリッド**を探し、**Grid** の開始タグと終了タグの間にコードを貼り付けます。 完成したコードは次のようになります。

    ```xml
    <Grid Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">
         <Grid HorizontalAlignment="Left" Height="222" VerticalAlignment="Top>
              <Button content="Button" x:Mame="Home" HorizontalAlignment="Left" VerticalAlignment="Top"/>
              <Button Content="Button" HorizontalAlignment="Left" VerticalAlignment="Top" Margin="0,38,0,0">
              <Button Content="Button" HorizontalAlignment="Left" VerticalAlignment="Top" Margin="0,75,0,0"/>
              <Button Content="Button" HorizontalAlignment="Left" VerticalAlignment="Top" Margin="0,112,0,0"/>
              <Button Content="Button" HorizontalAlignment="Left" VerticalAlignment="Top Margin="0,149,0,0"/>
         </Grid>
    </Grid>
    ```

10. **Ctrl**+**Shift**Shift+**B**キーを押して、プロジェクトをビルドします。

    プロジェクトをビルドできないことを警告するエラー メッセージが表示され、エラーを一覧表示した **[結果]** パネルがアプリの下部に表示されます。

    ![Blend for Visual Studio 内での XAML のデバッグ](../debugger/media/blend_debugxaml_xaml.png "blend_debugXAML_XAML")

### <a name="resolve-xaml-errors"></a>XAML エラーの解決

XAML エラーが検出された場合、プロジェクトに無効なマークアップが含まれているという警告がデザイン サーフェスに表示されます。 エラーを解決すると、**[結果]** パネルのエラー リストが更新されます。 すべてのエラーを解決すると、デザイン サーフェスが有効になり、アプリがデザイン サーフェスに表示されます。

#### <a name="to-resolve-the-xaml-errors"></a>XAML エラーを解決するには

1. リストの最初のエラーをダブルクリックします。 説明は、"値 '<' は、属性では無効です" となります。 エラーをダブルクリックすると、ポインターがコード内の対応する場所を見つけます。 `<` の前の `Button` は有効で、エラー メッセージで指定された属性ではありません。 コードの前の行を見ると、属性 `Top` の終わりの引用符がないことがわかります。 終わりの引用符を入力します。 **[結果]** パネルのエラー リストが更新されて変更が反映されていることに注意してください。

2. "' 0 ' は名前の先頭では無効です" という説明をダブルクリックします。 `Margin="0,149,0,0"`適切な形式である可能性があります。 ただし、`Margin` のカラー コーディングはコードの `Margin` の他のインスタンスと一致しないことに注意してください。 終わりの引用符が前の名前/値ペア (`VerticalAlignment="Top`) にないため、`Margin="` は前の属性の値の一部として読み込まれ、0 が名前/値ペアの先頭として読み込まれます。 `Top` の終わりの引用符を入力します。 **[結果]** パネルのエラー リストが更新されて変更が反映されます。

3. 残りのエラーをダブルクリックします。"終わりの XML タグ 'Button' が一致しません。" ポインターは終わりの **Grid** タグ (`</Grid>`) にあり、エラーが `Grid` オブジェクトの内側にあることを示します。 2 番目の `Button` オブジェクトで終わりのタグがないことに注意してください。 終わりの `/` を追加すると、**[結果]** パネル リストが更新されます。 これら 2 つの最初のエラーが解決され、さらに 2 つのエラーが識別されました。

4. "メンバー 'content' が認識されないか、アクセスできません。" をダブルクリックします。 `c` の `content` は大文字になります。 小文字の "c" を大文字の "c" に置き換えます。

5. [プロパティ ' Mame ' は`http://schemas.microsoft.com/winfx/2006/xaml`名前空間に存在しません。 "をダブルクリックします。 "Mame" の "M" は "N" でなければなりません。 "M" を "N" で置き換えます。 これで、XAML が解析でき、アプリがデザイン サーフェスに表示されます。

    ![Blend for Visual Studio 内での XAML のデバッグ](../debugger/media/blend_debugartboard_xaml.png "blend_debugArtboard_XAML")

    **Ctrl**+**Shift**Shift+**B**キーを押してプロジェクトをビルドし、エラーが残っていないことを確認します。

## <a name="debug-in-visual-studio"></a>Visual Studio でのデバッグ

Visual Studio で Blend プロジェクトを開くと、アプリのコードをより簡単にデバッグできます。 Visual Studio で Blend プロジェクトを開くには、[**プロジェクト**] パネルでプロジェクトを右クリックし、[ **visual Studio での編集**] をクリックします。 Visual Studio でデバッグセッションを完了したら、Ctrl + Shift + S キーを押してすべての変更を保存し、Blend に戻します。 プロジェクトの再読み込みを求めるメッセージが表示されます。 [**すべてはい] を**クリックして、Blend での作業を続行します。

アプリのデバッグの詳細については、「 [Visual Studio での UWP アプリのデバッグ](../debugger/debugging-windows-store-and-windows-universal-apps.md)」を参照してください。

## <a name="get-help"></a>ヘルプの参照

Blend アプリのデバッグに関するヘルプが必要な場合は、 [UWP アプリコミュニティフォーラム](https://social.msdn.microsoft.com/Forums/windowsapps/home?category=windowsapps)で、問題に関連する投稿や質問を投稿することができます。
