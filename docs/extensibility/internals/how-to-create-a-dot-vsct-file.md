---
title: '方法: .Vsct ファイルを作成する | Microsoft Docs'
description: .vsct ファイル (XML ベース Visual Studio コマンド テーブル構成ファイル) を手動で作成する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- VSCT files, creating
ms.assetid: b955f51c-f9f9-49c3-a8e4-63b6eb0e0341
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 7fe1d92a9117193a72f579a01f264f1a13be6b6e
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105056611"
---
# <a name="how-to-create-a-vsct-file"></a>方法: .vsct ファイルを作成する

XML ベース Visual Studio コマンド テーブル構成 ( *.vsct*) ファイルを作成する方法はいくつかあります。

- [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] パッケージ テンプレートで新しい VSPackage を作成できます。

- XML ベース コマンド テーブル構成コンパイラ *Vsct.exe* を使用して、既存の *.ctc* ファイルからファイルを生成できます。

- *Vsct.exe* を使用して、既存の *.cto* ファイルから *.vsct* ファイルを生成できます。

- 新しい *.vsct* ファイルを手動で作成できます。

  この記事では、新しい *.vsct* ファイルを手動で作成する方法について説明します。

### <a name="to-manually-create-a-new-vsct-file"></a>新しい .vsct ファイルを手動で作成するには

1. [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]を起動します。

2. **[ファイル]** メニューの **[新規作成]** をポイントし、 **[ファイル]** をクリックします。

3. **[テンプレート]** ペインで、 **[XML ファイル]** をクリックし、 **[開く]** をクリックします。

4. **[表示]** メニューの **[プロパティ]** をクリックして、XML ファイルのプロパティを表示します。

5. **[プロパティ]** ウィンドウで、 **[スキーマ]** プロパティの **[参照]** ボタンをクリックします。

6. XSD スキーマの一覧で、*vsct.xsd* スキーマを選択します。 これが一覧に表示されない場合、 **[追加]** をクリックし、ローカル ドライブでこのファイルを見つけます。 **[OK]** をクリックして終了します。

7. XML ファイルに、「 *<CommandTable*」と入力してから、**Tab** キーを押します。「 *>* 」と入力してタグを閉じます。

    この操作によって、基本的な *.vsct* ファイルが作成されます。

8. 「[VSCT XML スキーマ リファレンス](../../extensibility/vsct-xml-schema-reference.md)」に従って、追加しようとする XML ファイルに要素を入力します。 詳細については、「[vsct ファイルを記述する](../../extensibility/internals/authoring-dot-vsct-files.md)」を参照してください。

<a name="how-to-create-a-dot-vsct-file-from-an-existing-dot-ctc-file"></a>

## <a name="how-to-create-a-vsct-file-from-an-existing-ctc-file"></a>方法: 既存の .ctc ファイルから .vsct ファイルを作成する

既存のコマンド テーブルの *.ctc* ソース ファイルから XML ベースの *.vsct* ファイルを作成できます。 これにより、新しい XML ベースの [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] コマンド テーブル (VSCT) コンパイラ形式を利用できます。

### <a name="to-create-a-vsct-file-from-a-ctc-file"></a>.ctc ファイルから .vsct ファイルを作成するには

1. Perl 言語のコピーを取得します。

2. Perl スクリプト *ConvertCTCToVSCT.pl* のコピーを取得します (通常、 *\<Visual Studio SDK installation path>\VisualStudioIntegration\Tools\bin* フォルダーにあります)。

3. 変換する *.ctc* ソース ファイルのコピーを取得します。

4. 同じディレクトリにファイルを配置します。

5. [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] のコマンド プロンプト ウィンドウで、そのディレクトリに移動します。

6. Type

   ```
   perl.exe ConvertCTCtoVSCT.pl PkgCmd.ctc PkgCmd.vsct
   ```

    *PkgCmd.ctc* は *.ctc* ファイルの名前であり、*PkgCmd.vsct* は作成する *.vsct* ファイルの名前です。

    この操作によって、新しい *.vsct* XML コマンド テーブル ソース ファイルが作成されます。 他の *.vsct* ファイルと同様に、*Vsct.exe* (VSCT コンパイラ) を使用してファイルをコンパイルできます。

   > [!NOTE]
   > XML コメントの書式を変更すると、 *.vsct* ファイルの読みやすさを改善できます。

