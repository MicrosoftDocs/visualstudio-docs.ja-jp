---
title: '新しいプロジェクトの生成: 内部的な処理、パート 1 | Microsoft Docs'
description: 独自のプロジェクトの種類を作成したとき、Visual Studio 統合開発環境 (IDE) 内で何が起こるかを詳しく見てみましょう (パート 1/2)。
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- projects [Visual Studio], new project dialog
- projects [Visual Studio], new project generation
ms.assetid: 66778698-0258-467d-8b8b-c351744510eb
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 27a7e0f3175388b963e85950ea903843caff3baa
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105063150"
---
# <a name="new-project-generation-under-the-hood-part-one"></a>新しいプロジェクトの生成: 内部的な処理、パート 1
独自のプロジェクトの種類を作成する方法について考えたことはありますか。 新しいプロジェクトを作成すると、実際には何が起こるでしょうか。 では、実際に何が起こっているかを見てみましょう。

 Visual Studio によって自動的に調整されるタスクがいくつかあります。

- 使用できるすべてのプロジェクトの種類のツリーが表示されます。

- プロジェクトの種類ごとにアプリケーション テンプレートの一覧が表示され、いずれかを選択できます。

- プロジェクトの名前やパスなど、アプリケーションのプロジェクト情報が収集されます。

- この情報はプロジェクト ファクトリに渡されます。

- 現在のソリューションにプロジェクト項目とフォルダーが生成されます。

## <a name="the-new-project-dialog-box"></a>[新しいプロジェクト] ダイアログ ボックス
 すべては新しいプロジェクトのプロジェクトの種類を選択することから始まります。 まず、 **[ファイル]** メニューの **[新しいプロジェクト]** をクリックしましょう。 次のように **[新しいプロジェクト]** ダイアログ ボックスが表示されます。

 ![[新しいプロジェクト] ダイアログ ボックスのスクリーン ショット。](../../extensibility/internals/media/newproject.gif)

 詳しく見ていきましょう。 **[プロジェクトの種類]** ツリーには、作成できるさまざまなプロジェクトの種類が一覧表示されます。 **Visual C# Windows** などのプロジェクトの種類を選択すると、基礎となるアプリケーション テンプレートの一覧が表示されます。 **[Visual Studio にインストールされたテンプレート]** は Visual Studio によってインストールされたもので、コンピューターのすべてのユーザーが使用できます。 作成または収集した新しいテンプレートは **[マイ テンプレート]** に追加され、自分だけが使用できます。

 **Windows アプリケーション** のようなテンプレートを選択すると、アプリケーションの種類の説明 (この場合は "**Windows ユーザー インターフェイスを含むアプリケーションを作成するためのプロジェクト**") がダイアログ ボックスに表示されます。

 **[新しいプロジェクト]** ダイアログ ボックスの下部に、その他の情報が収集されるコントロールがいくつか表示されます。 表示されるコントロールはプロジェクトの種類によって異なりますが、通常、プロジェクトの **[名前]** テキスト ボックス、 **[場所]** テキスト ボックスと関連する **[参照]** ボタン、 **[ソリューション名]** テキスト ボックスと関連する **[ソリューションのディレクトリを作成]** チェック ボックスなどがあります。

## <a name="populating-the-new-project-dialog-box"></a>[新しいプロジェクト] ダイアログ ボックスの設定
 **[新しいプロジェクト]** ダイアログ ボックスの情報はどこから取得されているのでしょうか。 ここには 2 つのメカニズムが機能しており、そのうちの 1 つは非推奨です。 **[新しいプロジェクト]** ダイアログ ボックスには、両方のメカニズムから取得した情報が組み合わされ、表示されます。

 古い (非推奨の) 方法には、システム レジストリ エントリと .vsdir ファイルが使用されています。 このメカニズムは、Visual Studio を開いたときに実行されます。 新しい方法には、.vstemplate ファイルが使用されています。 このメカニズムは、たとえば、以下を実行した場合など、Visual Studio が初期化されるときに実行されます

```
devenv /setup
```

 or

```
devenv /installvstemplates
```

### <a name="project-types"></a>プロジェクトの種類
 **[Visual C#]** や **[他の言語]** などの **[プロジェクトの種類]** のルート ノードの位置と名前は、システム レジストリ エントリによって決定されます。 **[データベース]** や **[スマート デバイス]** などの子ノードの編成は、対応する .vstemplate ファイルを含むフォルダーの階層を反映しています。 まず、ルート ノードを見てみましょう。

#### <a name="project-type-root-nodes"></a>[プロジェクトの種類] のルート ノード
 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] が初期化されると、システム レジストリ キー HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\14.0\NewProjectTemplates\TemplateDirs のサブキーが走査され、 **[プロジェクトの種類]** ツリーのルート ノードを構築され、名前が付けられます。 この情報は、後で使用するためにキャッシュされます。 TemplateDirs\\{FAE04EC1-301F-11D3-BF4B-00C04F79EFBC}\\/1 キーを見てください。 各エントリは VSPackage GUID です。 サブキー (/1) の名前は無視されますが、その存在は、これが **[プロジェクトの種類]** ルート ノードであることを示します。 ルート ノードには、 **[プロジェクトの種類]** ツリーの外観を制御するサブキーがいくつかあります。 それらの一部を見てみましょう。

