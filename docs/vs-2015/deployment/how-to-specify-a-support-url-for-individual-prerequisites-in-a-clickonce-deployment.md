---
title: '方法: サポート URL を指定の ClickOnce 配置で個々 の前提条件 |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-deployment
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- ClickOnce deployment, prerequisites
- ClickOnce deployment, URLs
ms.assetid: 590742c3-a286-4160-aa75-7a441bb2207b
caps.latest.revision: 12
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 1907b619bcc616c73d9b9e37af30722c02bf100e
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/15/2019
ms.locfileid: "65679966"
---
# <a name="how-to-specify-a-support-url-for-individual-prerequisites-in-a-clickonce-deployment"></a>方法: ClickOnce 配置で個々 の前提条件のサポートの URL を指定します。
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

A[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]数のクライアント コンピューターで使用する必要がある前提条件の展開をテストできます、[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]アプリケーションを実行します。 必要な最小バージョンが含まれます、[!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)]のバージョン、オペレーティング システムとすべてのアセンブリをグローバル アセンブリ キャッシュ (GAC) にプレインストールする必要があります。 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]、ただし、インストールできませんこれらの前提条件のいずれか。前提条件が存在しない場合、インストールを中止し、インストールが失敗した理由を説明するダイアログ ボックスが表示されます。  
  
 前提条件をインストールするための 2 つの方法はあります。 ブートス トラップ アプリケーションを使用してインストールすることができます。 また、前提条件が存在しない場合、ダイアログ ボックスでユーザーに表示される個別の前提条件のサポート URL を指定できます。 この URL で参照されているページは、必須の前提条件をインストールするための手順へのリンクを含めることができます。 アプリケーションが、個別の前提条件に関するサポート URL を指定しない場合[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]定義されている場合、全体として、アプリケーションの配置マニフェストで指定されたサポート URL を表示します。  
  
 中に[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]、Mage.exe および MageUI.exe すべてできますを生成する[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]展開では、これらのツールを直接サポート個々 の必要条件のサポート URL を指定します。 このドキュメントは、実際のデプロイを変更する方法を説明しますアプリケーション マニフェストと配置マニフェストに含まれる Url をサポートします。  
  
### <a name="specifying-a-support-url-for-an-individual-prerequisite"></a>個々 の前提条件に関するサポート URL を指定します。  
  
1. アプリケーション マニフェスト (.manifest ファイル) を開き、[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]テキスト エディターでアプリケーション。  
  
2. オペレーティング システムの前提条件を追加、`supportUrl`属性を`dependentOS`要素。  
  
    ```  
     <dependency>  
        <dependentOS supportUrl="http://www.adatum.com/MyApplication/wrongOSFound.htm">  
          <osVersionInfo>  
            <os majorVersion="5" minorVersion="1" buildNumber="2600" servicePackMajor="0" servicePackMinor="0" />  
          </osVersionInfo>  
        </dependentOS>  
      </dependency>  
    ```  
  
3. 共通言語ランタイムの特定のバージョンの前提条件を追加、`supportUrl`属性を`dependentAssembly`共通言語ランタイムの依存関係を示すエントリ。  
  
    ```  
      <dependency>  
        <dependentAssembly dependencyType="preRequisite" allowDelayedBinding="true" supportUrl=" http://www.adatum.com/MyApplication/wrongClrVersionFound.htm">  
          <assemblyIdentity name="Microsoft.Windows.CommonLanguageRuntime" version="4.0.30319.0" />  
        </dependentAssembly>  
      </dependency>  
    ```  
  
4. アセンブリをグローバル アセンブリ キャッシュにプレインストールする必要がありますの前提条件、設定、`supportUrl`の`dependentAssembly`必要なアセンブリを指定する要素。  
  
    ```  
      <dependency>  
        <dependentAssembly dependencyType="preRequisite" allowDelayedBinding="true" supportUrl=" http://www.adatum.com/MyApplication/missingSampleGACAssembly.htm">  
          <assemblyIdentity name="SampleGACAssembly" version="5.0.0.0" publicKeyToken="04529dfb5da245c5" processorArchitecture="msil" language="neutral" />  
        </dependentAssembly>  
      </dependency>  
    ```  
  
5. 任意。 .NET Framework 4 を対象とするアプリケーションの配置マニフェスト (.application ファイル) を開いて、[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]テキスト エディターでアプリケーション。  
  
6. .NET Framework 4 の前提条件では、追加、`supportUrl`属性を`compatibleFrameworks`要素。  
  
    ```  
    <compatibleFrameworks  xmlns="urn:schemas-microsoft-com:clickonce.v2" supportUrl="http://adatum.com/MyApplication/CompatibleFrameworks.htm">  
      <framework targetVersion="4.0" profile="Client" supportedRuntime="4.0.30319" />  
      <framework targetVersion="4.0" profile="Full" supportedRuntime="4.0.30319" />  
    </compatibleFrameworks>  
    ```  
  
7. アプリケーション マニフェストを手動で変更した後、デジタル証明書を使用してアプリケーション マニフェストに再署名更新にも、配置マニフェストに再署名をする必要があります。 Mage.exe を使用する必要がありますまたは MageUI.exe SDK ツールを使用してこれらのファイルを再生成すると、このタスクを実行する[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]手動で変更を消去します。 Mage.exe を使用してマニフェストに再署名する詳細については、次を参照してください。[方法。アプリケーション マニフェストおよび配置マニフェストに再署名](../deployment/how-to-re-sign-application-and-deployment-manifests.md)します。  
  
## <a name="net-framework-security"></a>.NET Framework セキュリティ  
 サポート URL は、部分信頼で実行するアプリケーションがマークされている場合、ダイアログ ボックスでは表示されません。  
  
## <a name="see-also"></a>関連項目  
 [Mage.exe (マニフェストの生成および編集ツール)](https://msdn.microsoft.com/library/77dfe576-2962-407e-af13-82255df725a1)   
 [チュートリアル: ClickOnce アプリケーションを手動で展開します。](../deployment/walkthrough-manually-deploying-a-clickonce-application.md)   
 [\<compatibleFrameworks > 要素](../deployment/compatibleframeworks-element-clickonce-deployment.md)   
 [ClickOnce と Authenticode](../deployment/clickonce-and-authenticode.md)   
 [アプリケーション配置の必要条件](../deployment/application-deployment-prerequisites.md)
