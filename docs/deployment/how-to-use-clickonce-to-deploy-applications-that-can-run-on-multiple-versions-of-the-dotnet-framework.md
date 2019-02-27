---
title: '方法: ClickOnce を使用して、複数バージョンの .NET Framework で実行できるアプリケーションをデプロイする |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- ClickOnce applications, multiple .NET Framework versions
- ClickOnce deployment, multiple .NET Framework versions
- deploying applications [ClickOnce], multiple .NET Framework versions
ms.assetid: e0a8c330-21bc-4eb2-b936-fd0f3c3221f1
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: 154e6058689d308f35fd969438d1964b9383f653
ms.sourcegitcommit: d0425b6b7d4b99e17ca6ac0671282bc718f80910
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 02/21/2019
ms.locfileid: "56633968"
---
# <a name="how-to-use-clickonce-to-deploy-applications-that-can-run-on-multiple-versions-of-the-net-framework"></a>方法: ClickOnce を使用して、複数のバージョンの .NET Framework で実行できるアプリケーションを配置する
ClickOnce 配置テクノロジを使用して複数バージョンの .NET Framework を対象とするアプリケーションを展開することができます。 これは、生成し、アプリケーション マニフェストと配置マニフェストを更新する必要があります。

> [!NOTE]
>  複数バージョンの .NET Framework を対象とするアプリケーションを変更する前に、アプリケーションが .NET Framework の複数のバージョンで実行されることを確認する必要があります。 バージョンの共通言語ランタイムが異なる[!INCLUDE[net_v40_short](../code-quality/includes/net_v40_short_md.md)]と .NET Framework 2.0、.NET Framework 3.0、および .NET Framework 3.5。

 このプロセスでは、次の手順が必要です。

1.  アプリケーションと配置マニフェストを生成します。

2.  複数の .NET Framework バージョンを一覧表示、配置マニフェストを変更します。

3.  変更、 *app.config*ファイルが互換性のある .NET Framework ランタイムのバージョンを一覧表示します。

4.  依存アセンブリの .NET Framework アセンブリとしてマークするアプリケーション マニフェストを変更します。

5.  アプリケーション マニフェストに署名します。

6.  更新し、配置マニフェストに署名します。

### <a name="to-generate-the-application-and-deployment-manifests"></a>アプリケーションと配置マニフェストを生成するには

-   アプリケーションを発行して、アプリケーションと配置マニフェスト ファイルを生成するには、発行ウィザード、または、プロジェクト デザイナーの [発行] ページを使用します。 詳細については、次を参照してください。[方法: 発行ウィザードを使用して ClickOnce アプリケーションを発行](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md)または[発行 Page, Project Designer](../ide/reference/publish-page-project-designer.md)します。

### <a name="to-change-the-deployment-manifest-to-list-the-multiple-net-framework-versions"></a>複数の .NET Framework バージョンを一覧表示、配置マニフェストを変更するには

1.  発行ディレクトリには、Visual Studio で、XML エディターを使用して、配置マニフェストを開きます。 配置マニフェスト、 *.application*ファイル名拡張子。

2.  間の XML コードを置き換える、`<compatibleFrameworks xmlns="urn:schemas-microsoft-com:clickonce.v2">`と`</compatibleFrameworks>`アプリケーションのサポートされている .NET Framework バージョンを一覧表示する xml 要素。

     次の表では、使用可能な .NET Framework バージョンと配置マニフェストに追加できる、対応する XML の一部を示します。

    |.NET Framework のバージョン|XML|
    |----------------------------|---------|
    |4 Client|\<framework targetVersion="4.0" profile="Client" supportedRuntime="4.0.30319" />|
    |4 Full|\<framework targetVersion="4.0" profile="Full" supportedRuntime="4.0.30319" />|
    |3.5 Client|\<framework targetVersion="3.5" profile="Client" supportedRuntime="2.0.50727" />|
    |3.5 Full|\<framework targetVersion="3.5" profile="Full" supportedRuntime="2.0.50727" />|
    |3.0|\<framework targetVersion="3.0" supportedRuntime="2.0.50727" />|

### <a name="to-change-the-appconfig-file-to-list-the-compatible-net-framework-runtime-versions"></a>互換性のある .NET Framework ランタイムのバージョンを一覧表示する app.config ファイルを変更するには

1.  ソリューション エクスプ ローラーで開く、 *app.config* Visual Studio で、XML エディターを使用して、ファイル。

2.  間の XML コードを置き換えます (または追加)、`<startup>`と`</startup>`アプリケーションのサポートされている .NET Framework ランタイムの一覧を表示する xml 要素。

     次の表では、使用可能な .NET Framework バージョンと配置マニフェストに追加できる、対応する XML の一部を示します。

    |.NET framework ランタイムのバージョン|XML|
    |------------------------------------|---------|
    |4 Client|\<supportedRuntime version="v4.0.30319" sku=".NETFramework,Version=v4.0,Profile=Client" />|
    |4 Full|\<supportedRuntime version="v4.0.30319" sku=".NETFramework,Version=v4.0" />|
    |3.5 Full|\<supportedRuntime version="v2.0.50727"/>|
    |3.5 Client|\<supportedRuntime version="v2.0.50727" sku="Client"/>|

### <a name="to-change-the-application-manifest-to-mark-dependent-assemblies-as-net-framework-assemblies"></a>依存アセンブリの .NET Framework アセンブリとしてマークするアプリケーション マニフェストを変更するには

1. 発行ディレクトリには、Visual Studio で、XML エディターを使用して、アプリケーション マニフェストを開きます。 配置マニフェスト、 *.manifest*ファイル名拡張子。

2. 追加`group="framework"`sentinel アセンブリの依存関係 XML を (`System.Core`、 `WindowsBase`、 `Sentinel.v3.5Client`、および`System.Data.Entity`)。 たとえば、XML は次のようになります。

   ```xml
   <dependentAssembly dependencyType="preRequisite" allowDelayedBinding="true" group="framework">
   ```

3. 更新プログラムのバージョン番号、`<assemblyIdentity>`最小公分母をある .NET Framework のバージョン番号を Microsoft.Windows.CommonLanguageRuntime の要素。 たとえば、アプリケーションが .NET Framework 3.5 を対象とし、 [!INCLUDE[net_v40_short](../code-quality/includes/net_v40_short_md.md)]、バージョン番号を使用して、[2.0.50727.0] と、XML、次のようになります。

   ```xml
   <dependency>
     <dependentAssembly dependencyType="preRequisite" allowDelayedBinding="true">
       <assemblyIdentity name="Microsoft.Windows.CommonLanguageRuntime" version="2.0.50727.0" />
     </dependentAssembly>
   </dependency>
   ```

### <a name="to-update-and-re-sign-the-application-and-deployment-manifests"></a>マニフェストを更新して、アプリケーションおよび配置に再署名

-   更新し、アプリケーション マニフェストと配置マニフェストに再署名します。 詳細については、「[方法: アプリケーション マニフェストおよび配置マニフェストに再署名](../deployment/how-to-re-sign-application-and-deployment-manifests.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [ClickOnce アプリケーションの発行](../deployment/publishing-clickonce-applications.md)
- [\<compatibleFrameworks > 要素](../deployment/compatibleframeworks-element-clickonce-deployment.md)
- [\<依存関係 > 要素](../deployment/dependency-element-clickonce-application.md)
- [ClickOnce 配置マニフェスト](../deployment/clickonce-deployment-manifest.md)
- [構成ファイル スキーマ](/dotnet/framework/configure-apps/file-schema/index)