---
title: 'チュートリアル: SharePoint プロジェクト項目の種類の拡張 | Microsoft Docs'
description: このチュートリアルでは、ビジネス データ接続 (BDC) モデル プロジェクト項目など、SharePoint プロジェクト項目の種類の拡張機能を作成します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- project items [SharePoint development in Visual Studio], extending
- SharePoint project items, extending
- SharePoint development in Visual Studio, extending project items
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: a91cbd863ed613804418cd5d1666412a01f8f542
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/02/2021
ms.locfileid: "106217698"
---
# <a name="walkthrough-extend-a-sharepoint-project-item-type"></a>チュートリアル: SharePoint プロジェクト項目の種類を拡張する
  SharePoint にビジネス データ接続 (BDC) サービスのモデルを作成するには、**ビジネス データ接続モデル** プロジェクト項目を使用します。 既定では、このプロジェクト項目を使用してモデルを作成しただけでは、モデル内のデータがユーザーに表示されません。 ユーザーがデータを閲覧できるようにするには、それに加えて、SharePoint に外部リストを作成する必要があります。

 このチュートリアルでは、**ビジネス データ接続モデル** プロジェクト項目の拡張機能を作成します。 開発者は、この拡張機能を使用することで、BDC モデルのデータを表示するための外部リストを同じプロジェクト内で作成できます。 このチュートリアルでは、次のタスクについて説明します。

- 次の 2 つの主要タスクを実行する Visual Studio の拡張機能を作成する。

  - BDC モデル内のデータを表示するための外部リストを生成する。 この拡張機能は、リストを定義する *Elements.xml* ファイルを、SharePoint プロジェクト システムのオブジェクト モデルを使用して生成します。 さらに、BDC モデルと一緒に配置できるように、このファイルをプロジェクトに追加します。

  - **ソリューション エクスプローラー** 内の **ビジネス データ接続モデル** プロジェクト項目に対するショートカット メニュー項目を追加する。 開発者は、このメニュー項目をクリックして、BDC モデル用の外部リストを生成できます。

- 拡張機能のアセンブリを配置するための Visual Studio Extension (VSIX) パッケージを構築する。

- 拡張機能をテストする。

## <a name="prerequisites"></a>必須コンポーネント
 このチュートリアルを実行するには、開発コンピューターに次のコンポーネントが必要です。

- サポート対象エディションの Microsoft Windows、SharePoint、および Visual Studio。

- [!include[vssdk_current_long](../sharepoint/includes/vssdk-current-long-md.md)]。 このチュートリアルでは、プロジェクト項目を配置するための VSIX パッケージを、SDK の **VSIX プロジェクト** テンプレートを使用して作成します。 詳細については、「[Visual Studio での SharePoint ツールの拡張](../sharepoint/extending-the-sharepoint-tools-in-visual-studio.md)」を参照してください。

  次の概念に関する知識があると役に立ちますが、チュートリアルを実行するうえで必須というわけではありません。

- [!INCLUDE[moss_14_long](../sharepoint/includes/moss-14-long-md.md)] の BDC サービス。 詳細については、「[BDC アーキテクチャ](/previous-versions/office/developer/sharepoint-2010/ee558876(v=office.14))」を参照してください。

- BDC モデルの XML スキーマ。 詳細については、「[BDC モデル インフラストラクチャ](/previous-versions/office/developer/sharepoint-2010/ee556378(v=office.14))」を参照してください。

## <a name="create-the-projects"></a>プロジェクトを作成する
 このチュートリアルを完了するには、2 つのプロジェクトを作成する必要があります。

- プロジェクト項目の拡張機能を配置するために VSIX パッケージを作成する VSIX プロジェクト。

- プロジェクト項目の拡張機能を実装するクラス ライブラリ プロジェクト。

  この 2 つのプロジェクトを作成することから始めます。

#### <a name="to-create-the-vsix-project"></a>VSIX プロジェクトを作成するには

1. [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]を起動します。

2. メニュー バーで、 **[ファイル]**  >  **[新規作成]**  >  **[プロジェクト]** を選択します。

