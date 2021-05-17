---
title: ClickOnce を使用してマルチ ターゲット アプリを配置する
description: ClickOnce 配置テクノロジを使用して、複数バージョンの .NET Framework をターゲットとするアプリケーションを配置する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
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
manager: jmartens
ms.workload:
- dotnet
ms.openlocfilehash: c87ed73d2c3a26ecc4522c6497ac71e33e46a6c3
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99889123"
---
# <a name="how-to-use-clickonce-to-deploy-applications-that-can-run-on-multiple-versions-of-the-net-framework"></a>方法: ClickOnce を使用して、複数のバージョンの .NET Framework で実行できるアプリケーションを配置する
ClickOnce 配置テクノロジを使用して、複数バージョンの .NET Framework をターゲットとするアプリケーションを配置することができます。 そのためには、アプリケーション マニフェストと配置マニフェストを生成して更新する必要があります。

> [!NOTE]
> 複数バージョンの .NET Framework をターゲットとするようにアプリケーションを変更する前に、アプリケーションが複数のバージョンの .NET Framework で実行されることを確認する必要があります。 .NET Framework 4 と、.NET Framework 2.0、NET Framework 3.0、および .NET Framework 3.5 との間で、共通言語ランタイムのバージョンが異なっています。

 このプロセスでは、以下の手順が必要となります。

1. アプリケーション マニフェストと配置マニフェストを生成します。

2. .NET Framework の複数のバージョンを一覧で示すように配置マニフェストを変更します。

3. .NET Framework の互換性のあるランタイム バージョンを一覧で示すように *app.config* ファイルを変更します。

4. 依存アセンブリを .NET Framework アセンブリとしてマークするようにアプリケーション マニフェストを変更します。

5. アプリケーション マニフェストに署名します。

6. 配置マニフェストを更新し、署名します。

### <a name="to-generate-the-application-and-deployment-manifests"></a>アプリケーション マニフェストと配置マニフェストを生成するには

- 発行ウィザードまたはプロジェクト デザイナーの [発行] ページを使用して、アプリケーションを発行し、アプリケーション マニフェストと配置マニフェストのファイルを生成します。 詳細については、「[方法: 発行ウィザードを使用して ClickOnce アプリケーションを発行する](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md)」または「[[発行] ページ (プロジェクト デザイナー)](../ide/reference/publish-page-project-designer.md)」を参照してください。

### <a name="to-change-the-deployment-manifest-to-list-the-multiple-net-framework-versions"></a>.NET Framework の複数のバージョンを一覧で示すように配置マニフェストを変更するには

1. Visual Studio の XML エディターを使用して、配置ディレクトリで配置マニフェストを開きます。 配置マニフェストのファイル名拡張子は *.application* です。

2. `<compatibleFrameworks xmlns="urn:schemas-microsoft-com:clickonce.v2">` 要素と `</compatibleFrameworks>` 要素の間の XML コードを、アプリケーションでサポートされている .NET Framework バージョンが一覧に示されている XML に置き換えます。

     次の表は、.NET Framework の使用可能なバージョンの一部と、配置マニフェストに追加できる、対応する XML を示しています。

    |.NET Framework のバージョン|XML|
    |----------------------------|---------|
    |4 Client|\<framework targetVersion="4.0" profile="Client" supportedRuntime="4.0.30319" />|
    |4 Full|\<framework targetVersion="4.0" profile="Full" supportedRuntime="4.0.30319" />|
    |3.5 Client|\<framework targetVersion="3.5" profile="Client" supportedRuntime="2.0.50727" />|
    |3.5 Full|\<framework targetVersion="3.5" profile="Full" supportedRuntime="2.0.50727" />|
    |3.0|\<framework targetVersion="3.0" supportedRuntime="2.0.50727" />|

### <a name="to-change-the-appconfig-file-to-list-the-compatible-net-framework-runtime-versions"></a>.NET Framework の互換性のあるランタイム バージョンを一覧で示すように app.config ファイルを変更するには

1. ソリューション エクスプローラーで、Visual Studio の XML エディターを使用して *app.config* ファイルを開きます。

2. `<startup>` 要素と `</startup>` 要素の間の XML コードを、アプリケーションでサポートされている .NET Framework ランタイムが一覧に示されている XML に置き換えます (または追加します)。

     次の表は、.NET Framework の使用可能なバージョンの一部と、配置マニフェストに追加できる、対応する XML を示しています。

    |.NET Framework ランタイム バージョン|XML|
    |------------------------------------|---------|
    |4 Client|\<supportedRuntime version="v4.0.30319" sku=".NETFramework,Version=v4.0,Profile=Client" />|
    |4 Full|\<supportedRuntime version="v4.0.30319" sku=".NETFramework,Version=v4.0" />|
    |3.5 Full|\<supportedRuntime version="v2.0.50727"/>|
    |3.5 Client|\<supportedRuntime version="v2.0.50727" sku="Client"/>|

### <a name="to-change-the-application-manifest-to-mark-dependent-assemblies-as-net-framework-assemblies"></a>依存アセンブリを .NET Framework アセンブリとしてマークするようにアプリケーション マニフェストを変更するには

1. Visual Studio の XML エディターを使用して、配置ディレクトリでアプリケーション マニフェストを開きます。 配置マニフェストのファイル名拡張子は *.manifest* です。

2. Sentinel アセンブリ (`System.Core`、`WindowsBase`、`Sentinel.v3.5Client`、`System.Data.Entity`) の依存関係 XML に `group="framework"` を追加します。 たとえば、XML は次のようになっている必要があります。

   ```xml
   <dependentAssembly dependencyType="preRequisite" allowDelayedBinding="true" group="framework">
   ```

3. Microsoft.Windows.CommonLanguageRuntime の `<assemblyIdentity>` 要素のバージョン番号を、最小限の共通要件である .NET Framework のバージョン番号に更新します。 たとえば、アプリケーションが .NET Framework 3.5 および 4 をターゲットとしている場合は、バージョン番号として 2.0.50727.0 を使用します。XML は次のようになっている必要があります。

   ```xml
   <dependency>
     <dependentAssembly dependencyType="preRequisite" allowDelayedBinding="true">
       <assemblyIdentity name="Microsoft.Windows.CommonLanguageRuntime" version="2.0.50727.0" />
     </dependentAssembly>
   </dependency>
   ```

### <a name="to-update-and-re-sign-the-application-and-deployment-manifests"></a>アプリケーション マニフェストと配置マニフェストを更新して再署名するには

- アプリケーション マニフェストと配置マニフェストを更新して再署名します。 詳細については、「[方法: アプリケーション マニフェストおよび配置マニフェストに再署名](../deployment/how-to-re-sign-application-and-deployment-manifests.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [ClickOnce アプリケーションの発行](../deployment/publishing-clickonce-applications.md)
- [\<compatibleFrameworks> 要素](../deployment/compatibleframeworks-element-clickonce-deployment.md)
- [\<dependency> 要素](../deployment/dependency-element-clickonce-application.md)
- [ClickOnce 配置マニフェスト](../deployment/clickonce-deployment-manifest.md)
- [構成ファイル スキーマ](/dotnet/framework/configure-apps/file-schema/index)
