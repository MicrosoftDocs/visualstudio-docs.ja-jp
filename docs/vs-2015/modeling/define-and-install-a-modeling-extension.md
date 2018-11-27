---
title: 定義およびモデリング拡張機能のインストール |Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-tfs-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- UML - extending
- UML model, extending
ms.assetid: 82a58dc5-c7cf-4521-a6da-7ff09cd0de9d
caps.latest.revision: 39
author: gewarren
ms.author: gewarren
manager: douge
ms.openlocfilehash: 6f7895916cc4ee877c53b056f703d8e46b64b409
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/16/2018
ms.locfileid: "51805568"
---
# <a name="define-and-install-a-modeling-extension"></a>モデリング拡張機能を定義およびインストールする
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio では、モデリング図に対して拡張機能を定義することができます。 これにより、図とモデルを各自のニーズに適応させることができます。 たとえば、メニュー コマンド、UML プロファイル、検証制約、およびツールボックスの項目を定義できます。 単一の拡張機能で複数のコンポーネントを定義できます。 また、これらの拡張機能を [VSIX (Visual Studio Integration Extension)](http://go.microsoft.com/fwlink/?LinkId=160780)の形式で他の Visual Studio ユーザーに配布することもできます。 Visual Studio で VSIX プロジェクトを使用して VSIX を作成できます。  
  
## <a name="requirements"></a>必要条件  
 「 [要件](../modeling/extend-uml-models-and-diagrams.md#Requirements)」を参照してください。  
  
 この機能をサポートする Visual Studio のバージョンを確認するには、「 [Version support for architecture and modeling tools](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport)」を参照してください。  
  
## <a name="creating-a-modeling-extension-solution"></a>モデリング拡張機能ソリューションの生成  
 モデリング拡張機能を定義するには、次のプロジェクトを含むソリューションを生成する必要があります。  
  
- [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] Integration Extension (VSIX) プロジェクト。 このプロジェクトでは、拡張機能のコンポーネントのインストーラーとして機能するファイルを生成します。  
  
- プログラム コードを含むコンポーネントに必要なクラス ライブラリ プロジェクト。  
  
  1 つの拡張機能を複数のコンポーネントで構成する場合は、単一のソリューションにそれらのコンポーネントを組み込むことができます。 必要な VSIX プロジェクトは 1 つだけです。  
  
  カスタム ツールボックス項目やカスタム UML プロファイルなど、コードを必要としないコンポーネントは、別個のクラス ライブラリ プロジェクトを使用せずに直接 VSIX プロジェクトに追加できます。 プログラム コードが必要なコンポーネントは、別個のクラス ライブラリ プロジェクトを使用してさらに簡単に定義できます。 コードが必要なコンポーネントとしては、ジェスチャ ハンドラー、メニュー コマンド、検証コードなどがあります。  
  
#### <a name="to-create-a-class-library-project-for-menu-commands-gesture-handlers-or-validation"></a>メニュー コマンド、ジェスチャ ハンドラー、または検証のクラス ライブラリ プロジェクトを作成するには  
  
1.  **[ファイル]** メニューで、 **[新規]**、 **[プロジェクト]** をクリックします。  
  
2.  **[インストールされたテンプレート]** の **[Visual Basic]** または **[Visual C#]** をクリックし、 **[クラス ライブラリ]** をクリックします。  
  
#### <a name="to-create-a-vsix-project"></a>VSIX プロジェクトを作成するには  
  
1.  コードを含むコンポーネントを作成する場合は、最初にクラス ライブラリ プロジェクトを作成するのが最も簡単な方法です。 コードはそのプロジェクトに追加します。  
  
2.  VSIX プロジェクトを作成する。  
  
    1.  **ソリューション エクスプローラー**で、ソリューションのショートカット メニューを開き、 **[追加]**、 **[新しいプロジェクト]** の順にクリックします。  
  
    2.  **[インストールされたテンプレート]** の **[Visual C#]** または **[Visual Basic]** を展開し、 **[機能拡張]** をクリックします。 中央の列で、 **[VSIX プロジェクト]** をクリックします。  
  
3.  VSIX プロジェクトをソリューションのスタートアップ プロジェクトとして設定します。  
  
    -   ソリューション エクスプローラーで、VSIX プロジェクトのショートカット メニューを開き、 **[スタートアップ プロジェクトに設定]** をクリックします。  
  
4.  **source.extension.vsixmanifest**を開きます。 マニフェスト エディターでファイルが開きます。  
  
5.  **[メタデータ]** タブで、VSIX の名前と説明のフィールドを設定します。  
  
6.  **[インストールの対象]** タブで **[新規作成]** を選択し、Visual Studio のバージョンを対象として設定します。  
  
7.  **[アセット]** タブで、コンポーネントを Visual Studio 拡張機能に追加します。  
  
    1.  **[新規作成]** をクリックします。  
  
    2.  コードを含むコンポーネントの場合は、 **[Add New Asset]** (新しいアセットの追加) ダイアログ ボックスで、次のフィールドを設定します。  
  
        |||  
        |-|-|  
        |**型** =|**[Microsoft.visualstudio.mefcomponent]**|  
        |**Source** =|**現在のソリューション内のプロジェクト**|  
        |**プロジェクト** =|*クラス ライブラリ プロジェクト*|  
        |**このフォルダーに埋め込む** =|*(空)*|  
  
         その他の種類のコンポーネントについては、次のセクションのリンクを参照してください。  
  
## <a name="developing-the-component"></a>コンポーネントの開発  
 メニュー コマンドやジェスチャ ハンドラーなどの各コンポーネントに対し、個別のハンドラーを定義する必要があります。 同じクラス ライブラリ プロジェクトに複数のハンドラーを設定できます。 次の表は、さまざまな種類のハンドラーの一覧です。  
  
|拡張機能の種類|トピック|各コンポーネントの一般的な宣言方法|  
|--------------------|-----------|----------------------------------------------|  
|メニュー コマンド|[モデリング図にメニュー コマンドを定義する](../modeling/define-a-menu-command-on-a-modeling-diagram.md)|`[ClassDesignerExtension]`<br /><br /> `// or other diagram types`<br /><br /> `[Export(typeof(ICommandExtension))]`<br /><br /> `public class MyCommand : ICommandExtension`<br /><br /> `{...`|  
|ドラッグ アンド ドロップまたはダブルクリック|[モデリング図にジェスチャ ハンドラーを定義する](../modeling/define-a-gesture-handler-on-a-modeling-diagram.md)|`[ClassDesignerExtension]`<br /><br /> `// or other diagram types`<br /><br /> `[Export(typeof(IGestureExtension))]`<br /><br /> `public class MyGesture : IGestureExtension`<br /><br /> `{...`|  
|検証制約|[UML モデルの検証制約を定義する](../modeling/define-validation-constraints-for-uml-models.md)|`[Export(typeof(     System.Action<ValidationContext, object>))]`<br /><br /> `[ValidationMethod(ValidationCategories.Save`<br /><br /> `&#124; ValidationCategories.Menu)]`<br /><br /> `public void ValidateSomething`<br /><br /> `(ValidationContext context, IClassifier elementToValidate)`<br /><br /> `{...}`|  
|作業項目リンク イベント ハンドラー|[作業項目リンク ハンドラーを定義する](../modeling/define-a-work-item-link-handler.md)|`[Export(typeof(ILinkedWorkItemExtension))]`<br /><br /> `public class MyWorkItemEventHandler : ILinkedWorkItemExtension`<br /><br /> `{...`|  
|UML プロファイル|[プロファイルを定義して UML を拡張する](../modeling/define-a-profile-to-extend-uml.md)|(未定義)|  
|ツールボックス項目|[カスタム モデリング ツールボックス アイテムを定義する](../modeling/define-a-custom-modeling-toolbox-item.md)|(未定義)|  
  
## <a name="running-an-extension-during-its-development"></a>拡張機能の開発段階での実行  
  
#### <a name="to-run-an-extension-during-its-development"></a>拡張機能を開発段階において実行するには  
  
1.  [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)] **デバッグ**] メニューの [選択**デバッグの開始**します。  
  
     プロジェクトがビルドされ、 [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)] の新しいインスタンスが実験モードで起動されます。  
  
    -   または、 **[デバッグなしで開始]** を選択することもできます。 これにより、プログラムの起動時間が短縮されます。  
  
2.  Visual Studio の実験用のインスタンスでモデリング プロジェクトを生成または開き、図を生成または開きます。  
  
     拡張機能が読み込まれて実行されます。  
  
3.  **[デバッグなしで開始]** を使用したがデバッガーを使用する必要がある場合は、Visual Studio のメイン インスタンスに戻ります。 **[デバッグ]** メニューの **[プロセスにアタッチ]** をクリックします。 ダイアログ ボックスで、Visual Studio の実験用インスタンスを選択します。プログラム名は **devenv**です。  
  
##  <a name="Installing"></a> インストールして、拡張機能をアンインストールします。  
 自分のコンピューターまたは他のコンピューターにおいて Visual Studio のメイン インスタンスで拡張機能を実行するには、次の手順を実行します。  
  
1.  自分のコンピューターで、拡張機能プロジェクトによってビルドされた **.vsix** ファイルを見つけます。  
  
    1.  **ソリューション エクスプローラー**で、プロジェクトのショートカット メニューを開き、 **[エクスプローラーでフォルダーを開く]** をクリックします。  
  
    2.  ファイルを見つけます**bin\\\*\\**_プロジェクト_**.vsix**  
  
2.  拡張機能をインストールする対象のコンピューターに **.vsix** ファイルをコピーします。 自分のコンピューターでも別のコンピューターでもかまいません。  
  
    -   ターゲット コンピューターは、 **source.extension.vsixmanifest** の **[Installation Targets]**(インストールの対象) タブで指定した Visual Studio のいずれかのエディションを搭載している必要があります。  
  
3.  ターゲット コンピューターで **.vsix** ファイルを開きます。たとえば、ダブルクリックして開きます。  
  
     **Visual Studio 拡張機能インストーラー** が起動され、拡張機能がインストールされます。  
  
4.  Visual Studio を起動または再起動します。  
  
#### <a name="to-uninstall-an-extension"></a>拡張機能をアンインストールするには  
  
1. **[ツール]** メニューの **[拡張機能と更新プログラム]** をクリックします。  
  
2. **[インストール済みの拡張機能]** を展開します。  
  
3. 拡張機能を選択し、 **[アンインストール]** をクリックします。  
  
   拡張機能の障害が原因で読み込みが失敗し、エラー ウィンドウにレポートが生成されることがまれにありますが、それは拡張機能マネージャーには表示されません。 次の場所からファイルを削除することによって、拡張機能を削除する場合、場所 *%localappdata%* は通常*DriveName*: \Users\\*ユーザー名*\AppData\Local:  
  
   *%Localappdata%* **\Microsoft\VisualStudio\\[バージョン] \Extensions**  
  
## <a name="see-also"></a>関連項目  
 [プロファイルを定義すると、UML を拡張](../modeling/define-a-profile-to-extend-uml.md)   
 [定義のカスタム モデリング ツールボックス アイテム](../modeling/define-a-custom-modeling-toolbox-item.md)   
 [UML モデルの検証制約を定義します。](../modeling/define-validation-constraints-for-uml-models.md)   
 [モデリング図にメニュー コマンドを定義する](../modeling/define-a-menu-command-on-a-modeling-diagram.md)