3. **[新しいプロジェクト]** ダイアログ ボックスで、 **[Visual C#]** ノードまたは **[Visual Basic]** ノードを展開し、 **[機能拡張]** ノードをクリックします。

    > [!NOTE]
    > **[機能拡張]** ノードは、Visual Studio SDK がインストールされている場合にのみ使用できます。 詳細については、このトピックで前に説明した「前提条件」を参照してください。

4. **[新しいプロジェクト]** ダイアログ ボックスの上部にある一覧で **[.NET Framework 4.5]** を選択します。

     SharePoint ツールの拡張機能を使用するには、このバージョンの .NET Framework の機能が必要です。

5. **[VSIX プロジェクト]** テンプレートを選択します。

6. **[名前]** ボックスに「**GenerateExternalDataLists**」と入力し、 **[OK]** をクリックします。

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] によって、**GenerateExternalDataLists** プロジェクトが **ソリューション エクスプローラー** に追加されます。

7. source.extension.vsixmanifest ファイルが自動的に開かない場合は、GenerateExternalDataLists プロジェクトのショートカット メニューを開き、 **[開く]** をクリックします

8. source.extension.vsixmanifest ファイルで [作成者] フィールドが空白でないことを確認し (「Contoso」と入力し)、ファイルを保存して閉じます。

#### <a name="to-create-the-extension-project"></a>拡張機能プロジェクトを作成するには

1. **ソリューション エクスプローラー** で **[GenerateExternalDataLists]** ソリューション ノードのショートカット メニューを開き、 **[追加]** 、 **[新しいプロジェクト]** の順に選択します。

2. **[新しいプロジェクトの追加]** ダイアログ ボックスで、 **[Visual C#]** ノードまたは **[Visual Basic]** ノードを展開し、 **[Windows]** ノードをクリックします。

3. ダイアログ ボックスの上部にある一覧で **[.NET Framework 4.5]** を選択します。

4. プロジェクト テンプレートの一覧で **[クラス ライブラリ]** を選択します。

5. **[名前]** ボックスに「**BdcProjectItemExtension**」と入力し、 **[OK]** をクリックします。

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] によって、**BdcProjectItemExtension** プロジェクトがソリューションに追加され、既定の Class1 コード ファイルが開きます。

6. Class1 コード ファイルをプロジェクトから削除します。

## <a name="configure-the-extension-project"></a>拡張機能プロジェクトを構成する
 プロジェクト項目の拡張機能を作成するためのコードを記述する前に、コード ファイルおよびアセンブリ参照を拡張プロジェクトに追加します。

#### <a name="to-configure-the-project"></a>プロジェクトを構成するには

1. BdcProjectItemExtension プロジェクトに、次の名前を持つ 2 つのコード ファイルを追加します。

    - ProjectItemExtension

    - GenerateExternalDataLists

2. BdcProjectItemExtension プロジェクトを選択し、メニュー バーで **[プロジェクト]**  >  **[参照の追加]** の順に選択します。

3. **[アセンブリ]** ノードの下の **[フレームワーク]** ノードをクリックし、次のアセンブリの各チェック ボックスをオンにします。

    - System.ComponentModel.Composition

    - WindowsBase

4. **[アセンブリ]** ノードの下の **[拡張機能]** ノードをクリックし、次のアセンブリのチェック ボックスをオンにします。

    - Microsoft.VisualStudio.SharePoint

5. **[OK]** を選択します。

## <a name="define-the-project-item-extension"></a>プロジェクト項目の拡張機能を定義する
 **[ビジネス データ接続モデル]** プロジェクト項目の拡張機能を定義するクラスを作成します。 拡張機能を定義するため、このクラスに <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeExtension> インターフェイスを実装します。 このインターフェイスは、既存の種類のプロジェクト項目を拡張する場合に必ず実装します。

#### <a name="to-define-the-project-item-extension"></a>プロジェクト項目の拡張機能を定義するには

1. 次のコードを ProjectItemExtension コード ファイルに貼り付けます。

    > [!NOTE]
    > このコードを追加した直後は、いくつかのコンパイル エラーが発生します。 これらのエラーは、この後の手順でコードを追加すると解消されます。

     :::code language="csharp" source="../sharepoint/codesnippet/CSharp/generateexternaldatalists/bdcprojectitemextension/projectitemextension.cs" id="Snippet1":::
     :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/generateexternaldatalists/bdcprojectitemextension/projectitemextension.vb" id="Snippet1":::

