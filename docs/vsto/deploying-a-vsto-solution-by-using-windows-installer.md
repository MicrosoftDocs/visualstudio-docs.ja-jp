---
title: Windows インストーラーを使用した VSTO ソリューションの配置
description: Visual Studio インストーラー プロジェクトを使用して、Microsoft Visual Studio Tools for Office (VSTO) のアドインまたはドキュメント レベルのソリューションを配置する方法について説明します。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 08/18/2010
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Office development in Visual Studio, setup project
- Office development in Visual Studio, MSI
- deploying applications [Office development in Visual Studio], setup project
- deploying applications [Office development in Visual Studio], MSI
- ClickOnce deployment [Office development in Visual Studio], MSI
- publishing Office solutions [Office development in Visual Studio], setup project
- Office applications [Office development in Visual Studio], MSI
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 75c2d97e8cd30bb3cf5605d50e65a68513590647
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99939371"
---
# <a name="deploying-a-vsto-solution-using-windows-installer"></a>Windows インストーラーを使用した VSTO ソリューションの配置

## <a name="summary"></a>まとめ

Visual Studio インストーラー プロジェクトを使用して、Microsoft Visual Studio Tools for Office (VSTO) のアドインまたはドキュメント レベルのソリューションを配置する方法について説明します。

Wouter van Vugt、Code Counsel

Ted Pattison、Ted Pattison Group

この記事は、元の作成者の許可を得た上で Microsoft によって更新されたものです。

**適用対象:** Visual Studio Tools for Office、Microsoft Office、Microsoft Visual Studio。

## <a name="overview"></a>概要

VSTO ソリューションを開発し、Windows インストーラー パッケージを使用してそのソリューションを配置することができます。 ここでは、簡単な Office アドインを配置する手順について説明します。

## <a name="deployment-methods"></a>配置方法

ClickOnce を使用すると、アドインやソリューションのセットアップを簡単に作成できます。 ただし、管理特権を必要とするアドイン (マシン レベルのアドインなど) をこれでインストールすることはできません。

管理特権を必要とするアドインは Windows インストーラーを使用してインストールできますが、セットアップの作成にはより多くの作業が必要になります。

ClickOnce を使用して VSTO ソリューションを配置する方法の概要については、「[ClickOnce を使用して Office ソリューションを配置する](deploying-an-office-solution-by-using-clickonce.md)」を参照してください。

## <a name="deploying-office-solutions-that-target-the-vsto-runtime"></a>VSTO ランタイムを対象とする Office ソリューションの配置

ClickOnce と Windows インストーラーのパッケージでは、Office ソリューションのインストール時に同じ基本的なタスクを実行する必要があります。

1. ユーザーのコンピューターに前提条件コンポーネントをインストールします。
2. ソリューション用の特定のコンポーネントを配置します。
3. アドイン用に、レジストリ エントリを作成します。
4. ソリューションを信頼して実行できるようにします。

### <a name="required-prerequisite-components-on-the-target-computer"></a>ターゲット コンピューターに必要な前提条件コンポーネント

VSTO ソリューションを実行するためにコンピューターにインストールする必要があるソフトウェアの一覧を次に示します。

- Microsoft Office 2010 以降。
- Microsoft .NET Framework 4 以降。
- Microsoft Visual Studio 2010 Tools for Office Runtime
  このランタイムには、アドインとドキュメント レベルのソリューションを管理する環境が備わっています。 Microsoft Office にはあるバージョンのランタイムが付属していますが、アドインを使用して特定のバージョンを再配布することもできます。
- Microsoft Office 用のプライマリ相互運用機能アセンブリ (埋め込まれた相互運用機能型を使用していない場合)。
- プロジェクトによって参照される任意のアセンブリ。

### <a name="specific-components-for-the-solution"></a>ソリューション用の特定のコンポーネント

インストーラー パッケージでは、以下のコンポーネントをユーザーのコンピューターにインストールする必要があります。

- Microsoft Office ドキュメント (ドキュメント レベルのソリューションを作成する場合)。
- カスタマイズ アセンブリとそれに必要なすべてのアセンブリ。
- 構成ファイルなどの追加のコンポーネント。
- アプリケーション マニフェスト (.manifest)。
- 配置マニフェスト (.vsto)。

### <a name="registry-entries-for-add-ins"></a>アドイン用のレジストリ エントリ

Microsoft Office では、レジストリ エントリを使用してアドインの検索と読み込みを行います。これらのレジストリ エントリは、配置プロセスの一環として作成する必要があります。 これらのレジストリ エントリの詳細については、「[VSTO アドインのレジストリ エントリ](registry-entries-for-vsto-add-ins.md)」を参照してください。

