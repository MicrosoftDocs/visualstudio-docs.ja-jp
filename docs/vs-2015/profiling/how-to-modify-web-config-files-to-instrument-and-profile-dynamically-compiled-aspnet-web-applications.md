---
title: '方法: Web.config ファイルを変更して、動的にコンパイルされた ASP.NET Web アプリケーションをインストルメント化およびプロファイルする | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: a92e5692-2183-4ae3-9431-b067c6a7aab4
caps.latest.revision: 18
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 8c5cfc94bef15e34deaec9d07a4b66021cb4fc39
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/12/2018
ms.locfileid: "49176307"
---
# <a name="how-to-modify-webconfig-files-to-instrument-and-profile-dynamically-compiled-aspnet-web-applications"></a>方法: Web.config ファイルを変更して、動的にコンパイルされた ASP.NET Web アプリケーションをインストルメント化およびプロファイルする
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] プロファイリング ツールのインストルメンテーション方式を使用すると、動的にコンパイルされた [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] Web アプリケーションから、詳しいタイミング データ、.NET のメモリの割り当てデータ、.NET オブジェクトの有効期間に関するデータを収集できます。  
  
 このトピックでは、web.config 構成ファイルを変更して [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] Web アプリケーションのインストルメント化とプロファイルを有効にする方法について説明します。  
  
> [!NOTE]
>  サンプリング プロファイル方式を使用する場合や、プリコンパイルされた [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] モジュールをインストルメント化する場合は、web.config ファイルを変更する必要はありません。  
  
 web.config ファイルのルートは、**configuration** 要素です。 動的にコンパイルされた [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] Web アプリケーションをインストルメント化およびプロファイルするには、次の要素を追加するか変更する必要があります。  
  
-   プロファイリングを制御する Microsoft.VisualStudio.Enterprise.ASPNetHelper アセンブリを識別する **configuration/runtime/assemblyBinding/dependentAssembly** 要素。 **dependentAssembly** 要素には、2 つの子要素、**assemblyIdentity** と **codeBase** が含まれます。  
  
-   ターゲット アセンブリに対するプロファイラーの処理後のコンパイル手順を指定する **configuration/system.web/compilation** 要素。  
  
-   プロファイリング ツールの場所を識別する 2 つの **add** 要素が **configuration/appSettings** セクションに追加されます。  
  
 アプリケーションの構成を復元するために使用できるように、変更前の web.config ファイルのコピーを作成することをお勧めします。  
  
### <a name="to-add-the-aspnethelper-assembly-as-a-configurationruntimeassemblybindingdependentassembly-element"></a>ASPNetHelper アセンブリを configuration/runtime/assemblyBinding/dependentAssembly 要素として追加するには  
  
1.  必要に応じて、**configuration** 要素の子要素として **runtime** 要素を追加します。追加しない場合は次の手順に進みます。  
  
     **runtime** 要素には、属性はありません。 **configuration** 要素には、**runtime** 子要素を 1 つだけ含めることができます。  
  
2.  必要に応じて、**runtime** 要素の子要素として **assemblyBinding** 要素を追加します。追加しない場合は次の手順に進みます。  
  
     **runtime** 要素には、**assemblyBinding** 要素を 1 つだけ含めることができます。  
  
3.  **assemblyBinding** 要素に、次の属性名と値を追加します。  
  
    |属性名|属性の値|  
    |--------------------|---------------------|  
    |**Xmlns**|**urn:schemas-microsoft-com:asm.v1**|  
  
4.  **assemblyBinding** 要素の子要素として **dependentAssembly** 要素を追加します。  
  
     **dependentAssembly** 要素には属性がありません。  
  
5.  **dependentAssembly** 要素の子として **assemblyIdentity** 要素を追加します。  
  
6.  **assemblyIdentity** 要素に、次の属性名と値を追加します。  
  
    |属性名|属性の値|  
    |--------------------|---------------------|  
    |**name**|**Microsoft.VisualStudio.Enterprise.ASPNetHelper**|  
    |**PublicKeyToken**|**b03f5f7f11d50a3a**|  
    |**culture**|**Neutral**|  
  