## <a name="create-the-external-data-lists"></a>外部データ リストを作成する
 BDC モデル内の各エンティティの外部データ リストを作成する `GenerateExternalDataListsExtension` クラスの部分定義を追加します。 外部データ リストを作成するために、このコードはまず BDC モデル ファイル内の XML データを解析して、BDC モデルのエンティティ データを読み取ります。 次に、BDC モデルに基づくリスト インスタンスを作成し、このリスト インスタンスをプロジェクトに追加します。

#### <a name="to-create-the-external-data-lists"></a>外部データ リストを作成するには

1. 次のコードを GenerateExternalDataLists コード ファイルに貼り付けます。

     :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/generateexternaldatalists/bdcprojectitemextension/generateexternaldatalists.vb" id="Snippet2":::
     :::code language="csharp" source="../sharepoint/codesnippet/CSharp/generateexternaldatalists/bdcprojectitemextension/generateexternaldatalists.cs" id="Snippet2":::

## <a name="checkpoint"></a>Checkpoint
 この段階で、プロジェクト項目の拡張機能に必要なすべてのコードがプロジェクトに揃ったことになります。 エラーが発生することなくプロジェクトをコンパイルできるかどうか、ソリューションをビルドして確認してください。

#### <a name="to-build-the-solution"></a>ソリューションをビルドするには

1. メニュー バーで、 **[ビルド]**  >  **[ソリューションのビルド]** の順にクリックします。

## <a name="create-a-vsix-package-to-deploy-the-project-item-extension"></a>プロジェクト項目の拡張機能を配置するために VSIX パッケージを作成する
 拡張機能を配置するには、ソリューションで VSIX プロジェクトを使用して VSIX パッケージを作成します。 まず、VSIX プロジェクトに含まれている source.extension.vsixmanifest ファイルを変更して、VSIX パッケージを構成します。 次に、ソリューションをビルドして VSIX パッケージを作成します。

#### <a name="to-configure-and-create-the-vsix-package"></a>VSIX パッケージを構成および作成するには

1. **ソリューション エクスプローラー** で、GenerateExternalDataLists プロジェクトの source.extension.vsixmanifest ファイルのショートカット メニューを開き、 **[開く]** をクリックします。

     Visual Studio によってマニフェスト エディターでファイルが開きます。 source.extension.vsixmanifest ファイルが、すべての VSIX パッケージで必要とされる extension.vsixmanifest ファイルの基礎となります。 このファイルの詳細については、「[VSIX 拡張機能スキーマ 1.0 リファレンス](/previous-versions/dd393700(v=vs.110))」を参照してください。

2. **[製品名]** ボックスに「**External Data List Generator**」と入力します。

3. **[作成者]** ボックスに、「**Contoso**」と入力します。

4. **[説明]** ボックスに「**An extension for Business Data Catalog Model project items that can be used to generate external data lists」(外部データ リストを生成する用途に使用できるビジネス データ接続モデル プロジェクト項目用の拡張機能)** と入力します。

5. エディターの **[アセット]** タブで、 **[新規作成]** をクリックします。

     **[新しい資産の追加]** ダイアログ ボックスが表示されます。

6. **[種類]** ボックスの一覧で、 **[Microsoft.VisualStudio.MefComponent]** を選択します。

    > [!NOTE]
    > この値は、extension.vsixmanifest ファイル内の `MefComponent` 要素に対応します。 この要素は、VSIX パッケージ内の拡張機能アセンブリの名前を指定します。 詳細については、「[MEFComponent 要素 (VSX スキーマ)](/previous-versions/visualstudio/visual-studio-2010/dd393736\(v\=vs.100\))」を参照してください。

7. **[ソース]** ボックスの一覧で、 **[現在のソリューション内のプロジェクト]** を選択します。

8. **[プロジェクト]** ボックスの一覧で **[BdcProjectItemExtension]** を選択し、 **[OK]** をクリックします。

9. メニュー バーで、 **[ビルド]**  >  **[ソリューションのビルド]** の順にクリックします。

10. エラーが発生することなくプロジェクトがコンパイルされてビルドされたことを確認します。

11. GenerateExternalDataLists プロジェクトのビルド出力フォルダーに GenerateExternalDataLists.vsix ファイルが格納されていることを確認します。

     既定では、ビルド出力フォルダーは ..\bin\Debug で、プロジェクト ファイルが格納されているフォルダーの下にあります。

