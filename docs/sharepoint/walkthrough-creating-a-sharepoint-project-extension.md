---
title: 'チュートリアル: SharePoint プロジェクトの拡張機能の作成 | Microsoft Docs'
description: SharePoint プロジェクトの拡張機能を作成します。この拡張機能を使用すると、プロジェクトが追加、削除、または名前変更されたときなどのプロジェクトレベルのイベントに応答できます。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- projects [SharePoint development in Visual Studio], extending
- SharePoint development in Visual Studio, extending projects
- SharePoint projects, extending
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 1de6cdc2f5c1f1480a738f99aa05b8833eb4b2ed
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/02/2021
ms.locfileid: "106217793"
---
# <a name="walkthrough-create-a-sharepoint-project-extension"></a>チュートリアル: SharePoint プロジェクトの拡張機能を作成する
  このチュートリアルでは、SharePoint プロジェクトの拡張機能を作成する方法について説明します。 プロジェクトの拡張機能を使用して、プロジェクトが追加、削除、または名前変更されたときなどのプロジェクトレベルのイベントに応答できます。 また、カスタム プロパティを追加したり、プロパティ値が変更したときに応答したりすることもできます。 プロジェクト項目の拡張機能とは異なり、プロジェクトの拡張機能を特定の SharePoint プロジェクトの種類に関連付けることはできません。 プロジェクト拡張機能を作成すると、[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] で任意の種類の SharePoint プロジェクトが開かれたときに、拡張機能が読み込まれます。

 このチュートリアルでは、[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] で作成した任意の SharePoint プロジェクトに追加されるカスタムのブール型プロパティを作成し ます。 **True** に設定すると、新しいプロパティによって、Images リソース フォルダーがプロジェクトに追加されるか、マップされます。 **False** に設定すると、Images フォルダーが存在する場合は削除されます。 詳細については、「[方法: マップされたフォルダーの追加と削除を行う](../sharepoint/how-to-add-and-remove-mapped-folders.md)」を参照してください。

 このチュートリアルでは、次のタスクについて説明します。

