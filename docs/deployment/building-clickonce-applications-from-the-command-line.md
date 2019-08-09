---
title: コマンドラインから ClickOnce アプリケーションをビルドする |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- ClickOnce deployment, from command line
- publishing
- publishing, ClickOnce
ms.assetid: d9bc6212-c584-4f72-88c9-9a4b998c555e
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 9d8ce0753c63f1dcc177f36149cad9789ec150ab
ms.sourcegitcommit: a124076dfd6b4e5aecda4d01984fee7b0c034745
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/05/2019
ms.locfileid: "68787678"
---
# <a name="build-clickonce-applications-from-the-command-line"></a>ClickOnce アプリケーションのコマンド ラインからのビルド
で[!INCLUDE[vs_current_short](../code-quality/includes/vs_current_short_md.md)]は、統合開発環境 (IDE: integrated development environment) で作成されたプロジェクトであっても、コマンドラインからプロジェクトをビルドできます。 実際には、.NET Framework がインストールされて[!INCLUDE[vs_current_short](../code-quality/includes/vs_current_short_md.md)]いる別のコンピューターで、を使用して作成されたプロジェクトをリビルドすることができます。 これにより、たとえば、中央のビルドラボや、プロジェクト自体を構築する範囲を超えた高度なスクリプト手法を使用して、自動化されたプロセスを使用してビルドを再現できます。

## <a name="use-msbuild-to-reproduce-clickonce-application-deployments"></a>MSBuild を使用して ClickOnce アプリケーションの配置を再現する
 Msbuild/target: publish をコマンドラインで起動すると、msbuild システムに対してプロジェクトをビルドし、publish フォルダー [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]にアプリケーションを作成するように指示されます。 これは、IDE で [**発行**] コマンドを選択することと同じです。

 このコマンドは、Visual Studio のコマンドプロンプト環境のパスにある*msbuild.exe*を実行します。

 "ターゲット" は、コマンドの処理方法に関する MSBuild のインジケーターです。 キーターゲットは、"ビルド" ターゲットと "発行" ターゲットです。 ビルドターゲットは、IDE でビルドコマンドを選択する (または F5 キーを押す) ことに相当します。 プロジェクトをビルドするだけの場合は、「」と入力`msbuild`することでこれを実現できます。 このコマンドは、ビルドターゲットがによって[!INCLUDE[vs_current_short](../code-quality/includes/vs_current_short_md.md)]生成されるすべてのプロジェクトの既定のターゲットであるため、機能します。 これは、ビルドターゲットを明示的に指定する必要がないことを意味します。 したがって、 `msbuild` 「」 `msbuild /target:build`と入力した場合と同じ操作が実行されます。

 この`/target:publish`コマンドは、発行ターゲットを呼び出すように MSBuild に指示します。 発行ターゲットは、ビルドターゲットに依存します。 これは、発行操作がビルド操作のスーパーセットであることを意味します。 たとえば、Visual Basic またはC#ソースファイルのいずれかを変更した場合、対応するアセンブリは発行操作によって自動的に再構築されます。

 Mage.exe コマンドラインツールを使用[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]して[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]マニフェストを作成する完全な展開を生成する方法について[は、「チュートリアル:ClickOnce アプリケーション](../deployment/walkthrough-manually-deploying-a-clickonce-application.md)を手動で配置します。

## <a name="create-and-build-a-basic-clickonce-application-with-msbuild"></a>MSBuild を使用した基本的な ClickOnce アプリケーションの作成とビルド

#### <a name="to-create-and-publish-a-clickonce-project"></a>ClickOnce プロジェクトを作成および発行するには

1. Visual Studio を起動し、新しいプロジェクトを作成します。

    [ **Windows デスクトップアプリケーション**] プロジェクトテンプレートを選択し、 `CmdLineDemo`プロジェクトに名前を指定します。

1. [**ビルド**] メニューの [**発行**] をクリックします。

    この手順により、 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]アプリケーションの配置を生成するようにプロジェクトが適切に構成されます。

    発行ウィザードが表示されます。

1. 発行ウィザードで、[**完了**] をクリックします。

    Visual Studio によって、 *Publish*という既定の Web ページが生成されて表示されます。

1. プロジェクトを保存し、格納されているフォルダーの場所をメモします。

   上記の手順では[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 、初めて発行されたプロジェクトを作成します。 これで、IDE の外部でビルドを再現できます。

#### <a name="to-reproduce-the-build-from-the-command-line"></a>コマンドラインからビルドを再現するには

1. [!INCLUDE[vs_current_short](../code-quality/includes/vs_current_short_md.md)] を終了します。

2. Windows の [**スタート**] メニューから、[**すべてのプログラム**]、[ **Microsoft Visual Studio**]、[ **Visual Studio Tools**]、[ **Visual Studio コマンドプロンプト**] の順にクリックします。 これにより、現在のユーザーのルートフォルダーでコマンドプロンプトが開きます。

3. **Visual Studio のコマンドプロンプト**で、現在のディレクトリを、先ほど作成したプロジェクトの場所に変更します。 たとえば、「 `chdir My Documents\Visual Studio\Projects\CmdLineDemo`」と入力します。

4. 「 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]プロジェクトを作成および発行するには」で作成した既存のファイル`rmdir /s publish`を削除するには、「」と入力します。

    この手順は省略可能ですが、新しいファイルがすべてコマンドラインビルドによって生成されるようになります。