7.  **dependentAssembly** 要素の子として **codeBase** 要素を追加します。  
  
8.  **codeBase** 要素に、次の属性名と値を追加します。  
  
    |属性名|属性の値|  
    |--------------------|---------------------|  
    |**version**|**10.0.0.0**|  
    |**href**|`PathToASPNetHelperDll`|  
  
     `PathToASPNetHelperDll` は、Microsoft.VisualStudio.Enterprise.ASPNetHelper.dll のファイル URL です。 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] が既定の場所にインストールされている場合、**href** 値は `C:/Program%20Files/Microsoft%20Visual%20Studio%202010.0/Common7/IDE/PrivateAssemblies/Microsoft.VisualStudio.Enterprise.ASPNetHelper.DLL` となります。  
  
```  
    <configuration>  
        <runtime>  
            <assemblyBinding   
                xmlns="urn:schemas-microsoft-com:asm.v1"  
            >  
                <dependentAssembly>  
                    <assemblyIdentity                         name="Microsoft.VisualStudio.Enterprise.ASPNetHelper"   
                        publicKeyToken="b03f5f7f11d50a3a"                         culture="neutral"   
                    />  
                    <codeBase   
                        version="10.0.0.0"  
                        href="file:///C:/Program%20Files/Microsoft%20Visual%20Studio%2010.0/Common7/IDE/PrivateAssemblies/Microsoft.VisualStudio.Enterprise.ASPNetHelper.DLL"   
                    />  
                </dependentAssembly>  
            </assemblyBinding>  
        </runtime>  
```  
  
### <a name="to-add-the-profiler-post-process-step-to-the-configurationsystemwebcompilation-element"></a>configuration/system.web/compilation 要素にプロファイラーの処理後の手順を追加するには  
  
1.  必要に応じて、**configuration** 要素の子要素として **system.web** 要素を追加します。追加しない場合は次の手順に進みます。  
  
     **system.web** 要素には属性はありません。 **configuration** 要素には、**system.web** 子要素を 1 つだけ含めることができます。  
  
2.  必要に応じて、**system.web** 要素の子要素として **compilation** 要素を追加します。追加しない場合は次の手順に進みます。  
  
     **system.web** 要素には、**compilation** 子要素を 1 つだけ含めることができます。  
  
3.  **compilation** 要素に既存の属性があればすべて削除し、次の属性名と値を追加します。  
  
    |属性名|属性の値|  
    |--------------------|---------------------|  
    |**assemblyPostProcessorType**|**Microsoft.VisualStudio.Enterprise.Common.AspPerformanceInstrumenter, Microsoft.VisualStudio.Enterprise.ASPNetHelper, Version=10.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a**|  
  
```  
    <configuration>  
        <runtime>  
        . . .  
        </runtime>  
        <system.web>  
            <compilation  
                assemblyPostProcessorType="Microsoft.VisualStudio.Enterprise.Common.AspPerformanceInstrumenter,  
                    Microsoft.VisualStudio.Enterprise.ASPNetHelper,  
                    Version=10.0.0.0,  
                    Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a"   
            />  
        </system.web>  
    <configuration>  
```  
  
### <a name="to-add-profiler-location-settings-to-the-configurationappsettings-element"></a>プロファイラーの場所の設定を configuration/appSettings 要素に追加するには  
  
1.  必要に応じて、**configuration** 要素の子要素として **appSettings** 要素を追加します。追加しない場合は次の手順に進みます。  
  
     **appSettings** 要素には属性はありません。 **configuration** 要素には、**appSettings** 子要素を 1 つだけ含めることができます。  
  
2.  **add** 要素を **appSettings** 要素の子として追加します。  
  
3.  **add** 要素に、次の属性名と値を追加します。  
  
    |属性名|属性の値|  
    |--------------------|---------------------|  
    |**key**|**Microsoft.VisualStudio.Enterprise.AspNetHelper.VsInstrLocation**|  
    |**値**|`PerformanceToolsFolder` **\VSInstr.Exe**|  
  