<a name="how-to-create-a-dot-vsct-file-from-an-existing-dot-cto-file"></a>

## <a name="how-to-create-a-vsct-file-from-an-existing-cto-file"></a>方法: 既存の .cto ファイルから .vsct ファイルを作成する

既存のバイナリ *.cto* ファイルから XML ベースの *.vsct* ファイルを作成できます。 これを行うことで、新しいコマンド テーブル コンパイラ形式を活用できます。 このプロセスは、 *.ctc* ファイルから *.cto* ファイルをコンパイルした場合でも機能します。 *.vsct* ファイルを編集して、別の .cto ファイルにコンパイルできます。

### <a name="to-create-a-vsct-file-from-a-cto-file"></a>.cto ファイルから .vsct ファイルを作成するには

1. *.cto* ファイルと、対応する *.ctsym* ファイルのコピーを取得します。

2. ファイルを *vsct.exe* コンパイラと同じディレクトリに配置します。

3. Visual Studio コマンド プロンプトで、 *.cto* ファイルと *.ctsym* ファイルが保存されているディレクトリに移動します。

4. Type

    ```
    vsct.exe <ctofilename>.cto <vsctfilename>.vsct -S<symfilename>.ctsym
    ```

     ここで、\<ctofilename\> は *.cto* ファイルの名前、\<vsctfilename\> は作成する *.vsct* ファイルの名前、\<symfilename\> は *.ctsym* ファイルの名前です。

     このプロセスによって、新しい *.vsct* XML コマンド テーブル コンパイラ ファイルが作成されます。 他の *.vsct* ファイルと同様に、*vsct.exe* (vsct コンパイラ) を使用して、ファイルを編集およびコンパイルできます。

## <a name="compile-the-code"></a>コードのコンパイル
 *.vsct* ファイルをプロジェクトに追加するだけでは、コンパイルは行われません。 ビルド プロセスに組み込む必要があります。

### <a name="to-add-a-vsct-file-to-project-compilation"></a>プロジェクトのコンパイルに .vsct ファイルを追加するには

1. エディターでプロジェクト ファイルを開きます。 プロジェクトが読み込まれている場合は、最初にアンロードする必要があります。

2. 次の例に示すように、`VSCTCompile` 要素を含む [ItemGroup 要素](../../msbuild/itemgroup-element-msbuild.md)を追加します。

    ```xml
    <ItemGroup>
      <VSCTCompile Include="TopLevelMenu.vsct">
        <ResourceName>Menus.ctmenu</ResourceName>
      </VSCTCompile>
    </ItemGroup>

    ```

     `ResourceName` 要素には常に `Menus.ctmenu` を設定します。

3. プロジェクトに *.resx* ファイルが含まれる場合は、次の例に示すように、`MergeWithCTO`要素を含む `EmbeddedResource` 要素を追加します。

    ```xml
    <EmbeddedResource Include="VSPackage.resx">
      <MergeWithCTO>true</MergeWithCTO>
      <ManifestResourceName>VSPackage</ManifestResourceName>
    </EmbeddedResource>

    ```

     このマークアップは、埋め込みリソースを含む`ItemGroup` 要素内に配置する必要があります。

4. パッケージ ファイル (通常は *\<ProjectName\>Package.cs* または *\<ProjectName\>Package.vb* という名前) をエディターで開きます。

5. 次の例に示すように、`ProvideMenuResource` 属性をパッケージ クラスに追加します。

    ```csharp
    [ProvideMenuResource("Menus.ctmenu", 1)]
    ```

     最初のパラメーター値は、プロジェクト ファイルで定義した `ResourceName` 属性の値と一致する必要があります。

## <a name="see-also"></a>こちらもご覧ください
- [.vsct ファイルを記述する](../../extensibility/internals/authoring-dot-vsct-files.md)
- [Visual Studio コマンド テーブル (.vsct) ファイル](../../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
- [VSCT XML スキーマ リファレンス](../../extensibility/vsct-xml-schema-reference.md)
