---
title: ClickOnce 配置での前提条件に対するサポート URL
description: ClickOnce アプリケーションが実行するための前提条件の ClickOnce 配置によるテスト方法と、足りない前提条件の配置による処理方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- ClickOnce deployment, prerequisites
- ClickOnce deployment, URLs
ms.assetid: 590742c3-a286-4160-aa75-7a441bb2207b
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 585ea1a558b91ac733670ad94a9a3e0be33f1348
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99876317"
---
# <a name="how-to-specify-a-support-url-for-individual-prerequisites-in-a-clickonce-deployment"></a>方法: ClickOnce 配置で個々の必要条件にサポート URL を指定する
[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションが実行するためにクライアント コンピューターで利用できる必要があるいくつかの前提条件を、[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 配置でテストできます。 これらの依存関係には、最低限必要な .NET Framework のバージョン、オペレーティング システムのバージョン、およびグローバル アセンブリ キャッシュ (GAC) にプレインストールされている必要があるすべてのアセンブリが含まれます。 ただし、これらの前提条件自体を [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] でインストールすることはできません。前提条件が見つからない場合は、単にインストールが停止され、インストールが失敗した理由を説明するダイアログ ボックスが表示されます。

 前提条件をインストールするには 2 つの方法があります。 ブートストラッパー アプリケーションを使用してインストールできます。 または、個々の前提条件のサポート URL を指定することもできます。これは、前提条件が見つからない場合に、ダイアログ ボックスでユーザーに表示されます。 その URL によって参照されるページには、必要な前提条件をインストールするための説明へのリンクを含めることができます。 アプリケーションで個々の前提条件のサポート URL が指定されていない場合、配置マニフェストでアプリケーション全体に対するサポート URL が指定されていれば、[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] によってそれが表示されます。

 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]、*Mage.exe*、*MageUI.exe* はすべて、[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 配置を生成するために使用できますが、これらのどのツールでも、個々の前提条件のサポート URL を直接指定することはできません。 このドキュメントでは、配置のアプリケーション マニフェストと配置マニフェストを変更して、これらのサポート URL を含める方法について説明します。

### <a name="specify-a-support-url-for-an-individual-prerequisite"></a>個々の前提条件のサポート URL を指定する

1. [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションのアプリケーション マニフェスト ( *.manifest* ファイル) を、テキスト エディターで開きます。

2. オペレーティング システムに関する前提条件の場合、`supportUrl` 属性を `dependentOS` 要素に追加します。

   ```xml
    <dependency>
       <dependentOS supportUrl="http://www.adatum.com/MyApplication/wrongOSFound.htm">
         <osVersionInfo>
           <os majorVersion="5" minorVersion="1" buildNumber="2600" servicePackMajor="0" servicePackMinor="0" />
         </osVersionInfo>
       </dependentOS>
     </dependency>
   ```

3. 特定のバージョンの共通言語ランタイムに関する前提条件の場合は、共通言語ランタイムの依存関係を指定する `dependentAssembly` エントリに `supportUrl` 属性を追加します。

   ```xml
     <dependency>
       <dependentAssembly dependencyType="preRequisite" allowDelayedBinding="true" supportUrl=" http://www.adatum.com/MyApplication/wrongClrVersionFound.htm">
         <assemblyIdentity name="Microsoft.Windows.CommonLanguageRuntime" version="4.0.30319.0" />
       </dependentAssembly>
     </dependency>
   ```

4. グローバル アセンブリ キャッシュにプレインストールする必要があるアセンブリに関する前提条件の場合は、必要なアセンブリを指定する `dependentAssembly` 要素に `supportUrl` を設定します。

   ```xml
     <dependency>
       <dependentAssembly dependencyType="preRequisite" allowDelayedBinding="true" supportUrl=" http://www.adatum.com/MyApplication/missingSampleGACAssembly.htm">
         <assemblyIdentity name="SampleGACAssembly" version="5.0.0.0" publicKeyToken="04529dfb5da245c5" processorArchitecture="msil" language="neutral" />
       </dependentAssembly>
     </dependency>
   ```

5. 省略可能。 .NET Framework 4 を対象とするアプリケーションの場合は、[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションの配置マニフェスト ( *.application* ファイル) をテキスト エディターで開きます。

6. .NET Framework 4 の前提条件の場合は、`supportUrl` 属性を `compatibleFrameworks` 要素に追加します。

   ```xml
   <compatibleFrameworks  xmlns="urn:schemas-microsoft-com:clickonce.v2" supportUrl="http://adatum.com/MyApplication/CompatibleFrameworks.htm">
     <framework targetVersion="4.0" profile="Client" supportedRuntime="4.0.30319" />
     <framework targetVersion="4.0" profile="Full" supportedRuntime="4.0.30319" />
   </compatibleFrameworks>
   ```

7. アプリケーション マニフェストを手作業で変更したら、デジタル証明書を使用してアプリケーション マニフェストに再署名してから、配置マニフェストも更新して再署名する必要があります。 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] を使用してこれらのファイルを再生成すると手作業による変更が消去されるので、このタスクを実行するには、*Mage.exe* または *MageUI.exe* SDK ツールを使用します。 Mage.exe を使用してマニフェストに再署名する方法の詳細については、「[方法: アプリケーション マニフェストおよび配置マニフェストに再署名する](../deployment/how-to-re-sign-application-and-deployment-manifests.md)」を参照してください。

## <a name="net-framework-security"></a>.NET Framework のセキュリティ
 アプリケーションが部分信頼で実行するようにマークされている場合、サポート URL はダイアログ ボックスに表示されません。

## <a name="see-also"></a>こちらもご覧ください
- [Mage.exe (マニフェストの生成および編集ツール)](/dotnet/framework/tools/mage-exe-manifest-generation-and-editing-tool)
- [チュートリアル: ClickOnce アプリケーションを手動で配置する](../deployment/walkthrough-manually-deploying-a-clickonce-application.md)
- [\<compatibleFrameworks> 要素](../deployment/compatibleframeworks-element-clickonce-deployment.md)
- [ClickOnce と Authenticode](../deployment/clickonce-and-authenticode.md)
- [アプリケーション配置の必要条件](../deployment/application-deployment-prerequisites.md)