## <a name="test-the-project-item-extension"></a>プロジェクト項目の拡張機能をテストする
 これで、プロジェクト項目の拡張機能をテストする準備ができました。 まず、Visual Studio の実験用インスタンスで拡張機能プロジェクトのデバッグを開始します。 次に、Visual Studio の実験用インスタンスで拡張機能を使用して、BDC モデルの外部リストを生成します。 最後に、SharePoint サイトで外部リストを開いて正常に動作するかどうかを確認します。

#### <a name="to-start-debugging-the-extension"></a>拡張機能のデバッグを開始するには

1. 必要に応じて、管理者の資格情報を使用して Visual Studio を再起動し、GenerateExternalDataLists ソリューションを開きます。

2. BdcProjectItemExtension プロジェクトで、ProjectItemExtension コード ファイルを開き、`Initialize` メソッド内のコード行にブレークポイントを追加します。

3. GenerateExternalDataLists コード ファイルを開き、`GenerateExternalDataLists_Execute` メソッドのコードの先頭行にブレークポイントを追加します。

4. **F5** キーを押すかメニュー バーで **[デバッグ]**  >  **[デバッグ開始]** の順に選択して、デバッグを開始します。

     Visual Studio によって、拡張機能が %UserProfile%\AppData\Local\Microsoft\VisualStudio\10.0Exp\Extensions\Contoso\External Data List Generator\1.0 にインストールされ、Visual Studio の実験用インスタンスが開始されます。 このインスタンスの Visual Studio でプロジェクト項目をテストします。

#### <a name="to-test-the-extension"></a>拡張機能をテストするには

1. Visual Studio の実験用インスタンスのメニュー バーで **[ファイル]**  >  **[新規作成]**  >  **[プロジェクト]** の順に選択します。

