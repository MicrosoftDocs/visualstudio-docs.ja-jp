---
title: ClickOnce アプリケーションのコマンド ラインからのビルド | Microsoft Docs
description: コマンド ラインから Visual Studio プロジェクトをビルドする方法について説明します。この方法では、自動化されたプロセスを使用してビルドを再現できます。
ms.custom: SEO-VS-2020
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
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 13b057f0a688c3a1ae855215ac226a4d31993ea1
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99895155"
---
# <a name="build-clickonce-applications-from-the-command-line"></a>ClickOnce アプリケーションのコマンド ラインからのビルド

[!INCLUDE[vs_current_short](../code-quality/includes/vs_current_short_md.md)] では、統合開発環境 (IDE) で作成されたプロジェクトであってもコマンド ラインからビルドできます。 実際には、.NET Framework のみがインストールされている別のコンピューターで、[!INCLUDE[vs_current_short](../code-quality/includes/vs_current_short_md.md)] を使用して作成されたプロジェクトをリビルドできます。 これにより、たとえば中央のビルド ラボで自動化されたプロセスを使用して、または、プロジェクト自体をビルドする範囲を超えた高度なスクリプト手法を使用して、ビルドを再現できます。

## <a name="use-msbuild-to-reproduce-net-framework-clickonce-application-deployments"></a>MSBuild を使用して .NET Framework ClickOnce アプリケーションの配置を再現する

 コマンド ラインで msbuild /target:publish を呼び出すと、MSBuild システムに、プロジェクトをビルドし、発行フォルダー内に [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションを作成するよう指示されます。 これは、IDE で **[発行]** コマンドを選択することと同等です。

 このコマンドでは、*msbuild.exe* が実行されます。これは、Visual Studio のコマンドプロンプト環境のパスにあります。

 "ターゲット" は、コマンドをどのように処理するかについての、MSBuild に対するインジケーターです。 主要なターゲットは、"ビルド" ターゲットと "発行" ターゲットです。 ビルド ターゲットは、IDE でビルド コマンドを選択する (または F5 キーを押す) ことに相当します。 プロジェクトをビルドするだけの場合は、「`msbuild`」と入力すると、それを実現できます。 このコマンドが機能するのは、ビルド ターゲットが、[!INCLUDE[vs_current_short](../code-quality/includes/vs_current_short_md.md)] によって生成されるすべてのプロジェクトの既定のターゲットであるためです。 これは、ビルド ターゲットを明示的に指定する必要がないことを意味します。 したがって、「`msbuild`」と入力することは、「`msbuild /target:build`」と入力するのと同じ操作です。

 `/target:publish` コマンドでは、MSBuild に、発行ターゲットを呼び出すように指示します。 発行ターゲットは、ビルド ターゲットに応じて異なります。 これは、発行操作がビルド操作のスーパーセットであることを意味します。 たとえば、Visual Basic または C# のソース ファイルのいずれかに変更を加えた場合、対応するアセンブリは発行操作によって自動的にリビルドされます。

 Mage.exe コマンドライン ツールを使用して [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] マニフェストを作成する完全な [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 配置を生成することについては、「[チュートリアル: ClickOnce アプリケーションを手動で配置する](../deployment/walkthrough-manually-deploying-a-clickonce-application.md)」を参照してください。

## <a name="create-and-build-a-basic-clickonce-application-with-msbuild"></a>MSBuild で基本的な ClickOnce アプリケーションを作成してビルドする

### <a name="to-create-and-publish-a-clickonce-project"></a>ClickOnce プロジェクトを作成して発行するには

1. Visual Studio を起動し、新しいプロジェクトを作成します。

    **[Windows デスクトップ アプリケーション]** プロジェクト テンプレートを選択し、プロジェクトに `CmdLineDemo` という名前を付けます。

1. **[ビルド]** メニューの **[発行]** コマンドをクリックします。

    この手順により、[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションの配置を生成するようにプロジェクトが適切に構成されます。

    発行ウィザードが表示されます。

1. 発行ウィザードで、 **[完了]** をクリックします。

    Visual Studio によって、*Publish.htm* という名前の既定の Web ページが生成され、表示されます。

1. プロジェクトを保存し、それが格納されるフォルダーの場所をメモします。

   上記の手順では、初めて発行された [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] プロジェクトを作成しています。 これで、IDE の外部でビルドを再現することができます。

#### <a name="to-reproduce-the-build-from-the-command-line"></a>コマンド ラインからビルドを再現するには

1. [!INCLUDE[vs_current_short](../code-quality/includes/vs_current_short_md.md)] を終了します。

2. Windows の **[スタート]** メニューから、 **[すべてのプログラム]** 、 **[Microsoft Visual Studio]** 、 **[Visual Studio Tools]** 、 **[Visual Studio コマンド プロンプト]** の順にクリックします。 これで、現在のユーザーのルート フォルダーでコマンド プロンプトが開きます。

3. **[Visual Studio コマンド プロンプト]** で、現在のディレクトリを、上で作成したばかりのプロジェクトの場所に変更します。 たとえば、「 `chdir My Documents\Visual Studio\Projects\CmdLineDemo`」と入力します。

4. 「[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] プロジェクトを作成して発行するには」で作成した既存のファイルを削除するには、「`rmdir /s publish`」と入力します。

    この手順は省略可能ですが、これにより、新しいファイルがすべてコマンドラインのビルドによって生成されるようになります。

5. 「`msbuild /target:publish`.

   上記の手順で、プロジェクトの **Publish** という名前のサブフォルダーに [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションの完全な配置が生成されます。 *CmdLineDemo.application* は [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 配置マニフェストです。 *CmdLineDemo_1.0.0.0* フォルダーには、*CmdLineDemo.exe* ファイルと、[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーション マニフェストの *CmdLineDemo.exe.manifest* ファイルが含まれています。 *Setup.exe* はブートストラップで、既定では .NET Framework をインストールするように構成されています。 The DotNetFX フォルダーには、.NET Framework の再頒布可能パッケージが含まれています。 これは、Web 経由で、または UNC や CD/DVD を介してアプリケーションを配置するために必要な全ファイルのセットです。

> [!NOTE]
> MSBuild システムでは、**PublishDir** オプションを使用して出力の場所を指定します。たとえば、`msbuild /t:publish /p:PublishDir="<specific location>"` と指定します。

::: moniker range=">=vs-2019"

## <a name="build-net-clickonce-applications-from-the-command-line"></a>.NET ClickOnce アプリケーションをコマンド ラインからビルドする

コマンド ラインからの .NET ClickOnce アプリケーションのビルドでは同様の操作を行いますが、MSBuild コマンド ラインで、発行プロファイルに追加のプロパティを指定する必要がある点が異なります。 発行プロファイルを作成する最も簡単な方法は、Visual Studio を使用することです。  詳細については、[ClickOnce を使用して .NET Windows アプリケーションを配置する](quickstart-deploy-using-clickonce-folder.md)ことに関するページを参照してください。

発行プロファイルを作成したら、msbuild コマンド ラインで、pubxml ファイルをプロパティとして指定できます。 次に例を示します。

```cmd
    msbuild /t:publish /p:PublishProfile=<pubxml file> /p:PublishDir="<specific location>"
```
::: moniker-end

## <a name="publish-properties"></a>[発行] プロパティ

 上記の手順でアプリケーションを発行すると、発行ウィザード、または .NET Core 3.1 以降のプロジェクトの発行プロファイル ファイルによって、以下のプロパティがプロジェクト ファイルに挿入されます。 これらのプロパティは、[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションがどのように生成されるかに直接影響を及ぼします。

 *CmdLineDemo.vbproj* / *CmdLineDemo.csproj* 内は次のようになっています。

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

 .NET Framework プロジェクトでは、プロジェクト ファイル自体を変更することなく、コマンド ラインでこれらのどのプロパティもオーバーライドすることができます。 たとえば、次のように指定すると、ブートストラップを使用せずに [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションの配置がビルドされます。

```cmd
msbuild /target:publish /property:BootstrapperEnabled=false
 ```

::: moniker range=">=vs-2019"
.NET Core 3.1 以降のプロジェクトでは、これらの設定は pubxml ファイルで提供されます。

 発行プロパティは [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] で、**プロジェクト デザイナー** の **[発行]** 、 **[セキュリティ]** 、 **[署名]** の各プロパティ ページから制御されます。 以下では、発行プロパティの説明に加えて、それぞれが、アプリケーション デザイナーのさまざまなプロパティ ページでどのように設定されるかを示します。

> [!NOTE]
> .NET Windows デスクトップ プロジェクトの場合、これらの設定は発行ウィザードに含まれるようになりました
::: moniker-end

- `AssemblyOriginatorKeyFile` では、[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーション マニフェストに署名するために使用するキー ファイルを指定します。 この同じキーは、アセンブリに厳密な名前を割り当てるために使用することもできます。 このプロパティは、**プロジェクト デザイナー** の **[署名]** ページで設定されます。
::: moniker range=">=vs-2019"
.NET Windows アプリケーションの場合、この設定はプロジェクト ファイルに残されています
::: moniker-end

  以下のプロパティは、 **[セキュリティ]** ページで設定されます。

- **[ClickOnce セキュリティ設定を有効にする]** では、[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] マニフェストを生成するかどうかを指定します。 プロジェクトが最初に作成されるときには、[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] マニフェストの生成は既定で無効になっています。 初めて発行するときに、ウィザードによって自動的にこのフラグがオンにされます。

- **TargetZone** では、[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーション マニフェストに出力する信頼のレベルを指定します。 指定できる値は、"Internet"、"LocalIntranet"、"Custom" です。 Internet や LocalIntranet を指定すると、既定のアクセス許可のセットが [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーション マニフェストに出力されます。 LocalIntranet が既定値で、これは基本的に完全な信頼を意味します。 Custom は、基本の *app.manifest* ファイルで明示的に指定されているアクセス許可のみが、[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーション マニフェストに出力されることを指定します。 *app.manifest* ファイルは、信頼情報の定義のみが含まれる部分的なマニフェスト ファイルです。 これは非表示のファイルで、 **[セキュリティ]** ページでアクセス許可を構成するときに、プロジェクトに自動的に追加されます。
-
::: moniker range=">=vs-2019"
> [!NOTE]
> .NET Core 3.1 以降、Windows デスクトップ プロジェクトでは、これらのセキュリティ設定はサポートされていません。
::: moniker-end

  以下のプロパティは、 **[発行]** ページで設定されます。

- `PublishUrl` は、IDE 内でアプリケーションの公開先となる場所です。 プロパティとして `InstallUrl` または `UpdateUrl` のどちらも指定されていない場合は、これが [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーション マニフェストに挿入されます。

- `ApplicationVersion` では、[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションのバージョンを指定します。 これは 4 桁のバージョン番号です。 最後の数字が "*" である場合は、`ApplicationRevision` が、ビルド時にマニフェストに挿入される値の代わりになります。

- `ApplicationRevision` では、リビジョンを指定します。 これは、IDE での発行のたびに増える整数です。 これは、コマンド ラインで実行されるビルドについては自動的に増加されないことに注意してください。

- `Install` では、そのアプリケーションがインストールされるアプリケーションであるか、Web から実行されるアプリケーションであるかを指定します。

- `InstallUrl` (表示されていません) は、ユーザーによるアプリケーションのインストール元となる場所です。 指定されている場合、この値は `IsWebBootstrapper` プロパティが有効になっていると *setup.exe* ブートストラップに書き込まれます。 `UpdateUrl` が指定されていない場合、これはアプリケーション マニフェストにも挿入され ます。

- `SupportUrl` (表示されていません) は、インストールされたアプリケーションの **[プログラムの追加と削除]** ダイアログ ボックス内にリンクが表示される場所です。

  以下のプロパティは、 **[発行]** ページからアクセスする **[アプリケーションの更新]** ダイアログ ボックスで設定されます。

- `UpdateEnabled` では、アプリケーションで更新プログラムを確認する必要があるかどうかを指定します。

- `UpdateMode` では、Foreground 更新または Background 更新のいずれかを指定します。
::: moniker range=">=vs-2019"
   .NET Core 3.1 以降のプロジェクトでは、Background はサポートされていません。  
::: moniker-end
- `UpdateInterval` では、アプリケーションが更新プログラムを確認する必要がある頻度を指定します。
::: moniker range=">=vs-2019"
   .NET Core 3.1 以降、この設定はサポートされていません。
::: moniker-end

- `UpdateIntervalUnits` では、`UpdateInterval` 値の単位が時間、日、週のどれであるかを指定します。
::: moniker range=">=vs-2019"
   .NET Core 3.1 以降、この設定はサポートされていません。
::: moniker-end

- `UpdateUrl` (表示されていません) は、アプリケーションでの更新プログラムの受信元となる場所です。 指定されている場合は、この値がアプリケーション マニフェストに挿入されます。

  以下のプロパティは、 **[発行]** ページからアクセスする **[発行オプション]** ダイアログ ボックスで設定されます。

- `PublisherName` では、アプリケーションのインストール時または実行時に表示されるプロンプトに示される発行元の名前を指定します。 インストールされるアプリケーションの場合、 **[スタート]** メニューのフォルダー名を指定するためにも使用されます。

- `ProductName` では、アプリケーションのインストール時または実行時に表示されるプロンプトに表示される製品の名前を指定します。 インストールされるアプリケーションの場合、 **[スタート]** メニューのショートカット名を指定するためにも使用されます。

  以下のプロパティは、 **[発行]** ページからアクセスする **[前提条件]** ダイアログ ボックスで設定されます。

- `BootstrapperEnabled` では、*setup.exe* ブートストラップを生成するかどうかを指定します。

- `IsWebBootstrapper` では、*setup.exe* ブートストラップが Web 上またはディスク ベース モードのどちらで動作するかを指定します。

## <a name="installurl-supporturl-publishurl-and-updateurl"></a>InstallURL、SupportUrl、PublishURL、UpdateURL

 次の表に、ClickOnce 配置の 4 つの URL オプションを示します。

|URL オプション|説明|
|----------------|-----------------|
|`PublishURL`|ClickOnce アプリケーションを Web サイトに発行しようとしている場合に必要です。|
|`InstallURL`|省略可能。 インストール場所が `PublishURL` とは異なる場合は、この URL オプションを設定します。 たとえば、`PublishURL` を FTP パスに設定し、`InstallURL` を Web URL に設定できます。|
|`SupportURL`|省略可能。 サポート サイトが `PublishURL` とは異なる場合は、この URL オプションを設定します。 たとえば、`SupportURL` を、会社のカスタマー サポート Web サイトに設定できます。|
|`UpdateURL`|省略可能。 更新プログラムの場所が `InstallURL` とは異なる場合は、この URL オプションを設定します。 たとえば、`PublishURL` を FTP パスに設定し、`UpdateURL` を Web URL に設定できます。|

## <a name="see-also"></a>関連項目

- <xref:Microsoft.Build.Tasks.GenerateBootstrapper>
- <xref:Microsoft.Build.Tasks.GenerateApplicationManifest>
- <xref:Microsoft.Build.Tasks.GenerateDeploymentManifest>
- [ClickOnce のセキュリティと配置](../deployment/clickonce-security-and-deployment.md)
- [チュートリアル: ClickOnce アプリケーションを手動で配置する](../deployment/walkthrough-manually-deploying-a-clickonce-application.md)
