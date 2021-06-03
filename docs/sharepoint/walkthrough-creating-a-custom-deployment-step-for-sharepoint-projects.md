---
title: SharePoint プロジェクトのカスタムの配置手順を作成する
description: このチュートリアルでは、SharePoint を実行しているサーバーで SharePoint プロジェクト ソリューションをアップグレードするカスタム配置手順を作成します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint commands
- SharePoint development in Visual Studio, extending deployment
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 77c80134ad63346b363c072ef2eff7e49978501f
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/02/2021
ms.locfileid: "106217932"
---
# <a name="walkthrough-create-a-custom-deployment-step-for-sharepoint-projects"></a>チュートリアル: SharePoint プロジェクトのカスタムの配置手順を作成する
  SharePoint プロジェクトを配置すると、Visual Studio により一連の配置手順が一定の順序で実行されます。 Visual Studio には多くの配置手順が組み込まれていますが、独自の手順を作成することもできます。

 このチュートリアルでは、SharePoint を実行しているサーバーでソリューションをアップグレードするカスタム配置手順を作成します。 Visual Studio には、ソリューションの取り消しや追加など、多くのタスクに対する配置手順が組み込まれていますが、ソリューションをアップグレードするための配置手順は含まれていません。 既定では、SharePoint ソリューションを配置すると、Visual Studio ではまずソリューションが取り消され (既に配置されている場合)、ソリューション全体が再配置されます。 組み込み配置手順の詳細については、「[SharePoint ソリューション パッケージの配置、発行、およびアップグレードを行う](../sharepoint/deploying-publishing-and-upgrading-sharepoint-solution-packages.md)」を参照してください。

 このチュートリアルでは、次のタスクについて説明します。

- 次の 2 つの主要タスクを実行する Visual Studio の拡張機能を作成する。

  - 拡張機能によって、SharePoint ソリューションをアップグレードするカスタム配置手順が定義されます。

  - この拡張機能により、新しい配置構成を定義するプロジェクト拡張機能が作成されます。この配置構成は、特定のプロジェクトに対して実行される一連の配置手順になります。 新しい配置構成には、カスタム配置手順といくつかの組み込み配置手順が含まれます。

- 拡張機能アセンブリで呼び出される 2 つのカスタム SharePoint コマンドを作成する。 SharePoint コマンドは、SharePoint のサーバー オブジェクト モデルで API を使用するために拡張機能アセンブリで呼び出されるメソッドです。 詳細については、[SharePoint オブジェクト モデルの呼び出し](../sharepoint/calling-into-the-sharepoint-object-models.md)に関するページを参照してください。

- 両方のアセンブリを配置するための Visual Studio Extension (VSIX) パッケージを構築する。

- 新しい配置手順をテストする。

## <a name="prerequisites"></a>必須コンポーネント
 このチュートリアルを実行するには、開発コンピューターに次のコンポーネントが必要です。

- サポート対象エディションの Windows、SharePoint、Visual Studio。

- Visual Studio SDK。 このチュートリアルでは、拡張機能を配置するための VSIX パッケージを、SDK の **VSIX プロジェクト** テンプレートを使用して作成します。 詳細については、「[Visual Studio での SharePoint ツールの拡張](../sharepoint/extending-the-sharepoint-tools-in-visual-studio.md)」を参照してください。

  次の概念に関する知識があると役に立ちますが、チュートリアルを実行するうえで必須というわけではありません。

- SharePoint のサーバー オブジェクト モデルの使用。 詳細については、「[SharePoint Foundation サーバー側のオブジェクト モデルを使用する](/previous-versions/office/developer/sharepoint-2010/ee538251(v=office.14))」を参照してください。

- SharePoint ソリューション。 詳細については、「[ソリューションの概要](/previous-versions/office/developer/sharepoint-2010/aa543214(v=office.14))」を参照してください。

- SharePoint ソリューションのアップグレード。 詳細については、「[ファーム ソリューションをアップグレードする](/previous-versions/office/developer/sharepoint-2010/aa543659(v=office.14))」を参照してください。