##### <a name="default"></a>(既定値)。
 これは、ルート ノードの名前を表すローカライズされた文字列のリソース ID です。 文字列リソースは、VSPackage GUID によって選択されたサテライト DLL 内にあります。

 この例の VSPackage GUID は次のとおりです

 {FAE04EC1-301F-11D3-BF4B-00C04F79EFBC}

 また、ルート ノード (/1) のリソース ID (既定値) は #2345 です

 近くの Package キーで GUID を検索し、SatelliteDll サブキーを調べると、文字列リソースを含むアセンブリのパスを見つけることができます。

 \<Visual Studio installation path>\VC#\VCSPackages\1033\csprojui.dll

 これを確認するには、ファイル エクスプローラーを開き、csprojui.dll を Visual Studio ディレクトリにドラッグします。 文字列テーブルを見ると、リソース #2345 にキャプション **Visual C#** があることがわかります。

##### <a name="sortpriority"></a>SortPriority
 これにより、 **[プロジェクトの種類]** ツリー内のルート ノードの位置が決まります。

 SortPriority REG_DWORD 0x00000014 (20)

 優先度の数値が小さいほど、ツリー内の位置は高くなります。

##### <a name="developeractivity"></a>DeveloperActivity
 このサブキーが存在する場合、ルート ノードの位置は [Developer Settings]\(開発者向け設定\) ダイアログ ボックスによって制御されます。 たとえば、次のように入力します。

 DeveloperActivity REG_SZ VC#

 これは、Visual Studio が [!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)] 開発用に設定されている場合、Visual C# がルート ノードになることを示します。 それ以外の場合は、 **[他の言語]** の子ノードになります。

##### <a name="folder"></a>Folder
 このサブキーが存在する場合、ルート ノードは指定されたフォルダーの子ノードになります。 キーの下に指定できるフォルダーの一覧が表示されます

 HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\11.0\NewProjectTemplates\PseudoFolders

 たとえば、[データベース プロジェクト] エントリには、PseudoFolders の [その他のプロジェクトの種類] エントリと一致するフォルダー キーがあります。 そのため、 **[プロジェクトの種類]** ツリーでは、 **[データベース プロジェクト]** は **[その他のプロジェクトの種類]** の子ノードになります。