4.  別の **add** 要素を **appSettings** 要素の子として追加します。  
  
5.  この **add** 要素に、次の属性名と値を追加します。  
  
    |属性名|属性の値|  
    |--------------------|---------------------|  
    |**key**|**Microsoft.VisualStudio.Enterprise.AspNetHelper.VsInstrTools**|  
    |**値**|`PerformanceToolsFolder`|  
  
     `PerformanceToolsFolder` は、プロファイラーの実行可能ファイルへのパスです。 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] が既定の場所にインストールされている場合、値は **C:\Program Files\Microsoft Visual Studio 10.0\Team Tools\Performance Tools** になります。  
  
```  
    <configuration>  
        <runtime>  
        . . .  
        </runtime>  
        . . .  
        <system.web>  
        </system.web>  
        <appSettings>  
            <add  
                key="Microsoft.VisualStudio.Enterprise.AspNetHelper.VsInstrLocation"  
                value="C:\Program Files\Microsoft Visual Studio 10.0\Team Tools\Performance Tools\vsinstr.exe"  
        />  
            <add  
                key="Microsoft.VisualStudio.Enterprise.AspNetHelper.VsInstrTools"  
                value="C:\Program Files\Microsoft Visual Studio 10.0\Team Tools\Performance Tools\"  
            />  
        </appSettings>  
    </configuration>  
```  
  
## <a name="example"></a>例  
 次に示すのは、動的にコンパイルされた [!INCLUDE[vstecasp](../includes/vstecasp-md.md)]Web アプリケーションのインストルメント化とプロファイルを可能にする完全な web.config ファイルです。 この例では、変更前のファイルには他の設定が含まれていないことを前提としています。  
  
```  
<?xml version="1.0"?>  
    <configuration>  
        <runtime>  
            <assemblyBinding   
                xmlns="urn:schemas-microsoft-com:asm.v1"  
            >  
                <dependentAssembly>  
                    <assemblyIdentity   
                        name="Microsoft.VisualStudio.Enterprise.ASPNetHelper"   
                        publicKeyToken="b03f5f7f11d50a3a"  
                        culture="neutral"   
                    />  
                    <codeBase   
                        version="10.0.0.0"  
                        href="file:///C:/Program%20Files/Microsoft%20Visual%20Studio%2010.0/Common7/IDE/PrivateAssemblies/Microsoft.VisualStudio.Enterprise.ASPNetHelper.DLL"   
                    />  
                </dependentAssembly>  
            </assemblyBinding>  
        </runtime>  
        <system.web>  
            <compilation  
                assemblyPostProcessorType="Microsoft.VisualStudio.Enterprise.Common.AspPerformanceInstrumenter,  
                    Microsoft.VisualStudio.Enterprise.ASPNetHelper,  
                    Version=10.0.0.0,  
                    Culture=neutral,  
                    PublicKeyToken=b03f5f7f11d50a3a"   
            />  
        </system.web>  
        <appSettings>  
            <add  
                key="Microsoft.VisualStudio.Enterprise.AspNetHelper.VsInstrLocation"  
                value="C:\Program Files\Microsoft Visual Studio 10.0\Team Tools\Performance Tools\vsinstr.exe"  
            />  
            <add  
                key="Microsoft.VisualStudio.Enterprise.AspNetHelper.VsInstrTools"  
                value="C:\Program Files\Microsoft Visual Studio 10.0\Team Tools\Performance Tools\"  
            />  
        </appSettings>  
    </configuration>  
  
```  
  
## <a name="see-also"></a>関連項目  
 [方法: 動的にコンパイルされた ASP.NET アプリケーションをインストルメントし、詳細なタイミング データを収集する](../profiling/how-to-instrument-a-dynamically-compiled-aspnet-web-application-and-collect-detailed-timing-data-with-the-profiler-by-using-the-command-line.md)   
 [方法: 動的にコンパイルされた ASP.NET アプリケーションをインストルメントし、メモリ データを収集する](../profiling/how-to-instrument-a-dynamically-compiled-aspnet-web-application-and-collect-memory-data-by-using-the-profiler-command-line.md)