## <a name="create-the-projects"></a>プロジェクトを作成する
 このチュートリアルを完了するには、3 つのプロジェクトを作成する必要があります。

- 拡張機能を配置するために VSIX パッケージを作成する VSIX プロジェクト。

- 拡張機能を実装するクラス ライブラリ プロジェクト。 このプロジェクトは .NET Framework 4.5 を対象にする必要があります。

- カスタム SharePoint コマンドを定義するクラス ライブラリ プロジェクト。 このプロジェクトは .NET Framework 3.5 を対象にする必要があります。

  この 2 つのプロジェクトを作成することから始めます。

#### <a name="to-create-the-vsix-project"></a>VSIX プロジェクトを作成するには

1. [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]を起動します。

2. メニュー バーで、 **[ファイル]**  >  **[新規作成]**  >  **[プロジェクト]** を選択します。

3. **[新しいプロジェクト]** ダイアログ ボックスで、 **[Visual C#]** ノードまたは **[Visual Basic]** ノードを展開し、 **[機能拡張]** ノードをクリックします。

    > [!NOTE]
    > **[機能拡張]** ノードは、Visual Studio SDK がインストールされている場合にのみ使用できます。 詳細については、このトピックで前に説明した「前提条件」を参照してください。

4. ダイアログ ボックスの上部にある .NET Framework のバージョンの一覧で **[.NET Framework 4.5]** を選択します。

5. **[VSIX プロジェクト]** テンプレートを選択し、プロジェクトに **UpgradeDeploymentStep** という名前を付けて、 **[OK]** をクリックします。

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] により、**ソリューション エクスプローラー** に **UpgradeDeploymentStep** プロジェクトが追加されます。

#### <a name="to-create-the-extension-project"></a>拡張機能プロジェクトを作成するには

1. **ソリューション エクスプローラー** で [UpgradeDeploymentStep] ソリューション ノードのショートカット メニューを開き、 **[追加]** 、 **[新しいプロジェクト]** の順に選択します。

2. **[新しいプロジェクト]** ダイアログ ボックスで、 **[Visual C#]** ノードまたは **[Visual Basic]** ノードを展開し、 **[Windows]** ノードをクリックします。

3. ダイアログ ボックスの上部にある .NET Framework のバージョンの一覧で **[.NET Framework 4.5]** を選択します。

4. **[クラス ライブラリ]** プロジェクト テンプレートを選択し、プロジェクトに **DeploymentStepExtension** という名前を付けて、 **[OK]** をクリックします。

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] によって、**DeploymentStepExtension** プロジェクトがソリューションに追加され、既定の Class1 コード ファイルが開きます。

5. Class1 コード ファイルをプロジェクトから削除します。

#### <a name="to-create-the-sharepoint-command-project"></a>SharePoint コマンド プロジェクトを作成するには

1. **ソリューション エクスプローラー** で [UpgradeDeploymentStep] ソリューション ノードのショートカット メニューを開き、 **[追加]** 、 **[新しいプロジェクト]** の順に選択します。