カスタム フォーム領域を表示する Outlook アドインには、それらのフォーム領域を識別できるようにする追加のレジストリ エントリが必要です。 詳細については、「[Outlook フォーム領域のレジストリ エントリ](registry-entries-for-vsto-add-ins.md#OutlookEntries)」を参照してください。

ドキュメント レベルのソリューションには、レジストリ エントリは必要ありません。 代わりに、ドキュメント内のプロパティを使用してカスタマイズを検索します。 これらのプロパティの詳細については、「[カスタム ドキュメント プロパティの概要](custom-document-properties-overview.md)」を参照してください。

### <a name="trusting-the-vsto-solution"></a>VSTO ソリューションへの信頼

カスタマイズが実行されるようにするには、ソリューションがマシンによって信頼される必要があります。 アドインを信頼させるには、証明書を使用してマニフェストに署名するか、信頼のリストを使用して信頼関係を築くか、マシン上の信頼できる場所にアドインをインストールします。

署名用の証明書を取得する方法の詳細については、[ClickOnce での配置と Authenticode](../deployment/clickonce-and-authenticode.md) に関するページを参照してください。 ソリューションへの信頼の詳細については、[信頼のリストを使用した Office ソリューションへの信頼](trusting-office-solutions-by-using-inclusion-lists.md)に関するページを参照してください。 Windows インストーラー ファイルにカスタム アクションと共に、信頼のリストのエントリを追加できます。 信頼のリストを有効にする方法の詳細については、「[方法: 信頼のリストのセキュリティを構成する](how-to-configure-inclusion-list-security.md)」を参照してください。

どちらのオプションも使用しない場合は、信頼プロンプトがユーザーに表示され、ソリューションを信頼するかどうかを決めることができます。

ドキュメント レベルのソリューションに関連するセキュリティの詳細については、[ドキュメントへの信頼の付与](granting-trust-to-documents.md)に関するページを参照してください。

## <a name="creating-a-basic-installer"></a>基本インストーラーの作成

セットアップと配置プロジェクトのテンプレートは、ダウンロード可能な [Microsoft Visual Studio Installer Projects](https://marketplace.visualstudio.com/items?itemName=visualstudioclient.MicrosoftVisualStudio2017InstallerProjects) 拡張機能に含まれています。

Office ソリューション用のインストーラーを作成するには、次のタスクを実行する必要があります。

- 配置される Office ソリューションのコンポーネントを追加します。
- アプリケーション レベルのアドイン用に、レジストリ キーを構成します。
- エンド ユーザーのコンピューターにインストールできるように、前提条件コンポーネントを構成します。
- 必須の前提条件コンポーネントが使用可能であることを検証するための起動条件を構成します。 起動条件を使用すると、必須の前提条件がすべてインストールされていない場合にインストールをブロックできます。

最初の手順では、セットアップ プロジェクトを作成します。

### <a name="to-create-the-addin-setup-project"></a>AddIn セットアップ プロジェクトを作成するには

1. 配置する Office アドイン プロジェクトを開きます。 この例では、ExcelAddIn と呼ばれる Excel アドインを使用しています。
2. Office プロジェクトを開いた状態で、 **[ファイル]** メニューの **[追加]** を展開し、 **[新しいプロジェクト]** をクリックして新しいプロジェクトを追加します。
::: moniker range="=vs-2017"
3. **[新しいプロジェクトの追加]** ダイアログで、 **[プロジェクトの種類]** ペインの **[その他のプロジェクトの種類]** を展開した後、 **[セットアップと配置]** を展開して、 **[Visual Studio インストーラー]** を選択します。
4. **[テンプレート]** ペインで、 **[Visual Studio のインストール済み]** テンプレート グループから **[セットアップ プロジェクト]** を選択します。
::: moniker-end
::: moniker range="=vs-2019"
3. **[新しいプロジェクトの追加]** ダイアログで、 **[セットアップ プロジェクト]** テンプレートを選択します。
4. **[次へ]** をクリックします。
::: moniker-end

5. **[名前]** ボックスに「**OfficeAddInSetup**」と入力します。
::: moniker range="=vs-2017"
6. **[開く]** をクリックして、新しいセットアップ プロジェクトを作成します。
::: moniker-end
::: moniker range="=vs-2019"
6. **[作成]** をクリックして、新しいセットアップ プロジェクトを作成します。
::: moniker-end

Visual Studio によって、新しいセットアップ プロジェクト用のファイル システム エクスプローラーが開きます。 ファイル システム エクスプローラーでは、セットアップ プロジェクトにファイルを追加できます。

   ![セットアップ プロジェクト用のファイル システム エクスプローラーのスクリーンショット](media/setup-project-figure-1.png)

   **図 1: セットアップ プロジェクト用のファイル システム エクスプローラー**

セットアップ プロジェクトでは、ExcelAddIn を配置する必要があります。 このタスクのセットアップ プロジェクトを構成するには、ExcelAddIn プロジェクト出力をセットアップ プロジェクトに追加します。

### <a name="to-add-the-exceladdin-project-output"></a>ExcelAddIn プロジェクト出力を追加するには

1. **ソリューション エクスプローラー** で、 **[OfficeAddInSetup]** を右クリックし、 **[追加]** 、 **[プロジェクト出力]** の順にクリックします。
2. **[プロジェクト出力グループの追加]** ダイアログで、プロジェクト一覧から **ExcelAddIn** を選択して、 **[プライマリ出力]** を選択します。
3. **[OK]** をクリックして、プロジェクト出力をセットアップ プロジェクトに追加します。

    ![セットアップ プロジェクトの [プロジェクト出力グループの追加] ダイアログのスクリーンショット](media/setup-project-figure-2.png)

    **図 2: セットアップ プロジェクトの [プロジェクト出力グループの追加] ダイアログ**

セットアップ プロジェクトでは、配置マニフェストとアプリケーション マニフェストを配置する必要があります。 これらの 2 つのファイルは、ExcelAddIn プロジェクトの出力フォルダーからスタンドアロン ファイルとしてセットアップ プロジェクトに追加します。

### <a name="to-add-the-deployment-and-application-manifests"></a>配置およびアプリケーション マニフェストを追加するには

1. **ソリューション エクスプローラー** で、 **[OfficeAddInSetup]** を右クリックし、 **[追加]** 、 **[ファイル]** の順にクリックします。
2. **[ファイルの追加]** ダイアログ ボックスで、**ExcelAddIn** 出力ディレクトリに移動します。 選択したビルド構成にもよりますが、出力ディレクトリは通常、プロジェクトのルート ディレクトリ内にある **bin\\release** サブフォルダーです。
3. **ExcelAddIn.vsto** および **ExcelAddIn.dll.manifest** ファイルを選択し、 **[開く]** をクリックして、これらの 2 つのファイルをセットアップ プロジェクトに追加します。

    ![ソリューション エクスプローラーでのアプリケーションおよび配置マニフェストのスクリーンショット](media/setup-project-figure-3.jpg)

    **図 3: ソリューション エクスプローラーでのアドイン用のアプリケーションおよび配置マニフェスト**

ExcelAddIn の参照には、ExcelAddIn に必要なコンポーネントがすべて含まれています。 これらのコンポーネントを正しく登録できるようにするには、前提条件パッケージを使用してそれらを除外および配置する必要があります。 また、インストールを開始する前に、ソフトウェア ライセンス条項を表示し、それに同意する必要もあります。

### <a name="to-exclude-the-exceladdin-project-dependencies"></a>ExcelAddIn プロジェクトの依存関係を除外するには

1. **ソリューション エクスプローラー** の **[OfficeAddInSetup]** ノードで、 **[検出された依存関係]** 項目の下にあるすべての依存関係項目 (**Microsoft .NET Framework** と、 **\*.Utilities.dll** で終わるすべてアセンブリを除く) を選択します。 Utilities アセンブリは、アプリケーションと共に配置することになっています。
2. そのグループを右クリックし、 **[プロパティ]** を選択します。
3. **[プロパティ]** ウィンドウで、 **[除外]** プロパティを **[True]** に変更して、それらの依存アセンブリをセットアップ プロジェクトから除外します。 Utilities アセンブリを除外しないようにしてください。

    ![除外する依存関係を示すソリューション エクスプローラーのスクリーンショット](media/setup-project-figure-4.jpg)

    **図 4: 依存関係の除外**

前提条件コンポーネントをインストールするように Windows インストーラー パッケージを構成するには、ブートストラップとも呼ばれるセットアップ プログラムを追加します。 このセットアップ プログラムでは、前提条件コンポーネントのインストール (ブートストラップと呼ばれるプロセス) を実行できます。

**ExcelAddIn** の場合、アドインを正しく実行するには、以下の必須コンポーネントがインストールされている必要があります。

- Office ソリューションで対象となる Microsoft .NET Framework バージョン。
- Microsoft Visual Studio 2010 Tools for Office Runtime。

依存コンポーネントを必須コンポーネントとして構成するには

1. **ソリューション エクスプローラー** で、**OfficeAddInSetup** プロジェクトを右クリックして、 **[プロパティ]** を選択します。
2. **[OfficeAddInSetup プロパティ ページ]** ダイアログ ボックスが表示されます。
3. **[必須コンポーネント]** ボタンをクリックします。
4. [必須コンポーネント] ダイアログ ボックスで、適切なバージョンの .NET Framework と Microsoft Visual Studio Tools for Office Runtime を選択します。

    ![[必須コンポーネント] ダイアログ ボックスのスクリーンショット](media/setup-project-figure-5.png)

    **図 5: [必須コンポーネント] ダイアログ ボックス**

    > [!NOTE]
    >Visual Studio セットアップ プロジェクト内の構成済みの前提条件パッケージのいくつかは、選択したビルド構成に依存しています。 使用するビルド構成ごとに適切な前提条件コンポーネントを選択する必要があります。

Microsoft Office では、レジストリ キーを使用してアドインを検索します。 HKEY\_CURRENT\_USER ハイブ内のキーは、個々のユーザーごとにアドインを登録するために使用されます。 HKEY\_LOCAL\_MACHINE ハイブの下にあるキーは、マシンのすべてのユーザーにアドインを登録するために使用されます。 これらのレジストリ キーの詳細については、「[VSTO アドインのレジストリ エントリ](registry-entries-for-vsto-add-ins.md)」を参照してください。

### <a name="to-configure-the-registry"></a>レジストリを構成するには

1. **ソリューション エクスプローラー** で、 **[OfficeAddInSetup]** を右クリックします。
2. **[表示]** を展開します。
3. **[レジストリ]** をクリックして、レジストリ エディターのウィンドウを開きます。
4. **[レジストリ (OfficeAddInSetup)]** エディターで、 **[HKEY\_LOCAL\_MACHINE**]、 **[Software]** の順に展開します。
5. **HKEY\_LOCAL\_MACHINE\\Software** の下にある **\[Manufacturer\]** キーを削除します。
6. **[HKEY\_CURRENT\_USER]** 、 **[Software]** の順に展開します。
7. **HKEY\_CURRENT\_USER\\Software** の下にある **\[Manufacturer\]** キーを削除します。
8. アドインのインストール用のレジストリ キーを追加するには、**User/Machine Hive** キーを右クリックして、 **[新しいキー]** を選択します。 新しいキーの名前には、「**Software**」 というテキストを使用します。 新しく作成した **Software** キーを右クリックし、「**Microsoft**」というテキストを含む新しいキーを作成します。
9. 同様のプロセスを使用して、アドインの登録に必要なキー階層全体を作成します。

    **User/Machine Hive\\Software\\Microsoft\\Office\\Excel\\Addins\\SampleCompany.ExcelAddIn**

    会社名は、一意性を持たせるためにアドイン名のプレフィックスとしてよく使用されます。

10. **[SampleCompany.ExcelAddIn]** キーを右クリックして **[新規]** を選択し、 **[文字列値]** をクリックします。 [名前] に「**Description**」というテキストを使用します。
11. この手順を使用して、以下の 3 つの値をさらに追加します。
    - **FriendlyName** (**String** 型)
    - **LoadBehavior** (**DWORD** 型)
    - **Manifest** (**String** 型)

12. レジストリ エディターで **Description** 値を右クリックし、 **[プロパティ ウィンドウ]** をクリックします。 **[プロパティ ウィンドウ]** で、[値] プロパティに「**Excel Demo AddIn**」と入力します。
13. レジストリ エディターで **FriendlyName** キーを選択します。 **[プロパティ ウィンドウ]** で、 **[値]** プロパティを「**Excel Demo AddIn**」に変更します。
14. レジストリ エディターで **LoadBehavior** キーを選択します。 **[プロパティ ウィンドウ]** で、 **[値]** プロパティを「**3**」に変更します。 LoadBehavior の「3」という値は、ホスト アプリケーションの起動時にアドインが読み込まれる必要があることを示します。 読み込み動作の詳細については、「[VSTO アドインのレジストリ エントリ](registry-entries-for-vsto-add-ins.md)」を参照してください。

15. レジストリ エディターで **Manifest** キーを選択します。 **[プロパティ ウィンドウ]** で、 **[値]** プロパティを「**file:///[TARGETDIR]ExcelAddIn.vsto|vstolocal**」に変更します。

    ![レジストリ エディターのスクリーンショット](media/setup-project-figure-6.png)

    **図 6: レジストリ キーの設定**

      VSTO ランタイムは、このレジストリ キーを使用して配置マニフェストを検索します。 [TARGETDIR] マクロは、アドインがインストールされているフォルダーに置き換えられます。 このマクロには末尾に \ 文字が追加されるため、配置マニフェストのファイル名は、\ 文字の付かない ExcelAddIn.vsto にする必要があります。
      **vstolocal** 接尾辞は、ClickOnce キャッシュではなくこの場所からアドインが読み込まれる必要があることを VSTO ランタイムに通知します。 この接尾辞を削除すると、ランタイムによってカスタマイズが ClickOnce キャッシュにコピーされます。

   >[!WARNING]
   >Visual Studio でのレジストリ エディターの扱いには十分注意してください。 たとえば、間違ったキーに DeleteAtUninstall を誤って設定すると、レジストリのアクティブな部分が削除されて、ユーザーのコンピューターが不整合な状態になるか、さらに悪いことに、破損した状態になる可能性があります。

64 ビット版 Office では、64 ビット レジストリ ハイブを使用してアドインを検索します。64 ビット レジストリ ハイブの下にアドインを登録する場合は、セットアップ プロジェクトのターゲット プラットフォームを 64 ビットのみに設定する必要があります。

1. ソリューション エクスプローラーで、**OfficeAddInSetup** プロジェクトを選択します。
2. **[プロパティ]** ウィンドウにアクセスし、 **[TargetPlatform]** プロパティを **[x64]** に設定します。

32 ビット版と 64 ビット版の両方の Office 用にアドインをインストールする場合は、2 つの別々の MSI パッケージを作成する必要があります。 32 ビット版と 64 ビット版にそれぞれ 1 つずつです。

  ![64 ビット版 Office にアドインを登録するためのターゲット プラットフォームを示す [プロパティ] ウィンドウのスクリーンショット](media/setup-project-figure-7.jpg)

  **図 7: 64 ビット版 Office にアドインを登録するためのターゲット プラットフォーム**

MSI パッケージを使用してアドインまたはソリューションをインストールする場合、インストール時に必須の前提条件がインストールされないことがあります。 MSI で起動条件を使用すると、必須コンポーネントがインストールされていない場合にアドインのインストールをブロックできます。

### <a name="configure-a-launch-condition-to-detect-the-vsto-runtime"></a>VSTO ランタイムを検出するための起動条件を構成する

1. **ソリューション エクスプローラー** で、 **[OfficeAddInSetup]** を右クリックします。
2. **[表示]** を展開します。
3. **[起動条件]** をクリックします。
4. **[起動条件 (OfficeAddInSetup)]** エディターで、 **[ターゲット マシンの要件]** を右クリックしてから、 **[レジストリの起動条件の追加]** をクリックします。 この検索条件では、VSTO ランタイムでインストールされるキーをレジストリで検索できます。 キーの値はその後、名前付きプロパティを通じて、インストーラーのさまざまな部分で使用できます。 起動条件では、検索条件で定義されたプロパティを使用して特定の値を確認します。
5. **[起動条件 (OfficeAddInSetup)]** エディターで、 **[Search for RegistryEntry1]** 検索条件を選択し、条件を右クリックして、 **[プロパティ ウィンドウ]** を選択します。

6. **[プロパティ]** ウィンドウで、次のプロパティを設定します。
   1. **(Name)** の値を **Search for VSTO 2010 Runtime** (VSTO 2010 ランタイムの検索) に設定します。
   2. **Property** の値を **VSTORUNTIMEREDIST** に変更します。
   3. **RegKey** の値を **SOFTWARE\\Microsoft\\VSTO Runtime Setup\\v4R** に設定します。
   4. **Root** プロパティの設定を **vsdrrHKLM** のままにします。
   5. **Value** プロパティを **Version** に変更します。

7. **[起動条件 (OfficeAddInSetup)]** エディターで、 **[Condition1]** 起動条件を選択し、条件を右クリックして、 **[プロパティ ウィンドウ]** を選択します。
8. [プロパティ] ウィンドウで、次のプロパティを設定します。
   1. **(Name)** を **Verify VSTO 2010 Runtime availability** (VSTO 2010 ランタイムの可用性の検証) に設定します。
   2. **Condition** の値を **VSTORUNTIMEREDIST\>="10.0.30319"** に変更します。
   3. **InstallUrl** プロパティを空白のままにします。
   4. **Message** を **The Visual Studio 2010 Tools for Office Runtime is not installed. Please run Setup.exe to install the Add-in** (Visual Studio 2010 Tools for Office ランタイムがインストールされていません。Setup.exe を実行してアドインをインストールしてください) に設定します。

        ![ランタイムの可用性の検証という起動条件の [プロパティ] ウィンドウのスクリーンショット](media/setup-project-figure-8.jpg)

        **図 8: ランタイムの可用性の検証という起動条件の [プロパティ] ウィンドウ**

 上記の起動条件では、ブートストラップ パッケージによって VSTO ランタイムがインストールされるときにその存在を明示的に確認します。

### <a name="configure-a-launch-condition-to-detect-the-vsto-runtime-installed-by-office"></a>Office によってインストールされた VSTO ランタイムを検出するための起動条件を構成する

1. **[起動条件 (OfficeAddInSetup)]** エディターで、 **[ターゲット マシンの検索]** を右クリックしてから、 **[レジストリ検索の追加]** をクリックします。
2. **[Search for RegistryEntry1]** 検索条件を選択し、条件を右クリックして、 **[プロパティ ウィンドウ]** を選択します。
3. **[プロパティ]** ウィンドウで、次のプロパティを設定します。
    1. **(Name)** の値を **Search for Office VSTO Runtime** (Office VSTO ランタイムの検索) に設定します。
    2. **Property** の値を **OfficeRuntime** に変更します。
    3. **RegKey** の値を **SOFTWARE\\Microsoft\\VSTO Runtime Setup\\v4** に設定します。
    4. **Root** プロパティの設定を **vsdrrHKLM** のままにします。
    5. **Value** プロパティを **Version** に変更します。

4. **[起動条件 (OfficeAddInSetup)]** エディターで、前に定義した **[Verify VSTO 2010 Runtime availability]** 起動条件を選択し、条件を右クリックして、 **[プロパティ ウィンドウ]** を選択します。

5. **Condition** プロパティの値を **VSTORUNTIMEREDIST \>="10.0.30319" OR OFFICERUNTIME\>="10.0.21022"** に変更します。 バージョン番号は、アドインで必要とされるランタイムのバージョンによって異なる可能性があります。

    ![起動条件の [プロパティ] ウィンドウのスクリーンショット](media/setup-project-figure-9.jpg)
  
    **図 9: 再頒布可能パッケージまたは Office の起動条件を通じてランタイムの可用性を検証するための [プロパティ] ウィンドウ**

アドインが .NET Framework 4 以降を対象としている場合は、参照されるプライマリ相互運用機能アセンブリ (PIA) 内の型が VSTO アセンブリに埋め込まれることがあります。

アドインに相互運用機能型が埋め込まれるかどうかを確認するには、次の手順を実行します。

1. ソリューション エクスプローラーで、[参照] ノードを展開します。
2. PIA 参照の 1 つ ( **[Office]** など) を選択します。
3. F4 キーを押すか、アセンブリのコンテキスト メニューから [プロパティ] を選択して、[プロパティ] ウィンドウを表示します。
4. **[相互運用機能型の埋め込み]** プロパティの値を確認します。

値が **True** に設定されている場合は、型が埋め込まれるため、「[**セットアップ プロジェクトをビルドするには**](#to-build-the-setup-project)」セクションに進むことができます。

詳細については、「[型の等価性と埋め込まれた相互運用機能型](/dotnet/framework/interop/type-equivalence-and-embedded-interop-types)」を参照してください

### <a name="to-configure-launch-conditions-to-detect-that-for-office-pias"></a>Office PIA で検出するための起動条件を構成するには

1. **[起動条件 (OfficeAddInSetup)]** エディターで、 **[Requirements on Target Machine]** \(ターゲット マシンでの要件)を右クリックしてから、 **[Windows インストーラーの起動条件の追加]** をクリックします。 この起動条件では、特定のコンポーネント ID を検索する方法で、Office PIA を検索します。
2. **[Search for Component1]** を右クリックし、 **[プロパティ ウィンドウ]** をクリックして起動条件のプロパティを表示します。
3. **[プロパティ]** ウィンドウで、次のプロパティを設定します。

    1. **(Name)** プロパティの値を **Search for Office Shared PIA** (Office 共有 PIA の検索) に変更します。
    2. **ComponentID** の値を、使用している Office コンポーネントのコンポーネント ID に変更します。 コンポーネント ID の一覧は、以下の表で確認できます ( **{64E2917E-AA13-4CA4-BFFE-EA6EDA3AFCB4}** など)。
    3. **Property** プロパティの値を **HASSHAREDPIA** に変更します。

4. **[起動条件 (OfficeAddInSetup)]** エディターで、 **[Condition1]** を右クリックし、 **[プロパティ ウィンドウ]** をクリックして起動条件のプロパティを表示します。

5. **Condition1** の次のプロパティを変更します。

    1. **(Name)** を **Verify Office Shared PIA availability** (Office 共有 PIA の可用性の検証) に変更します。
    2. **Condition** を **HASSHAREDPIA** に変更します。
    3. **InstallUrl** を空白のままにします。
    4. **Message** を **A required component for interacting with Excel is not available. Please run setup.exe** (Excel との対話に必要なコンポーネントが使用できません。setup.exe を実行してください) に変更します。

    ![Office 共有 PIA の検証という起動条件の [プロパティ] ウィンドウのスクリーンショット](media/setup-project-figure-10.jpg)
  
    **図 10: Office 共有 PIA の検証という起動条件の [プロパティ] ウィンドウ**

### <a name="component-ids-of-the-primary-interop-assemblies-for-microsoft-office"></a>Microsoft Office 用のプライマリ相互運用機能アセンブリのコンポーネント ID

|プライマリ相互運用機能アセンブリ|Office 2010|Office 2013|Office 2013 (64 ビット)|Office 2016|Office 2016 (64 ビット)|
|------------------------|------------------------|------------------------|------------------------|------------------------|------------------------|
|Excel|{EA7564AC-C67D-4868-BE5C-26E4FC2223FF}|{C8A65ABE-3270-4FD7-B854-50C8082C8F39}|{E3BD1151-B9CA-4D45-A77E-51A6E0ED322A}|C4ACE6DB-AA99-401F-8BE6-8784BD09F003}|{C4ACE6DB-AA99-401F-8BE6-8784BD09F003}|
|InfoPath|{4153F732-D670-4E44-8AB7-500F2B576BDA}|{0F825A16-25B2-4771-A497-FC8AF3B355D8}|{C5BBD36E-B320-47EF-A512-556B99CB7E41}|-|-|
|Outlook|{1D844339-3DAE-413E-BC13-62D6A52816B2}|{F9F828D5-9F0B-46F9-9E3E-9C59F3C5E136}|{7824A03F-28CC-4371-BC54-93D15EFC1E7F}|{7C6D92EF-7B45-46E5-8670-819663220E4E}|{7C6D92EF-7B45-46E5-8670-819663220E4E}|
|PowerPoint|{EECBA6B8-3A62-44AD-99EB-8666265466F9}|{813139AD-6DAB-4DDD-8C6D-0CA30D073B41}|{05758318-BCFD-4288-AD8D-81185841C235}|{E0A76492-0FD5-4EC2-8570-AE1BAA61DC88}|{E0A76492-0FD5-4EC2-8570-AE1BAA61DC88}|
|Visio|{3EA123B5-6316-452E-9D51-A489E06E2347}|{C1713368-12A8-41F1-ACA1-934B01AD6EEB}|{2CC0B221-22D2-4C15-A9FB-DE818E51AF75}|{2D4540EC-2C88-4C28-AE88-2614B5460648}|{2D4540EC-2C88-4C28-AE88-2614B5460648}|
|Word|{8B74A499-37F8-4DEA-B5A0-D72FC501CEFA}|{9FE736B7-B1EE-410C-8D07-082891C3DAC8}|{13C07AF5-B206-4A48-BB5B-B8022333E3CA}|{DC5CCACD-A7AC-4FD3-9F70-9454B5DE5161}|{DC5CCACD-A7AC-4FD3-9F70-9454B5DE5161}|
|Microsoft Forms 2.0|{B2279272-3FD2-434D-B94E-E4E0F8561AC4}|{B2279272-3FD2-434D-B94E-E4E0F8561AC4}|{A5A30117-2D2A-4C5C-B3C8-8897AC32C2AC}|-|-|
|Microsoft Graph|{011B9112-EBB1-4A6C-86CB-C2FDC9EA7B0E}|{52DA4B37-B8EB-4B7F-89C1-824654CE4C70}|{24706F33-F0CE-4EB4-BC91-9E935394F510}|-|-|
|スマート タグ|{7102C98C-EF47-4F04-A227-FE33650BF954}|{487A7921-EB3A-4262-BB5B-A5736B732486}|{74EFC1F9-747D-4867-B951-EFCF29F51AF7}|-|-|
|Office 共有|{64E2917E-AA13-4CA4-BFFE-EA6EDA3AFCB4}|{6A174BDB-0049-4D1C-86EF-3114CB0C4C4E}|{76601EBB-44A7-49EE-8DE3-7B7B9D7EBB05}|{625F5772-C1B3-497E-8ABE-7254EDB00506}|{625F5772-C1B3-497E-8ABE-7254EDB00506}|
|Project|{957A4EC0-E67B-4E86-A383-6AF7270B216A}|{1C50E422-24FA-44A9-A120-E88280C8C341}|{706D7F44-8231-489D-9B25-3025ADE9F114}|{107BCD9A-F1DC-4004-A444-33706FC10058}|{107BCD9A-F1DC-4004-A444-33706FC10058}|

  ![最後の起動条件のスクリーンショット](media/setup-project-figure-11.jpg)

  **図 11: 最後の起動条件**

ExcelAddIn のインストールの起動条件をさらに絞り込むことができます。 たとえば、対象となる実際の Office アプリケーションがインストールされているかどうかを確認すると便利な場合があります。

### <a name="to-build-the-setup-project"></a>セットアップ プロジェクトをビルドするには

1. **ソリューション エクスプローラー** で、**OfficeAddInSetup** プロジェクトを右クリックして、 **[ビルド]** をクリックします。
2. **Windows エクスプローラー** を使用して、**OfficeAddInSetup** プロジェクトの出力ディレクトリに移動し、選択したビルド構成に応じて Release または Debug フォルダーにアクセスします。 そのフォルダーのすべてのファイルを、ユーザーがアクセスできる場所にコピーします。

ExcelAddIn のセットアップをテストするには

1. **OfficeAddInSetup** をコピーした場所に移動します。
2. setup.exe ファイルをダブルクリックして、**OfficeAddInSetup** アドインをインストールします。 表示されたソフトウェア ライセンス条項に同意し、セットアップ ウィザードを完了して、ユーザーのコンピューターにアドインをインストールします。

Excel Office ソリューションがインストールされ、セットアップ時に指定した場所から実行されます。

## <a name="additional-requirements-for-document-level-solutions"></a>ドキュメント レベルのソリューションの追加要件

ドキュメント レベルのソリューションを配置する場合は、Windows インストーラーのセットアップ プロジェクトでいくつかの異なる構成手順を実行する必要があります。

ドキュメント レベルのソリューションを配置するための基本的な手順の一覧を次に示します。

- Visual Studio セットアップ プロジェクトを作成します。
- ドキュメント レベルのソリューションのプライマリ出力を追加します。 プライマリ出力には、Microsoft Office ドキュメントも含まれます。
- 配置およびアプリケーション マニフェストを Loose ファイルとして追加します。
- 依存コンポーネントをインストーラー パッケージから除外します (すべてのユーティリティ アセンブリを除く)。
- 前提条件パッケージを構成します。
- 起動条件を構成します。
- セットアップ プロジェクトをビルドし、結果を配置場所にコピーします。
- セットアップを実行して、ドキュメント レベルのソリューションをユーザーのコンピューターに配置します。
- 必要に応じてカスタム ドキュメントのプロパティを更新します。

### <a name="changing-the-location-of-the-deployed-document"></a>配置されたドキュメントの場所の変更

Office ドキュメント内のプロパティは、ドキュメント レベルのソリューションを検索するために使用されます。 ドキュメントが VSTO アセンブリと同じフォルダーにインストールされている場合、変更は必要ありません。 しかし、それが別のフォルダーにインストールされている場合は、セットアップ中にこれらのプロパティを更新する必要があります。

これらのドキュメント プロパティの詳細については、「[カスタム ドキュメント プロパティの概要](custom-document-properties-overview.md)」を参照してください。

これらのプロパティを変更するには、セットアップ中にカスタム アクションを使用する必要があります。

次の例では、ExcelWorkbookProject というドキュメント レベルのソリューションと ExcelWorkbookSetup というセットアップ プロジェクトを使用します。 ExcelWorkbookSetup プロジェクトは、レジストリ キーの設定を除き、上記と同じ手順を使用して構成されます。

カスタム アクション プロジェクトを Visual Studio ソリューションに追加するには

1. 新しい .NET コンソール プロジェクトをソリューションに追加するために、**ソリューション エクスプローラー** で **[Office Document Deployment Project]** を右クリックします。
2. **[追加]** を展開し、 **[新しいプロジェクト]** をクリックします。
3. [コンソール アプリ] テンプレートを選択し、プロジェクトに「**AddCustomizationCustomAction**」という名前を付けます。

    ![ソリューション エクスプローラー - AddCustomizationCustomAction のスクリーンショット](media/setup-project-figure-15.jpg)
  
    **図 12: ソリューション エクスプローラー - AddCustomizationCustomAction**

4. 以下のアセンブリへの参照を追加します。
    1. System.ComponentModel
    2. System.Configuration.Install
    3. Microsoft.VisualStudio.Tools.Applications
    4. Microsoft.VisualStudio.Tools.Applications.ServerDocument

5. 以下のコードを Program.cs または Program.vb にコピーします

```csharp
    using System;
    using System.IO;
    using System.Collections;
    using System.ComponentModel;
    using System.Configuration.Install;
    using Microsoft.VisualStudio.Tools.Applications;
    using Microsoft.VisualStudio.Tools.Applications.Runtime;

    namespace AddCustomizationCustomAction
    {
        [RunInstaller(true)]
        public class AddCustomizations : Installer
        {
            public AddCustomizations() : base() { }

            public override void Install(IDictionary savedState)
            {
                base.Install(savedState);

                //Get the CustomActionData Parameters
                string documentLocation = Context.Parameters.ContainsKey("documentLocation") ? Context.Parameters["documentLocation"] : String.Empty;
                string assemblyLocation = Context.Parameters.ContainsKey("assemblyLocation") ? Context.Parameters["assemblyLocation"] : String.Empty;
                string deploymentManifestLocation = Context.Parameters.ContainsKey("deploymentManifestLocation") ? Context.Parameters["deploymentManifestLocation"] : String.Empty;
                Guid solutionID = Context.Parameters.ContainsKey("solutionID") ? new Guid(Context.Parameters["solutionID"]) : new Guid();

                string newDocLocation = Path.Combine(Environment.GetFolderPath(Environment.SpecialFolder.MyDocuments), Path.GetFileName(documentLocation));

                try
                {
                    //Move the file and set the Customizations
                    if (Uri.TryCreate(deploymentManifestLocation, UriKind.Absolute, out Uri docManifestLocationUri))
                    {
                        File.Move(documentLocation, newDocLocation);
                        ServerDocument.RemoveCustomization(newDocLocation);
                        ServerDocument.AddCustomization(newDocLocation, assemblyLocation,
                                                        solutionID, docManifestLocationUri,
                                                        true, out string[] nonpublicCachedDataMembers);
                    }
                    else
                    {
                        LogMessage("The document could not be customized.");
                    }
                }
                catch (ArgumentException)
                {
                    LogMessage("The document could not be customized.");
                }
                catch (DocumentNotCustomizedException)
                {
                    LogMessage("The document could not be customized.");
                }
                catch (InvalidOperationException)
                {
                    LogMessage("The customization could not be removed.");
                }
                catch (IOException)
                {
                    LogMessage("The document does not exist or is read-only.");
                }
            }

            public override void Rollback(IDictionary savedState)
            {
                base.Rollback(savedState);
                DeleteDocument();
            }
            public override void Uninstall(IDictionary savedState)
            {
                base.Uninstall(savedState);
                DeleteDocument();
            }
            private void DeleteDocument()
            {
                string documentLocation = Context.Parameters.ContainsKey("documentLocation") ? Context.Parameters["documentLocation"] : String.Empty;

                try
                {
                    File.Delete(Path.Combine(Environment.GetFolderPath(Environment.SpecialFolder.MyDocuments), Path.GetFileName(documentLocation)));
                }
                catch (Exception)
                {
                    LogMessage("The document doesn't exist or is read-only.");
                }
            }
            private void LogMessage(string Message)
            {
                if (Context.Parameters.ContainsKey("LogFile"))
                {
                    Context.LogMessage(Message);
                }
            }

            static void Main() { }
            }
    }
```

ドキュメントにカスタマイズを追加する場合は、VSTO ドキュメント レベルのソリューションのソリューション ID が必要です。 この値は、Visual Studio プロジェクト ファイルから取得されます。

ソリューション ID を取得するには

1. **[ビルド]** メニューの **[ソリューションのビルド]** をクリックしてドキュメント レベルのソリューションをビルドし、ソリューション ID プロパティをプロジェクト ファイルに追加します。
2. **ソリューション エクスプローラー** で、**ExcelWorkbookProject** というドキュメント レベルのプロジェクトを右クリックします。
3. **[プロジェクトのアンロード]** をクリックして、Visual Studio 内からプロジェクト ファイルにアクセスします。

    ![ソリューション エクスプローラー - Excel ドキュメント ソリューションのアンロードのスクリーンショット](media/setup-project-figure-16.jpg)

    **図 13: Excel ドキュメント ソリューションのアンロード**

4. **ソリューション エクスプローラー** で、 **[ExcelWorkbookProject]** を右クリックして、 **[ExcelWorkbookProject.vbproj の編集]** または **[ExcelWorkbookProject.csproj の編集]** をクリックします。
5. **ExcelWorkbookProject** のエディターで、**PropertyGroup** 要素内の **SolutionID** 要素を見つけます。
6. この要素の GUID 値をコピーします。

    ![SolutionID の取得](media/setup-project-figure-17.jpg)

    **図 14: SolutionID の取得**

7. **ソリューション エクスプローラー** で、 **[ExcelWorkbookProject]** を右クリックして、 **[プロジェクトの再読み込み]** をクリックします。
8. 表示されるダイアログ ボックスで **[はい]** をクリックして、**ExcelWorkbookProject** のエディターを閉じます。
9. この **ソリューション ID** は、インストールのカスタム アクションで使用されます。

最後の手順では、 **[インストール]** および **[アンインストール]** ステップ用のカスタム アクションを構成します。

### <a name="to-configure-the-setup-project"></a>セットアップ プロジェクトを構成するには

1. **ソリューション エクスプローラー** で、 **[ExcelWorkbookSetup]** を右クリックし、 **[追加]** を展開して、 **[プロジェクト出力]** をクリックします。
2. **[プロジェクト出力グループの追加]** ダイアログ ボックスの **[プロジェクト]** ボックスの一覧で、 **[AddCustomizationCustomAction]** をクリックします。
3. **[プライマリ出力]** を選択し、 **[OK]** をクリックしてダイアログ ボックスを閉じ、そのカスタム アクションを含むアセンブリをセットアップ プロジェクトに追加します。

    ![ドキュメント マニフェストのカスタム アクション - [プロジェクト出力グループの追加] ウィンドウのスクリーンショット](media/setup-project-figure-18.jpg)

    **図 15: ドキュメント マニフェストのカスタム アクション - [プロジェクト出力グループの追加]**

4. **ソリューション エクスプローラー** で、 **[ExcelWorkbookSetup]** を右クリックします。
5. **[表示]** を展開し、 **[カスタム アクション]** をクリックします。
6. **[カスタム アクション (ExcelWorkbookSetup)]** エディターで、 **[カスタム アクション]** を右クリックして、 **[カスタム アクションの追加]** をクリックします。
7. **[プロジェクト内の項目の選択]** ダイアログ ボックスの **[検索対象]** ボックスの一覧で、 **[アプリケーション フォルダー]** をクリックします。 **[Primary output from AddCustomizationCustomAction(Active)]** を選択し、 **[OK]** をクリックして、そのカスタム アクションを [インストール] ステップに追加します。
8. **[インストール]** ノードで、 **[Primary output from AddCustomizationCustomAction(Active)** ] を右クリックして、 **[名前の変更]** をクリックします。 カスタム アクションに「**Copy document to My Documents and attach customization**」(ドキュメントを [マイ ドキュメント] にコピーし、カスタマイズを添付する) という名前を付けます。
9. **[アンインストール]** ノードで、 **[Primary output from AddCustomizationCustomAction(Active)** ] を右クリックして、 **[名前の変更]** をクリックします。 カスタム アクションに「**Remove document from the Documents folder**」(ドキュメントを [ドキュメント] フォルダーから削除する) という名前を付けます。

    ![ドキュメント マニフェストの [カスタム アクション] ウィンドウのスクリーンショット](media/setup-project-figure-19.jpg)

    **図 16: ドキュメント マニフェストの [カスタム アクション] ウィンドウ**

10. **[カスタム アクション (ExcelWorkbookSetup)]** エディターで、 **[Copy document to My Documents and attach customization]** を右クリックして、 **[プロパティ ウィンドウ]** をクリックします。
11. **CustomActionData** の **[プロパティ]** ウィンドウで、カスタマイズ DLL の場所、配置マニフェスト、Microsoft Office ドキュメントの場所を入力します。 SolutionID も必要です。
12. セットアップ エラーをログ ファイルに記録する場合は、LogFile パラメーターも含めます。
s
    ``` text
    /assemblyLocation="[INSTALLDIR]ExcelWorkbookProject.dll" /deploymentManifestLocation="[INSTALLDIR]ExcelWorkbookProject.vsto" /documentLocation="[INSTALLDIR]ExcelWorkbookProject.xlsx" /solutionID="Your Solution ID" /LogFile="[TARGETDIR]Setup.log"
    ```

    ![ドキュメントを [マイ ドキュメント] にコピーするカスタム アクションの [プロパティ] ウィンドウのスクリーンショット](media/setup-project-figure-20.jpg)

    **図 17: ドキュメントを [マイ ドキュメント] にコピーするカスタム アクション**

13. [アンインストール] 用のカスタム アクションには、ドキュメントの名前が必要です。これは、**CustomActionData** 内の同じ documentLocation パラメーターを使用して指定できます

    ``` text
    /documentLocation="[INSTALLDIR]ExcelWorkbookProject.xlsx"
    ```

14. **ExcelWorkbookSetup** プロジェクトをコンパイルして配置します。
15. **[マイ ドキュメント]** フォルダーを検索し、ExcelWorkbookProject.xlsx ファイルを開きます。

## <a name="additional-resources"></a>その他の情報

[方法: Visual Studio Tools for Office ランタイムをインストールする](how-to-install-the-visual-studio-tools-for-office-runtime-redistributable.md)

[Office Primary Interop Assemblies](office-primary-interop-assemblies.md)

[VSTO アドインのレジストリ エントリ](registry-entries-for-vsto-add-ins.md)

[Custom Document Properties Overview](custom-document-properties-overview.md)

[Windows レジストリでのフォーム領域の指定](/office/vba/outlook/concepts/creating-form-regions/specifying-form-regions-in-the-windows-registry)

[Granting Trust to Documents](granting-trust-to-documents.md)

## <a name="about-the-authors"></a>作成者について

Wouter van Vugt 氏は、Office Open XML テクノロジにおける Microsoft MVP であり、SharePoint、Microsoft Office、関連する .NET テクノロジを用いた Office Business Applications (OBA) の作成に重点を置く独立系コンサルタントです。
Wouter は、[MSDN](/previous-versions/office/developer/office-2007/bb879915(v=office.12)) などの開発者コミュニティのサイトに頻繁に参加しています。 ホワイト ペーパーや記事を公表するだけでなく、オンラインで購入できる『Open XML: Explained』という電子書籍も出版しています。
Wouter は、さまざまなチャネルを通じて最先端のテクニカル コンテンツを配信することに注力する、Code-Counsel というオランダ企業の創設者です。 Wouter の詳しいプロフィールについては、ご本人のブログをご覧ください。

Ted Pattison 氏は、SharePoint MVP、作家、トレーナーであり、また Ted Pattison Group の創設者です。 2005 年の秋、Ted は Microsoft の Developer Platform Evangelism グループに採用され、Windows SharePoint Services 3.0 と Microsoft Office SharePoint Server 2007 用の上級開発者向けトレーニング カリキュラムを作成しました。 それ以来、Ted は SharePoint 2007 テクノロジのプロフェッショナルな開発者の教育に専念してきました。 Ted は、SharePoint をビジネス ソリューションの構築用の開発プラットフォームとして使用する方法に重点を置く『Inside Windows SharePoint Services 3.0』という Microsoft Press の書籍を執筆しました。 また、Ted は『Office Space』 という MSDN 雑誌に開発者向けコラムも執筆しています。
