---
title: DSL の MSI および VSIX 配置
description: 自分のコンピューターまたは他のコンピューターにドメイン固有言語 (DSL) をインストールする方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
author: JoshuaPartlow
ms.author: joshuapa
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: bf6082ec8860f7f50e758eb65a8471ece94103aa
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99950412"
---
# <a name="msi-and-vsix-deployment-of-a-dsl"></a>DSL の MSI および VSIX 配置
ドメイン固有言語は、自分のコンピューターにもその他のコンピューターにインストールできます。 Visual Studio は、あらかじめターゲット コンピューターにインストールされている必要があります。

## <a name="choosing-between-vsix-and-msi-deployment"></a><a name="which"></a> VSIX と MSI の配置の選択
 ドメイン固有言語を配置するには、次の 2 つの方法があります。

|メソッド|メリット|
|-|-|
|VSX (Visual Studio 拡張機能)|配置が非常に簡単: DslPackage プロジェクトから **.vsix** ファイルをコピーして実行します。<br /><br /> 詳細については、「[VSX を使用した DSL のインストールおよびアンインストール](#Installing)」を参照してください。|
|MSI (インストーラー ファイル)|-   ユーザーが DSL ファイルをダブルクリックして Visual Studio を開くことを許可します。<br />-   ターゲット コンピューターの DSL ファイルの種類にアイコンを関連付けます。<br />-   XSD (XML スキーマ) を DSL ファイルの種類に関連付けます。 これにより、ファイルが Visual Studio に読み込まれるときの警告が回避されます。<br /><br /> MSI を作成するには、ソリューションにセットアップ プロジェクトを追加する必要があります。<br /><br /> 詳細については、「[MSI ファイルを使用した DSL の配置](#msi)」を参照してください。|

## <a name="install-and-uninstall-a-dsl-by-using-the-vsx"></a><a name="Installing"></a> VSX を使用した DSL のインストールおよびアンインストール

DSL がこの方法でインストールされている場合、ユーザーは Visual Studio 内から DSL ファイルを開くことができますが、エクスプローラーからファイルを開くことはできません。

### <a name="to-install-a-dsl-by-using-the-vsx"></a>VSX を使用して DSL をインストールするには

1. DSL パッケージ プロジェクトによって作成された **.vsix** ファイルを見つけます。

   1. **ソリューション エクスプローラー** で **[DslPackage]** プロジェクトを右クリックし、 **[エクスプローラーでフォルダーを開く]** をクリックします。

   2. ファイル **bin\\\*\\** _YourProject_ **.DslPackage.vsix** を見つけます

2. DSL をインストールするターゲット コンピューターに **.vsix** ファイルをコピーします。 自分のコンピューターでも別のコンピューターでもかまいません。

   - ターゲット コンピューターには、実行時に DSL をサポートする [!INCLUDE[vs_current_short](../code-quality/includes/vs_current_short_md.md)] のいずれかのエディションが必要です。 詳細については、「[Visualization and Modeling SDK に対してサポートされている Visual Studio のエディション](../modeling/supported-visual-studio-editions-for-visualization-amp-modeling-sdk.md)」を参照してください。

   - ターゲット コンピューターには、**DslPackage\source.extensions.manifest** で指定されている Visual Studio のいずれかのエディションが必要です。

3. ターゲット コンピューターで **.vsix** ファイルをダブルクリックします。

    **Visual Studio 拡張機能インストーラー** が起動され、拡張機能がインストールされます。

4. [!INCLUDE[vs_current_short](../code-quality/includes/vs_current_short_md.md)]を起動または再起動します。

5. DSL をテストするには、Visual Studio を使用して、DSL 用に定義した拡張機能を含む新しいファイルを作成します。

### <a name="to-uninstall-a-dsl-that-was-installed-by-using-vsx"></a>VSX を使用してインストールされた DSL をアンインストールするには

1. **[ツール]** メニューの **[拡張機能と更新プログラム]** をクリックします。

2. **[インストール済みの拡張機能]** を展開します。

3. DSL が定義されている拡張機能を選択し、 **[アンインストール]** をクリックします。

   拡張機能の障害が原因で読み込みが失敗し、エラー ウィンドウにレポートが生成されることがまれにありますが、それは拡張機能マネージャーには表示されません。 その場合は、以下の場所からファイルを削除して、拡張機能を削除します。

   *LocalAppData* **\Microsoft\VisualStudio\10.0\Extensions**

## <a name="deploying-a-dsl-in-an-msi"></a><a name="msi"></a> MSI で DSL を配置する
 DSL 用の MSI (Windows インストーラー) ファイルを定義することで、ユーザーに Windows エクスプローラーから DSL ファイルを開くことを許可できます。 また、アイコンと簡単な説明をファイル名拡張子に関連付けることもできます。 また、MSI では、DSL ファイルの検証に使用できる XSD をインストールできます。 必要に応じて、同時にインストールされる他のコンポーネントを MSI に追加することができます。

 MSI ファイルとその他の配置オプションの詳細については、[アプリケーション、サービス、およびコンポーネントの配置](../deployment/deploying-applications-services-and-components.md)に関するページを参照してください。

 MSI をビルドするには、Visual Studio ソリューションにセットアップ プロジェクトを追加します。 セットアップ プロジェクトの最も簡単な作成方法は、[VMSDK サイト](https://code.msdn.microsoft.com/Visualization-and-Modeling-313535db)からダウンロードできる CreateMsiSetupProject.tt テンプレートを使用することです。

### <a name="to-deploy-a-dsl-in-an-msi"></a>DSL を MSI に配置するには

1. 拡張機能マニフェストで `InstalledByMsi` を設定します。 これにより、MSI 以外で VSX をインストールおよびアンインストールすることができなくなります。 これは、MSI に他のコンポーネントを含める場合に重要です。

   1. DslPackage\source.extension.tt を開きます

   2. `<SupportedProducts>` の前に次のコード行を挿入します。

       ```xml
       <InstalledByMsi>true</InstalledByMsi>
       ```

2. Windows エクスプローラーで DSL を表すアイコンを作成または編集します。 たとえば、**DslPackage\Resources\File.ico** を編集します

3. DSL の次の属性が正しいことを確認します。

   - DSL エクスプローラーでルート ノードをクリックし、プロパティ ウィンドウで次の内容を確認します。

       - 説明

       - Version

   - **[エディター]** ノードをクリックし、プロパティ ウィンドウの **[アイコン]** をクリックします。 **Dslpackage\Resources** でアイコン ファイルを参照するように値を設定します (**File.ico** など)

   - **[ビルド]** メニューの **[Configuration Manager]** を開き、 **[リリース]** や **[デバッグ]** など、ビルドする構成を選択します。

4. [Visualization and Modeling SDK のホームページ](https://code.msdn.microsoft.com/Visualization-and-Modeling-313535db)にアクセスし、 **[ダウンロード]** タブから **CreateMsiSetupProject.tt** をダウンロードします。

5. Dsl プロジェクトに **CreateMsiSetupProject.tt** を追加します。

    Visual Studio によって、**CreateMsiSetupProject** という名前のファイルが作成されます。

6. Windows エクスプローラーで、Dsl\\*.vdproj を Setup という名前の新しいフォルダーにコピーします。

    (必要に応じて、Dsl プロジェクトから CreateMsiSetupProject.tt を除外できるようになりました。)

7. **ソリューション エクスプローラー** で、既存のプロジェクトとして **Setup\\\*.vdproj** を追加します。

8. **[プロジェクト]** メニューの **[プロジェクトの依存関係]** をクリックします。

    **[プロジェクトの依存関係]** ダイアログ ボックスで、セットアップ プロジェクトを選択します。

    **[DslPackage]** の横にあるチェックボックスをオンにします。

9. ソリューションをリビルドします。

10. Windows エクスプローラーで、セットアップ プロジェクトでビルドされた MSI ファイルを見つけます。

     DSL をインストールするコンピューターに MSI ファイルをコピーします。 MSI ファイルをダブルクリックします。 インストーラーを実行します。

11. ターゲット コンピューターで、DSL のファイル拡張子を持つ新しいファイルを作成します。 次のことを確認します。

    - Windows エクスプローラーのリスト ビューでは、定義したアイコンと説明がファイルに表示されます。

    - ファイルをダブルクリックすると、Visual Studio が起動し、DSL エディターで DSL ファイルが開きます。

    必要に応じて、テキスト テンプレートを使用する代わりに、手動でセットアップ プロジェクトを作成することもできます。 この手順が含まれているチュートリアルについては、[Visualization and Modeling SDK ラボ](https://code.msdn.microsoft.com/DSLToolsLab/Release/ProjectReleases.aspx?ReleaseId=4207)の第 5 章を参照してください。

### <a name="to-uninstall-a-dsl-that-was-installed-from-an-msi"></a>MSI からインストールされた DSL をアンインストールするには

1. Windows で、コントロール パネルの **[プログラムと機能]** を開きます。

2. DSL をアンインストールします。

3. Visual Studio を再起動します。