2. **[新しいプロジェクト]** ダイアログ ボックスで、 **[Visual C#]** または **[Visual Basic]** を展開し、 **[Windows]** ノードをクリックします。

3. ダイアログ ボックスの上部にある .NET Framework のバージョンの一覧で **[.NET Framework 3.5]** を選択します。

4. **[クラス ライブラリ]** プロジェクト テンプレートを選択し、プロジェクトに **SharePointCommands** という名前を付けて、 **[OK]** をクリックします。

     Visual Studio によって、**SharePointCommands** プロジェクトがソリューションに追加され、既定の Class1 コード ファイルが開きます。

5. Class1 コード ファイルをプロジェクトから削除します。

## <a name="configure-the-projects"></a>プロジェクトを構成する
 カスタム配置手順を作成するコードを記述する前に、コード ファイルとアセンブリ参照を追加し、プロジェクトを構成する必要があります。

#### <a name="to-configure-the-deploymentstepextension-project"></a>DeploymentStepExtension プロジェクトを構成するには

1. **DeploymentStepExtension** プロジェクトに、次の名前を持つ 2 つのコード ファイルを追加します。

    - UpgradeStep

    - DeploymentConfigurationExtension

2. DeploymentStepExtension プロジェクトのショートカット メニューを開き、 **[参照の追加]** を選択します。

3. **[フレームワーク]** タブで、System.ComponentModel.Composition アセンブリのチェック ボックスをオンにします。

4. **[拡張機能]** タブで、Microsoft.VisualStudio.SharePoint アセンブリのチェック ボックスをオンにして、 **[OK]** をクリックします。

#### <a name="to-configure-the-sharepointcommands-project"></a>SharePointCommands プロジェクトを構成するには

1. **SharePointCommands** プロジェクトに、Commands というコード ファイルを追加します。

2. **ソリューション エクスプローラー** で、 **[SharePointCommands]** プロジェクト ノードのショートカット メニューを開き、 **[参照の追加]** をクリックします。

3. **[拡張機能]** タブで、次のアセンブリのチェック ボックスをオンにして、 **[OK]** をクリックします

    - Microsoft.SharePoint

    - Microsoft.VisualStudio.SharePoint.Commands

## <a name="define-the-custom-deployment-step"></a>カスタム配置手順を定義する
 アップグレード配置手順を定義するクラスを作成します。 配置手順を定義するために、このクラスでは <xref:Microsoft.VisualStudio.SharePoint.Deployment.IDeploymentStep> インターフェイスを実装します。 カスタム配置手順を定義する場合は、常にこのインターフェイスを実装します。

#### <a name="to-define-the-custom-deployment-step"></a>カスタム配置手順を定義するには

1. **DeploymentStepExtension** プロジェクトで、UpgradeStep コード ファイルを開き、次のコードを貼り付けます。

    > [!NOTE]
    > このコードを追加すると、プロジェクトにコンパイル エラーが発生しますが、後の手順でコードを追加したときに、そのエラーは解消されます。

     :::code language="csharp" source="../sharepoint/codesnippet/CSharp/UpgradeDeploymentStep/deploymentstepextension/upgradestep.cs" id="Snippet1":::
     :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/upgradedeploymentstep/deploymentstepextension/upgradestep.vb" id="Snippet1":::

## <a name="create-a-deployment-configuration-that-includes-the-custom-deployment-step"></a>カスタム配置手順を含む配置構成を作成する
 新しい配置構成のプロジェクト拡張機能を作成します。これには、いくつかの組み込み配置手順と新しいアップグレード配置手順が含まれます。 この拡張機能を作成することにより、SharePoint 開発者は SharePoint プロジェクトのアップグレード配置手順を使用することができます。

 配置構成を作成するために、このクラスでは <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectExtension> インターフェイスを実装します。 SharePoint プロジェクト拡張機能を作成する場合は、常にこのインターフェイスを実装します。

#### <a name="to-create-the-deployment-configuration"></a>配置構成を作成するには

1. **DeploymentStepExtension** プロジェクトで DeploymentConfigurationExtension コード ファイルを開き、次のコードを貼り付けます。

     :::code language="csharp" source="../sharepoint/codesnippet/CSharp/UpgradeDeploymentStep/deploymentstepextension/deploymentconfigurationextension.cs" id="Snippet2":::
     :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/upgradedeploymentstep/deploymentstepextension/deploymentconfigurationextension.vb" id="Snippet2":::

## <a name="create-the-custom-sharepoint-commands"></a>カスタム SharePoint コマンドを作成する
 SharePoint のサーバー オブジェクト モデルを呼び出す 2 つのカスタム コマンドを作成します。 1 つのコマンドは、ソリューションが既に配置されているかどうかを判断します。もう 1 つのコマンドは、ソリューションをアップグレードします。

#### <a name="to-define-the-sharepoint-commands"></a>SharePoint コマンドを定義するには

1. **SharePointCommands** プロジェクトで Commands コード ファイルを開き、それに次のコードを貼り付けます。

     :::code language="csharp" source="../sharepoint/codesnippet/CSharp/UpgradeDeploymentStep/SharePointCommands/Commands.cs" id="Snippet4":::
     :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/upgradedeploymentstep/sharepointcommands/commands.vb" id="Snippet4":::

## <a name="checkpoint"></a>Checkpoint
 チュートリアルのこの時点で、カスタム配置手順と SharePoint コマンドのすべてのコードがプロジェクトに含まれています。 これらをビルドして、エラーが発生することなくコンパイルできるかどうかを確認してください。

#### <a name="to-build-the-projects"></a>プロジェクトをビルドするには

1. **ソリューション エクスプローラー** で、**DeploymentStepExtension** プロジェクトのショートカット メニューを開き、 **[ビルド]** をクリックします。

2. **SharePointCommands** プロジェクトのショートカット メニューを開き、 **[ビルド]** をクリックします。

## <a name="create-a-vsix-package-to-deploy-the-extension"></a>拡張機能を配置するための VSIX パッケージを作成する
 拡張機能を配置するには、ソリューションで VSIX プロジェクトを使用して VSIX パッケージを作成します。 まず、VSIX プロジェクトの source.extension.vsixmanifest ファイルを変更して、VSIX パッケージを構成します。 次に、ソリューションをビルドして VSIX パッケージを作成します。

#### <a name="to-configure-and-create-the-vsix-package"></a>VSIX パッケージを構成および作成するには

1. **ソリューション エクスプローラー** の **UpgradeDeploymentStep** プロジェクトで、**source.extension.vsixmanifest** ファイルのショートカット メニューを開き、 **[開く]** をクリックします。

     Visual Studio によってマニフェスト エディターでファイルが開きます。 source.extension.vsixmanifest ファイルが、すべての VSIX パッケージで必要になる extension.vsixmanifest ファイルの基礎となります。 このファイルの詳細については、「[VSIX 拡張機能スキーマ 1.0 リファレンス](/previous-versions/dd393700(v=vs.110))」を参照してください。

2. **[製品名]** ボックスに、「**Upgrade Deployment Step for SharePoint Projects**」(SharePoint プロジェクトのアップグレードの配置手順) と入力します。

3. **[作成者]** ボックスに、「**Contoso**」と入力します。

4. **[説明]** ボックスに「**Provides a custom upgrade deployment step that can be used in SharePoint projects**」(SharePoint プロジェクトで使用できるカスタム アップグレード配置手順を提供します) と入力します。

5. エディターの **[アセット]** タブで、 **[新規作成]** をクリックします。

     **[新しい資産の追加]** ダイアログ ボックスが表示されます。

6. **[種類]** ボックスの一覧で、 **[Microsoft.VisualStudio.MefComponent]** を選択します。

    > [!NOTE]
    > この値は、extension.vsixmanifest ファイル内の `MefComponent` 要素に対応します。 この要素は、VSIX パッケージ内の拡張機能アセンブリの名前を指定します。 詳細については、「[MEFComponent 要素 (VSX スキーマ)](/previous-versions/visualstudio/visual-studio-2010/dd393736\(v\=vs.100\))」を参照してください。

7. **[ソース]** ボックスの一覧で、 **[現在のソリューション内のプロジェクト]** を選択します。

8. **[プロジェクト]** ボックスの一覧で **[DeploymentStepExtension]** を選択し、 **[OK]** をクリックします。

9. マニフェスト エディターで、 **[新規作成]** をもう一度クリックします。

     **[新しい資産の追加]** ダイアログ ボックスが表示されます。

10. **[種類]** ボックスの一覧に「**SharePoint.Commands.v4**」と入力します。

    > [!NOTE]
    > この要素により、Visual Studio 拡張機能に含めるカスタム拡張機能が指定されます。 詳細については、[Asset 要素 (VSX スキーマ)](/previous-versions/dd393737(v=vs.110)) に関するページを参照してください。

11. **[ソース]** ボックスの一覧で、 **[現在のソリューション内のプロジェクト]** を選択します。

12. **[プロジェクト]** ボックスの一覧で **[SharePointCommands]** プロジェクトを選択し、 **[OK]** をクリックします。

13. メニュー バーで **[ビルド]**  >  **[ソリューションのビルド]** の順に選択し、ソリューションがエラーなしでコンパイルされることを確認します。

14. UpgradeDeploymentStep プロジェクトのビルド出力フォルダーに、UpgradeDeploymentStep.vsix ファイルが含まれていることを確認します。

     既定では、ビルド出力フォルダーは ..\bin\Debug で、プロジェクト ファイルが格納されているフォルダーの下にあります。

## <a name="prepare-to-test-the-upgrade-deployment-step"></a>アップグレード配置手順のテストを準備する
 アップグレード配置手順をテストするには、最初にサンプル ソリューションを SharePoint サイトに配置する必要があります。 まず、Visual Studio の実験用インスタンスで拡張機能をデバッグします。 続いて、配置手順をテストするために使用するリスト定義とリスト インスタンスを作成し、SharePoint サイトに配置します。 次に、リスト定義とリスト インスタンスを変更し、それらを再配置して、既定の配置プロセスで SharePoint サイトのソリューションを上書きする方法を示します。

 このチュートリアルの後半で、リスト定義とリスト インスタンスを変更し、SharePoint サイトでそれらをアップグレードします。

#### <a name="to-start-debugging-the-extension"></a>拡張機能のデバッグを開始するには

1. 管理者の資格情報で Visual Studio を再起動し、UpgradeDeploymentStep ソリューションを開きます。

2. DeploymentStepExtension プロジェクトで、UpgradeStep コード ファイルを開き、`CanExecute` メソッドと `Execute` メソッド内の最初のコード行にブレークポイントを追加します。

3. **F5** キーを押すかメニュー バーで **[デバッグ]**  >  **[デバッグ開始]** の順に選択して、デバッグを開始します。

4. Visual Studio によって、拡張機能が %UserProfile%\AppData\Local\Microsoft\VisualStudio\11.0Exp\Extensions\Contoso\Upgrade Deployment Step for SharePoint Projects\1.0 にインストールされ、Visual Studio の実験用インスタンスが開始されます。 Visual Studio のこのインスタンスで、アップグレード配置手順をテストします。

#### <a name="to-create-a-sharepoint-project-with-a-list-definition-and-a-list-instance"></a>リスト定義とリスト インスタンスを使用して SharePoint プロジェクトを作成するには

1. Visual Studio の実験用インスタンスのメニュー バーで **[ファイル]**  >  **[新規作成]**  >  **[プロジェクト]** の順に選択します。

2. **[新しいプロジェクト]** ダイアログ ボックスで、 **[Visual C#]** ノードまたは **[Visual Basic]** ノード、 **[SharePoint]** ノードの順に展開し、 **[2010]** ノードをクリックします。

3. ダイアログ ボックスの上部にある .NET Framework のバージョンの一覧で、 **.NET Framework 3.5** が表示されていることを確認します。

    [!INCLUDE[wss_14_long](../sharepoint/includes/wss-14-long-md.md)] および [!INCLUDE[moss_14_long](../sharepoint/includes/moss-14-long-md.md)] のプロジェクトには、このバージョンの .NET Framework が必要です。

4. プロジェクト テンプレートの一覧で **[SharePoint 2010 プロジェクト]** を選択し、プロジェクトに **EmployeesListDefinition** という名前を付けて、 **[OK]** をクリックします。

5. **SharePoint カスタマイズ ウィザード** で、デバッグに使用するサイトの URL を入力します。

6. **[この SharePoint ソリューションの信頼レベル]** の下で、 **[ファーム ソリューションとして配置する]** オプション ボタンをクリックします。

   > [!NOTE]
   > アップグレード配置手順では、サンドボックス ソリューションはサポートしていません。

7. **[完了]** をクリックします。

    [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]により、EmployeesListDefinition プロジェクトが作成されます。

8. EmployeesListDefinition プロジェクトのショートカット メニューを開き、 **[追加]** 、 **[新しい項目]** の順に選択します。

9. **[新しい項目の追加 - EmployeesListDefinition]** ダイアログ ボックスで、 **[SharePoint]** ノードを展開し、 **[2010]** ノードを選択します。

10. **[リスト]** 項目テンプレートを選択し、項目に「**従業員リスト**」の名前を付け、 **[追加]** をクリックします。

     SharePoint カスタマイズ ウィザードが表示されます

11. **[リストの設定を選択]** ページで、次の設定を確認し、 **[完了]** をクリックします。

    1. **[リストの表示名]** ボックスに「**従業員リスト**」と表示されます。

    2. **[次に基づいてカスタマイズ可能なリストを作成:]** オプション ボタンが選択されます。

    3. **[次に基づいてカスタマイズ可能なリストを作成:]** ボックスの一覧で、 **[既定 (空白)]** が選択されます。

       [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] により、[従業員リスト] 項目が [タイトル] 列および空の単一のインスタンスとともに作成され、リスト デザイナーが開きます。

12. リスト デザイナーの **[列]** タブで、 **[新規または既存の列名を入力します]** 行を選択し、 **[列の表示名]** ボックスの一覧に次の列を追加します。

    1. 名

    2. [会社]

    3. Business Phone (勤務先電話番号)

    4. 電子メール

13. すべてのファイルを保存し、リスト デザイナーを閉じます。

14. **[ソリューション エクスプローラー]** で、 **[従業員リスト]** ノードを展開し、 **[従業員リスト インスタンス]** 子ノードを展開します。

15. *Elements.xml* ファイルで、このファイルの既定の XML を次の XML に置き換えます。 この XML では、リストの名前が **[従業員]** に変更され、Jim という名前の従業員に関する情報が追加されます。

    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <Elements xmlns="http://schemas.microsoft.com/sharepoint/">
      <ListInstance Title="Employees"
                    OnQuickLaunch="TRUE"
                    TemplateType="10000"
                    Url="Lists/Employees"
                    Description="Simple list to test upgrade deployment step">
        <Data>
          <Rows>
            <Row>
              <Field Name="Title">Hance</Field>
              <Field Name="FirstName">Jim</Field>
              <Field Name="Company">Contoso</Field>
              <Field Name="Business Phone">555-555-5555</Field>
              <Field Name="E-Mail">jim@contoso.com</Field>
            </Row>
          </Rows>
        </Data>
      </ListInstance>
    </Elements>
    ```

16. *Elements.xml* ファイルを保存して閉じます。

17. EmployeesListDefinition プロジェクトのショートカット メニューを開き、 **[開く]** または **[プロパティ]** を選択します。

     プロパティ デザイナーが開きます。

18. **[SharePoint]** タブで、 **[デバッグ後に自動取り消し]** チェック ボックスをオフにし、プロパティを保存します。

#### <a name="to-deploy-the-list-definition-and-list-instance"></a>リスト定義とリスト インスタンスを配置するには

1. **ソリューション エクスプローラー** で、 **[EmployeesListDefinition]** プロジェクト ノードをクリックします。

2. **[プロパティ]** ウィンドウで、"**アクティブな配置構成**" プロパティが **[既定]** に設定されていることを確認します。

3. **F5** キーを押すか、またはメニュー バーで **[デバッグ]**  >  **[デバッグ開始]** の順に選択します。

4. プロジェクトが正常にビルドされたこと、Web ブラウザーで SharePoint サイトが開いたこと、クイック起動バーの **[リスト]** 項目に新しい **[従業員]** ボックスの一覧が含まれていること、その **[従業員]** ボックスの一覧の Jim Hance のエントリが含まれていることを確認します。

5. Web ブラウザーを閉じます。

#### <a name="to-modify-the-list-definition-and-list-instance-and-redeploy-them"></a>リスト定義とリスト インスタンスを変更して再配置するには

1. EmployeesListDefinition プロジェクトで、 **[従業員リスト インスタンス]** プロジェクト項目の子である *Elements.xml* ファイルを開きます。

2. `Data` 要素とその子を削除して、リストから Jim Hance のエントリを削除します。

     終了したら、次の XML をファイルに含める必要があります。

    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <Elements xmlns="http://schemas.microsoft.com/sharepoint/">
      <ListInstance Title="Employees"
                    OnQuickLaunch="TRUE"
                    TemplateType="10000"
                    Url="Lists/Employees"
                    Description="Simple list to test upgrade deployment step">
      </ListInstance>
    </Elements>
    ```

3. *Elements.xml* ファイルを保存して閉じます。

4. **従業員リスト** プロジェクトのショートカット メニューを開き、 **[開く]** または **[プロパティ]** を選択します。

5. リスト デザイナーで、 **[ビュー]** タブを選択します。

6. **[選択した列]** ボックスの一覧で、 **[添付]** を選択し、< キーを押してその列を **[使用可能な列]** ボックスの一覧に移します。

7. 前の手順を繰り返して、 **[選択した列]** ボックスの一覧から **[使用可能な列]** ボックスの一覧に **[勤務先電話番号]** 列を移します。

     この操作により、SharePoint サイトの **[従業員]** ボックスの一覧の既定のビューから、これらのフィールドが削除されます。

8. **F5** キーを押すかメニュー バーで **[デバッグ]**  >  **[デバッグ開始]** の順に選択して、デバッグを開始します。

9. **[配置競合]** ダイアログ ボックスが表示されていることを確認します。

     Visual Studio で、ソリューションが既に配置されている SharePoint サイトにソリューション (リスト インスタンス) を配置しようとすると、このダイアログ ボックスが表示されます。 このダイアログ ボックスは、このチュートリアルの後半でアップグレード配置手順を実行するときには表示されません。

10. **[配置競合]** ダイアログ ボックスで、 **[自動的に解決]** オプション ボタンをクリックします。

     Visual Studio によって SharePoint サイトのリスト インスタンスが削除され、プロジェクトにリスト項目が配置され、SharePoint サイトが開きます。

11. クイック起動バーの **[リスト]** セクションで、 **[従業員]** ボックスの一覧を選択し、次の詳細を確認します。

    - **[添付]** と **[自宅の電話番号]** の列は、リストのこのビューには表示されません。

    - リストが空です。 **[既定]** の配置構成を使用してソリューションを再配置したときに、 **[従業員]** ボックスの一覧がプロジェクトの新しい空のリストに置き換えられました。

## <a name="test-the-deployment-step"></a>配置手順をテストする
 これで、アップグレード配置手順をテストする準備ができました。 まず、SharePoint のリスト インスタンスに項目を追加します。 次に、リスト定義とリスト インスタンスを変更し、SharePoint サイトでそれらをアップグレードして、アップグレード配置手順で新しい項目が上書きされないことを確認します。

#### <a name="to-manually-add-an-item-to-the-list"></a>項目をリストに手動で追加するには

1. SharePoint サイトのリボンの **[リスト ツール]** タブで、 **[項目]** タブを選択します。

2. **[新規]** グループで、 **[新しい項目]** を選択します。

     または、項目リスト自体で **[新しい項目の追加]** リンクを選択することもできます。

3. **[Employees - New Item]\(従業員 - 新しい項目\)** ウィンドウの **[役職]** ボックスに「**ファシリティ マネージャー**」と入力します。

4. **[名]** ボックスに「**Andy**」と入力します。

5. **[会社]** ボックスに「**Contoso**」と入力します。

6. **[保存]** をクリックし、リストに新しい項目が表示されていることを確認して、Web ブラウザーを閉じます。

     このチュートリアルの後半では、この項目を使用して、アップグレード配置手順でこのリストの内容が上書きされないことを確認します。

#### <a name="to-test-the-upgrade-deployment-step"></a>アップグレード配置手順をテストするには

1. Visual Studio の実験用インスタンスの **ソリューション エクスプローラー** で、 **[EmployeesListDefinition]** プロジェクト ノードのショートカット メニューを開き、 **[プロパティ]** を選択します。

    プロパティ エディターまたはデザイナーが開きます。

2. **[SharePoint]** タブで、"**アクティブな配置構成**" プロパティを **[アップグレード]** に設定します。

    このカスタム配置構成には、新しいアップグレード配置手順が含まれています。

3. **[従業員リスト]** プロジェクト項目のショートカット メニューを開き、 **[プロパティ]** または **[開く]** を選択します。

    プロパティ エディターまたはデザイナーが開きます。

4. **[表示]** タブの **[電子メール]** 列を選択し、 **<** キーを選択して、その列を **[選択した列]** ボックスの一覧から **[使用可能な列]** ボックスの一覧に移します。

    この操作により、SharePoint サイトの **[従業員]** ボックスの一覧の既定のビューから、これらのフィールドが削除されます。

5. **F5** キーを押すかメニュー バーで **[デバッグ]**  >  **[デバッグ開始]** の順に選択して、デバッグを開始します。

6. Visual Studio のもう一方のインスタンスで、先ほど `CanExecute` メソッドに設定したブレークポイントで、コードが停止していることを確認します。

7. **F5** キーをもう一度押すか、メニュー バーで **[デバッグ]**  >  **[続行]** の順に選択します。

8. 先ほど `Execute` メソッドに設定したブレークポイントで、コードが停止していることを確認します。

9. **F5** キーを押すか、メニュー バーで **[デバッグ]**  >  **[続行]** の順に選択します (これが最後です)。

     SharePoint サイトが Web ブラウザーで開きます。

10. クイック起動領域の **[リスト]** セクションで、 **[従業員]** ボックスの一覧を選択し、次の詳細を確認します。

    - 前に手動で追加した項目 (ファシリティ マネージャーの Andy の場合) が、まだリストに表示されます。

    - **[勤務先電話番号]** 列と **[電子メール アドレス]** 列は、リストのこのビューに表示されません。

      **[アップグレード]** 配置構成により、SharePoint の既存の **[従業員]** リスト インスタンスが変更されます。 **[アップグレード]** 構成ではなく **[既定]** 配置構成を使用した場合は、配置の競合が発生します。 Visual Studio では、 **[従業員]** ボックスの一覧を置き換えて競合を解決し、ファシリティ マネージャーの Andy の項目は削除されます。

## <a name="clean-up-the-development-computer"></a>開発コンピューターをクリーンアップする
 アップグレード配置手順のテストが完了したら、SharePoint サイトからリスト インスタンスとリスト定義を削除し、Visual Studio から配置手順の拡張機能を削除します。

#### <a name="to-remove-the-list-instance-from-the-sharepoint-site"></a>リスト インスタンスを SharePoint サイトから削除するには

1. まだ開いていない場合は、SharePoint サイトで **[従業員]** ボックスの一覧を開きます。

2. SharePoint サイトのリボンで、 **[リスト ツール]** タブを選択し、 **[リスト]** タブを選択します。

3. **[設定]** グループで、 **[リストの設定]** 項目をクリックします。

4. **[権限と管理]** の下で、 **[このリストを削除します]** コマンドを選択し、 **[OK]** をクリックして、リストをごみ箱に送り、Web ブラウザーを閉じます。

#### <a name="to-remove-the-list-definition-from-the-sharepoint-site"></a>リスト定義を SharePoint サイトから削除するには

1. Visual Studio の実験用インスタンスのメニュー バーで **[ビルド]**  >  **[取り消し]** の順に選択します。

     Visual Studio によって、リスト定義を SharePoint サイトから取り消します。

#### <a name="to-uninstall-the-extension"></a>拡張機能をアンインストールするには

1. Visual Studio の実験用インスタンスのメニュー バーで、 **[ツール]**  >  **[拡張機能と更新プログラム]** の順に選択します。

     **[拡張機能と更新プログラム]** ダイアログ ボックスが表示されます。

2. 拡張機能の一覧で、 **[SharePoint プロジェクトのアップグレード配置手順]** を選択し、 **[アンインストール]** コマンドをクリックします。

3. 表示されるダイアログ ボックスで、 **[はい]** を選択して拡張機能のアンインストールを確定し、 **[今すぐ再起動]** を選択してアンインストールを完了します。

4. Visual Studio の両方のインスタンス (実験用インスタンスと、UpgradeDeploymentStep ソリューションが開かれたインスタンス) を閉じます。

## <a name="see-also"></a>関連項目
- [SharePoint のパッケージ化と配置を拡張する](../sharepoint/extending-sharepoint-packaging-and-deployment.md)