2. **[新しいプロジェクト]** ダイアログ ボックスで、 **[テンプレート]** ノード、 **[Visual C#]** ノード、 **[SharePoint]** ノードの順に展開し、 **[2010]** をクリックします。

3. ダイアログ ボックスの上部にある一覧で **[.NET Framework 3.5]** が選択されていることを確認します。 [!INCLUDE[moss_14_long](../sharepoint/includes/moss-14-long-md.md)] のプロジェクトには、このバージョンの .NET Framework が必要です。

4. プロジェクト テンプレートの一覧で **[SharePoint 2010 プロジェクト]** を選択します。

5. **[名前]** ボックスに「**SharePointProjectTestBDC**」と入力し、 **[OK]** をクリックします。

6. SharePoint カスタマイズ ウィザードで、デバッグに使用するサイトの URL を入力し、 **[ファーム ソリューションとして配置する]** を選択して、 **[完了]** をクリックします。

7. SharePointProjectTestBDC プロジェクトのショートカット メニューを開き、 **[追加]** を選択して、 **[新しい項目]** をクリックします。

8. **[新しい項目の追加 - SharePointProjectTestBDC]** ダイアログ ボックスで、インストールされている言語ノード、 **[SharePoint]** ノードの順に展開します。

9. **[2010]** ノード、 **[ビジネス データ接続モデル (ファーム ソリューションのみ)]** テンプレートの順に選択します。

10. **[名前]** ボックスに「**TestBDCModel**」と入力し、 **[追加]** をクリックします。

11. Visual Studio のもう一方のインスタンスで、ProjectItemExtension コード ファイルの `Initialize` メソッドに設定したブレークポイントで、コードが停止していることを確認します。

12. 停止した Visual Studio のインスタンスで、**F5** キーを押すかメニュー バーで **[デバッグ]**  >  **[続行]** の順に選択して、プロジェクトのデバッグを続行します。

13. Visual Studio の実験用インスタンスで、**F5** キーを押すかメニュー バーで **[デバッグ]**  >  **[デバッグ開始]** の順に選択して、**TestBDCModel** プロジェクトをビルド、配置、実行します。

     デバッグ用に指定した SharePoint サイトの既定のページが Web ブラウザーに表示されます。

14. クイック起動領域の **[リスト]** セクションを見て、プロジェクトの既定の BDC モデルに基づくリストがまだ存在しないことを確認します。 まず、SharePoint のユーザー インターフェイスを使用するか、プロジェクト項目の拡張機能を使用して、外部データ リストを作成する必要があります。

15. Web ブラウザーを閉じます。

16. TestBDCModel プロジェクトを開いている Visual Studio のインスタンスで、**ソリューション エクスプローラー** の **[TestBDCModel]** ノードのショートカット メニューを開き、 **[外部データ リストの生成]** をクリックします。

17. Visual Studio のもう一方のインスタンスで、`GenerateExternalDataLists_Execute` メソッドに設定したブレークポイントで、コードが停止していることを確認します。 **F5** キーを押すかメニュー バーで **[デバッグ]**  >  **[続行]** の順に選択して、プロジェクトのデバッグを続行します。

18. Visual Studio の実験用インスタンスによって、TestBDCModel プロジェクトに **Entity1DataList** という名前のリスト インスタンスが追加されます。また、そのリスト インスタンスに対して **Feature2** という名前のフィーチャーが生成されます。

19. **F5** キーを押すかメニュー バーで **[デバッグ]**  >  **[デバッグ開始]** の順に選択して、TestBDCModel プロジェクトをビルド、配置、実行します。

     デバッグに使用する SharePoint サイトの既定のページが Web ブラウザーに表示されます。

20. クイック起動領域の **[リスト]** セクションで、 **[Entity1DataList]** リストを選択します。

21. リストに Identifier1 および Message という名前の列が存在し、項目 (Identifier1 の値は 0 で、Message の値は Hello World) が 1 つ含まれていることを確認します。

     **[ビジネス データ接続モデル]** プロジェクト テンプレートにより、このデータをすべて提供する既定の BDC モデルが生成されます。

22. Web ブラウザーを閉じます。

## <a name="clean-up-the-development-computer"></a>開発コンピューターをクリーンアップする
 プロジェクト項目の拡張機能のテストが終わったら、外部リストおよび BDC モデルを SharePoint サイトから削除し、さらにプロジェクト項目の拡張機能を Visual Studio から削除します。

#### <a name="to-remove-the-external-data-list-from-the-sharepoint-site"></a>SharePoint サイトから外部データ リストを削除するには

1. SharePoint サイトのクイック起動領域で、 **[Entity1DataList]** リストをクリックします。

2. SharePoint サイトのリボンで、 **[リスト]** タブをクリックします。

3. **[リスト]** タブで、 **[設定]** グループの **[リストの設定]** をクリックします。

4. **[権限と管理]** の下で、 **[このリストの削除]** を選択し、 **[OK]** をクリックして、リストをごみ箱に送ります。

5. Web ブラウザーを閉じます。

#### <a name="to-remove-the-bdc-model-from-the-sharepoint-site"></a>BDC モデルを SharePoint サイトから削除するには

1. Visual Studio の実験用インスタンスのメニュー バーで **[ビルド]**  >  **[取り消し]** の順に選択します。

     Visual Studio によって BDC モデルが SharePoint サイトから削除されます。

#### <a name="to-remove-the-project-item-extension-from-visual-studio"></a>プロジェクト項目の拡張機能を Visual Studio から削除するには

1. Visual Studio の実験用インスタンスのメニュー バーで、 **[ツール]**  >  **[拡張機能と更新プログラム]** の順に選択します。

     **[拡張機能と更新プログラム]** ダイアログ ボックスが表示されます。

2. 拡張機能の一覧で **[External Data List Generator]** を選択し、 **[アンインストール]** をクリックします。

3. 確認のダイアログ ボックスが表示されたら、 **[はい]** を選択して、拡張機能をアンインストールします。

4. **[今すぐ再起動]** をクリックするとアンインストールは完了です。

5. Visual Studio の両方のインスタンス (実験用インスタンスと、GenerateExternalDataLists ソリューションを開いたインスタンス) を閉じます。

## <a name="see-also"></a>関連項目
- [SharePoint プロジェクト システムを拡張する](../sharepoint/extending-the-sharepoint-project-system.md)
- [ビジネス データ接続モデルを作成する](../sharepoint/creating-a-business-data-connectivity-model.md)
- [ビジネス データ接続モデルを設計する](../sharepoint/designing-a-business-data-connectivity-model.md)