- 次の操作を行う SharePoint プロジェクト用の [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 拡張機能の作成。

  - カスタム プロジェクト プロパティをプロパティ ウィンドウに追加する。 プロパティはすべての SharePoint プロジェクトに適用されます。

  - SharePoint プロジェクト オブジェクト モデルを使用して、マップされたフォルダーをプロジェクトに追加する。

  - [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] オートメーション オブジェクト モデル (DTE) を使用して、マップされたフォルダーをプロジェクトから削除する。

- プロジェクト プロパティの拡張機能アセンブリを配置するための [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] Extension (VSIX) パッケージの作成。

- プロジェクト プロパティのデバッグおよびテスト。

## <a name="prerequisites"></a>必須コンポーネント
 このチュートリアルを実行するには、開発コンピューターに次のコンポーネントが必要です。

- サポートされている [!INCLUDE[TLA#tla_win](../sharepoint/includes/tlasharptla-win-md.md)]、SharePoint、[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] のエディション。

- [!INCLUDE[vssdk_current_long](../sharepoint/includes/vssdk-current-long-md.md)]。 このチュートリアルでは、プロジェクト プロパティの拡張機能を配置するための VSIX パッケージを、[!INCLUDE[TLA2#tla_sdk](../sharepoint/includes/tla2sharptla-sdk-md.md)] の **VSIX プロジェクト** テンプレートを使用して作成します。 詳細については、「[Visual Studio での SharePoint ツールの拡張](../sharepoint/extending-the-sharepoint-tools-in-visual-studio.md)」を参照してください。

## <a name="create-the-projects"></a>プロジェクトを作成する
 このチュートリアルを完了するには、2 つのプロジェクトを作成する必要があります。

- プロジェクト拡張機能を配置するために VSIX パッケージを作成する VSIX プロジェクト。

- プロジェクト拡張機能を実装するクラス ライブラリ プロジェクト。

  この 2 つのプロジェクトを作成することから始めます。

#### <a name="to-create-the-vsix-project"></a>VSIX プロジェクトを作成するには

1. [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]を起動します。

2. メニュー バーで、 **[ファイル]**  >  **[新規作成]**  >  **[プロジェクト]** を選択します。

3. **[新しいプロジェクト]** ダイアログ ボックスで、 **[Visual C#]** ノードまたは **[Visual Basic]** ノードを展開し、 **[機能拡張]** ノードをクリックします。

    > [!NOTE]
    > このノードは、Visual Studio SDK がインストールされている場合にのみ使用できます。 詳細については、このトピックで前に説明した「前提条件」を参照してください。

4. ダイアログ ボックスの上部にある .NET Framework のバージョンの一覧で **[.NET Framework 4.5]** を選択し、 **[VSIX プロジェクト]** テンプレートをクリックします。

5. **[名前]** ボックスに「**ProjectExtensionPackage**」と入力し、 **[OK]** をクリックします。

     **ソリューション エクスプローラー** に **ProjectExtensionPackage** プロジェクトが表示されます。

#### <a name="to-create-the-extension-project"></a>拡張機能プロジェクトを作成するには

1. **ソリューション エクスプローラー** でソリューション ノードのショートカット メニューを開き、 **[追加]** 、 **[新しいプロジェクト]** の順に選択します。

2. **[新しいプロジェクト]** ダイアログ ボックスで、 **[Visual C#]** ノードまたは **[Visual Basic]** ノードを展開し、 **[Windows]** をクリックします。

3. ダイアログ ボックスの上部にある .NET Framework のバージョンの一覧で **[.NET Framework 4.5]** を選択し、 **[クラス ライブラリ]** プロジェクト テンプレートをクリックします。

4. **[名前]** ボックスに「**ProjectExtension**」と入力し、 **[OK]** をクリックします。

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] によって、**ProjectExtension** プロジェクトがソリューションに追加され、既定の Class1 コード ファイルが開きます。

5. Class1 コード ファイルをプロジェクトから削除します。

## <a name="configure-the-project"></a>プロジェクトを構成する
 プロジェクト拡張機能を作成するためのコードを記述する前に、コード ファイルおよびアセンブリ参照を拡張プロジェクトに追加します。

#### <a name="to-configure-the-project"></a>プロジェクトを構成するには

1. **CustomProperty** という名前のコード ファイルを ProjectExtension プロジェクトに追加します。

2. **ProjectExtension** プロジェクトのショートカット メニューを開いてから、 **[参照の追加]** を選択します。

3. **[参照マネージャー - CustomProperty]** ダイアログ ボックスで、 **[フレームワーク]** ノードを選択し、System.ComponentModel.Composition アセンブリと System.Windows.Forms アセンブリの横にあるチェック ボックスをオンにします。

4. **[拡張機能]** ノードを選択し、Microsoft.VisualStudio.SharePoint アセンブリと EnvDTE アセンブリの横にあるチェック ボックスをオンにして、 **[OK]** をクリックします。

5. **ソリューション エクスプローラー** で、 **[ProjectExtension]** プロジェクトの **[参照設定]** フォルダーの下の **[EnvDTE]** をクリックします。

6. **[プロパティ]** ウィンドウで、"**相互運用機能型の埋め込み**" プロパティを **[False]** に変更します。

## <a name="define-the-new-sharepoint-project-property"></a>新しい SharePoint プロジェクト プロパティを定義する
 プロジェクト拡張機能と新しいプロジェクト プロパティの動作を定義するクラスを作成します。 新しいプロジェクト拡張機能を定義するため、このクラスに <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectExtension> インターフェイスを実装します。 SharePoint プロジェクトの拡張機能を定義する場合は、常にこのインターフェイスを実装します。 また、<xref:System.ComponentModel.Composition.ExportAttribute> もクラスに追加します。 この属性を使用すると、[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] で <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectExtension> 実装を検出して読み込むことができます。 属性のコンストラクターに <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectExtension> 型を渡します。

#### <a name="to-define-the-new-sharepoint-project-property"></a>新しい SharePoint プロジェクト プロパティを定義するには

1. 次のコードを CustomProperty コード ファイルに貼り付けます。

     :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/projectextension/customproperty.vb" id="Snippet1":::
     :::code language="csharp" source="../sharepoint/codesnippet/CSharp/projectextension/customproperty.cs" id="Snippet1":::

## <a name="build-the-solution"></a>ソリューションをビルドする
 次に、ソリューションをビルドして、エラーが発生することなくコンパイルできるかどうかを確認します。

#### <a name="to-build-the-solution"></a>ソリューションをビルドするには

1. メニュー バーで、 **[ビルド]**  >  **[ソリューションのビルド]** の順にクリックします。

## <a name="create-a-vsix-package-to-deploy-the-project-property-extension"></a>プロジェクト プロパティの拡張機能を配置するために VSIX パッケージを作成する
 プロジェクト拡張機能を配置するには、ソリューションで VSIX プロジェクトを使用して VSIX パッケージを作成します。 まず、VSIX プロジェクトに含まれている source.extension.vsixmanifest ファイルを変更して、VSIX パッケージを構成します。 次に、ソリューションをビルドして VSIX パッケージを作成します。

#### <a name="to-configure-and-create-the-vsix-package"></a>VSIX パッケージを構成および作成するには

1. **ソリューション エクスプローラー** で、source.extension.vsixmanifest ファイルのショートカット メニューを開き、 **[開く]** をクリックします。

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] により、マニフェスト デザイナーにファイルが開きます。 **[メタデータ]** タブに表示される情報は、 **[拡張機能と更新プログラム]** にも表示されます。 すべての VSIX パッケージに extension.vsixmanifest ファイルが必要です。 このファイルの詳細については、「[VSIX 拡張機能スキーマ 1.0 リファレンス](/previous-versions/dd393700(v=vs.110))」を参照してください。

2. **[プロジェクト名]** ボックスに「**Custom Project Property**」と入力します。

3. **[作成者]** ボックスに、「**Contoso**」と入力します。

4. **[説明]** ボックスに、「**A custom SharePoint project property that toggles the mapping of the Images resource folder to the project**」(Images リソース フォルダーのプロジェクトへのマッピングを切り替えるカスタム SharePoint プロジェクト プロパティ) と入力します。

5. **[アセット]** タブをクリックし、 **[新規作成]** をクリックします。

     **[新しい資産の追加]** ダイアログ ボックスが表示されます。

6. **[種類]** ボックスの一覧で、 **[Microsoft.VisualStudio.MefComponent]** を選択します。

    > [!NOTE]
    > この値は、extension.vsixmanifest ファイル内の `MEFComponent` 要素に対応します。 この要素は、VSIX パッケージ内の拡張機能アセンブリの名前を指定します。 詳細については、「[MEFComponent 要素 (VSX スキーマ)](/previous-versions/visualstudio/visual-studio-2010/dd393736\(v\=vs.100\))」を参照してください。

7. **[ソース]** ボックスの一覧で、 **[現在のソリューション内のプロジェクト]** オプション ボタンをクリックします。

8. **[プロジェクト]** ボックスの一覧で、 **[ProjectExtension]** を選択します。

     この値は、プロジェクトでビルドしているアセンブリの名前を識別します。

9. **[OK]** をクリックして、 **[新しい資産の追加]** ダイアログ ボックスを閉じます。

10. メニュー バーで、 **[ファイル]**  >  **[すべてを保存]** の順に選択し、完了したらマニフェスト デザイナーを閉じます。

11. メニュー バーで **[ビルド]**  >  **[ソリューションのビルド]** の順にクリックし、プロジェクトがエラーなしでコンパイルされたことを確認します。

12. **ソリューション エクスプローラー** で、**ProjectExtensionPackage** プロジェクトのショートカット メニューを開き、 **[エクスプローラーでフォルダーを開く]** をクリックします。

13. **ファイル エクスプローラー** で、ProjectExtensionPackage プロジェクトのビルド出力フォルダーを開き、フォルダーに ProjectExtensionPackage.vsix という名前のファイルが含まれていることを確認します。

     既定では、ビルド出力フォルダーは ..\bin\Debug で、プロジェクト ファイルが格納されているフォルダーの下にあります。

## <a name="test-the-project-property"></a>プロジェクト プロパティをテストする
 これで、カスタム プロジェクト プロパティをテストする準備ができました。 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] の実験用インスタンスで、新しいプロジェクト プロパティ拡張機能のデバッグとテストを行うことが最も簡単です。 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] のこのインスタンスは、VSIX または他の機能拡張プロジェクトを実行するときに作成されます。 プロジェクトをデバッグした後、拡張機能をシステムにインストールし、[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] の通常のインスタンスでデバッグとテストを続行できます。

#### <a name="to-debug-and-test-the-extension-in-an-experimental-instance-of-visual-studio"></a>Visual Studio の実験用インスタンスで拡張機能をデバッグしテストするには

1. 管理者の資格情報で [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] を再起動し、ProjectExtensionPackage ソリューションを開きます。

2. **F5** キーを押すか、メニュー バーで **[デバッグ]**  >  **[デバッグの開始]** の順に選択して、プロジェクトのデバッグ ビルドを開始します。

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] によって、拡張機能が %UserProfile%\AppData\Local\Microsoft\VisualStudio\11.0Exp\Extensions\Contoso\Custom Project Property\1.0 にインストールされ、[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] の実験用インスタンスが開始されます。

3. [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] の実験用インスタンスで、ファーム ソリューション用の SharePoint プロジェクトを作成し、ウィザードでのその他の値に既定値を使用します。

    1. メニュー バーで、 **[ファイル]**  >  **[新規作成]**  >  **[プロジェクト]** を選択します。

    2. **[新しいプロジェクト]** ダイアログ ボックスの上部にある .NET Framework のバージョンの一覧で **[.NET Framework 3.5]** を選択します。

         SharePoint ツールの拡張機能を使用するには、このバージョンの [!INCLUDE[dnprdnshort](../sharepoint/includes/dnprdnshort-md.md)] のフィーチャーが必要です。

    3. **[テンプレート]** ノードで、 **[Visual C#]** ノードまたは **[Visual Basic]** ノードを展開し、 **[SharePoint]** ノードを選択してから、 **[2010]** ノードを選択します。

    4. **[SharePoint 2010 プロジェクト]** テンプレートを選択し、プロジェクトの名前として「**ModuleTest**」と入力します。

4. **ソリューション エクスプローラー** で、 **[ModuleTest]** プロジェクト ノードを選択します。

     **[プロパティ]** ウィンドウに、新しいカスタム プロパティ **[マップ イメージ フォルダー]** が **False** の既定値で表示されます。

5. そのプロパティの値を **True** に変更します。

     Images リソース フォルダーが SharePoint プロジェクトに追加されます。

6. そのプロパティの値を **False** に戻します。

     **[Images フォルダーを削除しますか?]** ダイアログ ボックスで **[はい]** をクリックすると、SharePoint プロジェクトから Images リソース フォルダーが削除されます。

7. [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] の実験用インスタンスを閉じます。

## <a name="see-also"></a>関連項目
- [SharePoint プロジェクトを拡張する](../sharepoint/extending-sharepoint-projects.md)
- [方法: SharePoint プロジェクトにプロパティを追加する](../sharepoint/how-to-add-a-property-to-sharepoint-projects.md)
- [SharePoint プロジェクト システムの種類とその他の Visual Studio プロジェクトの種類の変換](../sharepoint/converting-between-sharepoint-project-system-types-and-other-visual-studio-project-types.md)
- [SharePoint プロジェクト システムの拡張機能にデータを保存する](../sharepoint/saving-data-in-extensions-of-the-sharepoint-project-system.md)
- [カスタム データを SharePoint ツール拡張機能に関連付ける](../sharepoint/associating-custom-data-with-sharepoint-tools-extensions.md)