#### <a name="project-type-child-nodes-and-vstdir-files"></a>[プロジェクトの種類] の子ノードと .vstdir ファイル
 **[プロジェクトの種類]** ツリー内の子ノードの位置は、ProjectTemplates フォルダー内のフォルダーの階層に従います。 マシン テンプレート (**Visual Studio によってインストールされたテンプレート**) の場合、通常の場所は \Program Files\Microsoft Visual Studio 14.0\Common7\IDE\ProjectTemplates\ であり、ユーザー テンプレート (**マイ テンプレート**) の場合、一般的な場所は \My Documents\Visual Studio 14.0\Templates\ProjectTemplates\\ です。 これら 2 つの場所のフォルダー階層がマージされて、 **[プロジェクトの種類]** ツリーが作成されます。

 C# の開発者向け設定を行った Visual Studio の場合、 **[プロジェクトの種類]** ツリーは次のようになります。

 ![C# の開発者向け設定を行った Visual Studio の [プロジェクトの種類] フォルダー ツリーのスクリーンショット。](../../extensibility/internals/media/projecttypes.png)

 対応する ProjectTemplates フォルダーは次のようになります。

 ![C# の開発者向け設定を行った Visual Studio の [プロジェクトのテンプレート] フォルダー ツリーのスクリーンショット。](../../extensibility/internals/media/projecttemplates.png)

 **[新しいプロジェクト]** ダイアログ ボックスが開くと、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] は ProjectTemplates フォルダーが走査され、変更をいくつか加えた構造が **[プロジェクトの種類]** ツリーに再作成されます。

- **[プロジェクトの種類]** ツリーのルート ノードは、アプリケーション テンプレートによって決定されます。

- ノード名はローカライズすることができます。また、特殊文字を含めることができます。

- 並べ替え順序は変更できます。

##### <a name="finding-the-root-node-for-a-project-type"></a>プロジェクトの種類のルート ノードの検索
 Visual Studio によって ProjectTemplates フォルダーが走査されると、すべての .zip ファイルが開かれ、.vstemplate ファイルが抽出されます。 .vstemplate ファイルには、XML を使用してアプリケーション テンプレートが記述されています。 詳細については、「[新しいプロジェクトの生成: 内部的な処理、パート 2](../../extensibility/internals/new-project-generation-under-the-hood-part-two.md)」を参照してください。

 \<ProjectType> タグにより、アプリケーションのプロジェクトの種類が決まります。 たとえば、\CSharp\SmartDevice\WindowsCE\1033\WindowsCE-EmptyProject.zip ファイルには、次のタグを持つ EmptyProject.vstemplate ファイルが含まれています。

```
<ProjectType>CSharp</ProjectType>
```

 ProjectTemplates フォルダー内のサブフォルダーではなく、\<ProjectType> タグにより、 **[プロジェクトの種類]** ツリー内のアプリケーションのルート ノードが決まります。 この例では、Windows CE アプリケーションは **[Visual C#]** ルート ノードの下に表示され、WindowsCE フォルダーを VisualBasic フォルダーに移動したとしても、Windows CE アプリケーションは **[Visual C#]** ルート ノードの下に表示されます。

##### <a name="localizing-the-node-name"></a>ノード名のローカライズ
 Visual Studio によって ProjectTemplates フォルダーが走査されるときに、見つかったすべての .vstdir ファイルが調査されます。 .vstdir ファイルは、 **[新しいプロジェクト]** ダイアログ ボックスのプロジェクトの種類の外観を制御する XML ファイルです。 .vstdir ファイルで、\<LocalizedName> タグを使用して **[プロジェクトの種類]** ノードに名前を付けます。

 たとえば、\CSharp\Database\TemplateIndex.vstdir ファイルには次のタグが含まれています。

```
<LocalizedName Package="{462b036f-7349-4835-9e21-bec60e989b9c}" ID="4598"/>
```

 これにより、ルート ノード (この場合は **データベース**) の名前を表すローカライズされた文字列のサテライト DLL とリソース ID が決まります。 ローカライズされた名前には、 **.NET** などのフォルダー名には使用できない特殊文字を含めることができます。

 \<LocalizedName> タグが存在しない場合、プロジェクトの種類は、フォルダー自体 **SmartPhone2003** によって名前が付けられます。

##### <a name="finding-the-sort-order-for-a-project-type"></a>プロジェクトの種類の並べ替え順序の検索
 プロジェクトの種類の並べ替え順序を決定するために、.vstdir ファイルに \<SortOrder> タグを使用します。

 たとえば、\CSharp\Windows\Windows.vstdir ファイルには次のタグが含まれています。

```
<SortOrder>5</SortOrder>
```

 \CSharp\Database\TemplateIndex.vstdir ファイルには、より大きな値のタグがあります。

```
<SortOrder>5000</SortOrder>
```

 \<SortOrder> タグの数値が小さいほど、ツリー内の位置が高くなるため、 **[プロジェクトの種類]** ツリーで **[Windows]** ノードは **[データベース]** ノードよりも上位に表示されます。

 プロジェクトの種類に \<SortOrder> タグが指定されていない場合、\<SortOrder> 仕様を含むプロジェクトの種類の後にアルファベット順に表示されます。

 My Documents (**My Templates**) フォルダーには .vstdir ファイルがないことに注意してください。 ユーザー アプリケーションのプロジェクトの種類名はローカライズされておらず、アルファベット順に表示されます。

#### <a name="a-quick-review"></a>クイック レビュー
 **[新しいプロジェクト]** ダイアログ ボックスを変更して、新しいユーザー プロジェクト テンプレートを作成しましょう。

1. MyProjectNode サブフォルダーを \Program Files\Microsoft Visual Studio 14.0\Common7\IDE\ProjectTemplates\CSharp フォルダーに追加します。

2. 任意のテキスト エディターを使用して、MyProjectNode フォルダーに MyProject.vstdir ファイルを作成します。

3. 次の行を .vstdir ファイルに追加します。

   ```
   <TemplateDir Version="1.0.0">
       <SortOrder>6</SortOrder>
   </TemplateDir>
   ```

4. .vstdir ファイルを保存して閉じます。

5. 任意のテキスト エディターを使用して、MyProjectNode フォルダーに MyProject.vstemplate ファイルを作成します。

6. 次の行を .vstemplate ファイルに追加します。

   ```
   <VSTemplate Version="2.0.0" Type="Project" xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">
       <TemplateData>
           <ProjectType>CSharp</ProjectType>
       </TemplateData>
   </VSTemplate>
   ```

7. .vstemplate ファイルを保存し、エディターを閉じます。

8. .vstemplate ファイルを新しい圧縮された MyProjectNode\MyProject.zip フォルダーに送信します。

9. Visual Studio のコマンド ウィンドウで、次のように入力します。

    ```
    devenv /installvstemplates
    ```

   Visual Studio を開きます。

10. **[新しいプロジェクト]** ダイアログ ボックスを開き、 **[Visual C#]** プロジェクト ノードを展開します。

    ![展開された Visual C# プロジェクト ノードの下で MyProjectNode が強調表示された、[新しいプロジェクト] ダイアログ ボックスの [プロジェクトの種類] フォルダー ツリーのスクリーンショット。](../../extensibility/internals/media/myprojectnode.png)

    **MyProjectNode** は、Windows ノードのすぐ下にある Visual C# の子ノードとして表示されます。

## <a name="see-also"></a>こちらもご覧ください
- [新しいプロジェクトの生成: 内部的な処理、パート 2](../../extensibility/internals/new-project-generation-under-the-hood-part-two.md)