5. 「`msbuild /target:publish`」と入力します。

   上記の手順を実行すると[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 、 **Publish**という名前のプロジェクトのサブフォルダーにアプリケーションの完全配置が生成されます。 *Cmdlinedemo. アプリケーション*は[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]配置マニフェストです。 *Cmdlinedemo_ 1.0.0.0*というフォルダーには[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 、アプリケーションマニフェストである*cmdlinedemo .exe*および*cmdlinedemo .exe*というファイルが含まれています。 *Setup.exe* はブートストラップで、既定では .NET Framework をインストールするように構成されています。 Dotnetfx.exe フォルダーには、.NET Framework の再頒布可能ファイルが含まれています。 これは、Web 経由で、または UNC または CD/DVD 経由でアプリケーションをデプロイするために必要なファイルのセット全体です。
   
> [!NOTE]
> MSBuild システムでは、 **Publishdir**オプションを使用して、出力の場所を`msbuild /t:publish /p:PublishDir="<specific location>"`指定します。たとえば、のようにします。

## <a name="publish-properties"></a>[発行] プロパティ
 上記の手順でアプリケーションを発行すると、発行ウィザードによって次のプロパティがプロジェクトファイルに挿入されます。 これらのプロパティは、アプリケーション[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]の生成方法に直接影響します。

 *CmdLineDemo.vbproj* / *CmdLineDemo.csproj*で：

```xml
<AssemblyOriginatorKeyFile>WindowsApplication3.snk</AssemblyOriginatorKeyFile>
<GenerateManifests>true</GenerateManifests>
<TargetZone>LocalIntranet</TargetZone>
<PublisherName>Microsoft</PublisherName>
<ProductName>CmdLineDemo</ProductName>
<PublishUrl>http://localhost/CmdLineDemo</PublishUrl>
<Install>true</Install>
<ApplicationVersion>1.0.0.*</ApplicationVersion>
<ApplicationRevision>1</ApplicationRevision>
<UpdateEnabled>true</UpdateEnabled>
<UpdateRequired>false</UpdateRequired>
<UpdateMode>Foreground</UpdateMode>
<UpdateInterval>7</UpdateInterval>
<UpdateIntervalUnits>Days</UpdateIntervalUnits>
<UpdateUrlEnabled>false</UpdateUrlEnabled>
<IsWebBootstrapper>true</IsWebBootstrapper>
<BootstrapperEnabled>true</BootstrapperEnabled>
```

 これらのプロパティは、プロジェクトファイル自体を変更せずに、コマンドラインでオーバーライドできます。 たとえば、次のようにすると[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 、ブートストラップを使用せずにアプリケーションの展開がビルドされます。

```cmd
msbuild /target:publish /property:BootstrapperEnabled=false
```

 発行プロパティは[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 、**プロジェクトデザイナー**の [**発行**]、[**セキュリティ**]、[**署名**] の各プロパティページからで制御されます。 次に示すのは、発行プロパティの説明と、アプリケーションデザイナーのさまざまなプロパティページでそれぞれがどのように設定されているかを示しています。

- `AssemblyOriginatorKeyFile`[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]アプリケーションマニフェストに署名するために使用するキーファイルを指定します。 この同じキーを使用して、アセンブリに厳密な名前を割り当てることもできます。 このプロパティは、**プロジェクトデザイナー**の [**署名**] ページで設定します。

  [**セキュリティ**] ページでは、次のプロパティが設定されます。

- **ClickOnce セキュリティ設定を有効に**すると、マニフェストを生成するかどうか[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]が決まります。 プロジェクトが最初に作成され[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]たとき、マニフェストの生成は既定で無効になっています。 初回の発行時に、ウィザードによって自動的にこのフラグがオンになります。

- **Targetzone**は、 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]アプリケーションマニフェストに出力する信頼のレベルを決定します。 指定できる値は、"Internet"、"LocalIntranet"、および "Custom" です。 インターネットとイントラネットでは、既定のアクセス許可セットが[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]アプリケーションマニフェストに出力されます。 既定値は LocalIntranet で、基本的には完全信頼であることを意味します。 Custom は、基本アプリケーションの*マニフェスト*ファイルで明示的に指定されたアクセス許可のみが[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]アプリケーションマニフェストに出力されることを指定します。 *アプリケーションのマニフェスト*ファイルは、信頼情報の定義のみを含む部分的なマニフェストファイルです。 これは、[**セキュリティ**] ページでアクセス許可を構成するときにプロジェクトに自動的に追加される、非表示のファイルです。

  [**発行**] ページでは、次のプロパティが設定されます。

- `PublishUrl`は、アプリケーションが IDE で公開される場所です。 `InstallUrl`また[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] は`UpdateUrl`プロパティが指定されていない場合は、アプリケーションマニフェストに挿入されます。

- `ApplicationVersion`[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]アプリケーションのバージョンを指定します。 これは4桁のバージョン番号です。 最後の数字が "*" `ApplicationRevision`の場合、ビルド時にマニフェストに挿入される値の代わりにが使用されます。

- `ApplicationRevision`リビジョンを指定します。 これは、IDE で公開するたびにインクリメントされる整数です。 これは、コマンドラインで実行されるビルドに対して自動的にはインクリメントされないことに注意してください。

- `Install`アプリケーションがインストールされているアプリケーションであるか、Web アプリケーションから実行されているかを判断します。

- `InstallUrl`(表示されません) は、ユーザーがアプリケーションをインストールする場所です。 この値が指定されている場合 、 `IsWebBootstrapper`プロパティが有効になっている場合は、*setup.exe* ブートストラップに書き込まれます。 `UpdateUrl`が指定されていない場合は、アプリケーションマニフェストにも挿入されます。

- `SupportUrl`(表示されません) は、インストールされているアプリケーションの [**プログラムの追加と削除**] ダイアログボックスにリンクされている場所です。

  [**アプリケーションの更新**] ダイアログボックスでは、次のプロパティが設定されます。このダイアログボックスは、[**発行**] ページからアクセスします。

- `UpdateEnabled`アプリケーションが更新プログラムを確認する必要があるかどうかを示します。

- `UpdateMode`フォアグラウンド更新またはバックグラウンド更新のいずれかを指定します。

- `UpdateInterval`アプリケーションが更新プログラムを確認する頻度を指定します。

- `UpdateIntervalUnits``UpdateInterval`値が時間単位、日単位、または週単位のどちらであるかを指定します。

- `UpdateUrl`(表示されません) は、アプリケーションが更新プログラムを受信する場所です。 この値が指定されている場合は、アプリケーションマニフェストに挿入されます。

- [発行**オプション**] ダイアログボックスでは、次のプロパティが設定されます。このダイアログボックスは、[**発行**] ページからアクセスします。

- `PublisherName`アプリケーションのインストール時または実行時に表示されるプロンプトに表示される発行元の名前を指定します。 インストールされているアプリケーションの場合は、[**スタート**] メニューのフォルダー名を指定するためにも使用されます。

- `ProductName`アプリケーションのインストール時または実行時に表示されるプロンプトに表示される製品の名前を指定します。 アプリケーションがインストールされている場合は、[**スタート**] メニューのショートカット名を指定するためにも使用されます。

- [**必須コンポーネント**] ダイアログボックスでは、次のプロパティが設定されます。このダイアログボックスは、[**発行**] ページからアクセスします。

- `BootstrapperEnabled`*setup.exe* ブートストラップを生成するかどうかを決定します。

- `IsWebBootstrapper`*setup.exe* ブートストラップが Web またはディスクベースモードのどちらで動作するかを決定します。

## <a name="installurl-supporturl-publishurl-and-updateurl"></a>InstallURL、SupportUrl、PublishURL、UpdateURL
 次の表は、ClickOnce 配置の4つの URL オプションを示しています。

|URL オプション|説明|
|----------------|-----------------|
|`PublishURL`|ClickOnce アプリケーションを Web サイトに発行する場合に必要です。|
|`InstallURL`|省略可能です。 インストールサイトがと異なる場合は、 `PublishURL`この URL オプションを設定します。 たとえば、を FTP パス`PublishURL`に設定し、 `InstallURL`を Web URL に設定できます。|
|`SupportURL`|任意。 サポートサイトがと異なる場合は、 `PublishURL`この URL オプションを設定します。 たとえば、を会社のカスタマーサポート`SupportURL` Web サイトに設定できます。|
|`UpdateURL`|省略可能です。 更新プログラムの場所がと異なる場合は、 `InstallURL`この URL オプションを設定します。 たとえば、を FTP パス`PublishURL`に設定し、 `UpdateURL`を Web URL に設定できます。|

## <a name="see-also"></a>関連項目
- <xref:Microsoft.Build.Tasks.GenerateBootstrapper>
- <xref:Microsoft.Build.Tasks.GenerateApplicationManifest>
- <xref:Microsoft.Build.Tasks.GenerateDeploymentManifest>
- [ClickOnce のセキュリティと配置](../deployment/clickonce-security-and-deployment.md)
- [チュートリアル: ClickOnce アプリケーションを手動で配置する](../deployment/walkthrough-manually-deploying-a-clickonce-application.md)
