---
title: 標準ツールセット構成とカスタム ツールセット構成 | Microsoft Docs
ms.custom: ''
ms.date: 01/31/2018
ms.technology: msbuild
ms.topic: conceptual
helpviewer_keywords:
- MSBuild, custom toolset configurations
- MSBuild, msbuild.exe.config
ms.assetid: 15a048c8-5ad3-448e-b6e9-e3c5d7147ed2
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 855bd7af4372f5216abab3d6ddd45ec8f7809baa
ms.sourcegitcommit: 42ea834b446ac65c679fa1043f853bea5f1c9c95
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/19/2018
ms.locfileid: "31573116"
---
# <a name="standard-and-custom-toolset-configurations"></a>標準ツールセット構成とカスタム ツールセット構成
MSBuild ツールセットには、アプリケーション プロジェクトのビルドに使用できるタスク、ターゲット、およびツールへの参照が含まれています。 MSBuild には標準ツールセットが用意されていますが、カスタム ツールセットを作成することもできます。 ツールセットを指定する方法については、「[ツールセット (ToolsVersion)](../msbuild/msbuild-toolset-toolsversion.md)」を参照してください。  
  
## <a name="standard-toolset-configurations"></a>標準ツールセット構成  
 MSBuild 15.0 には以下の標準ツールセットが含まれています。  
  
|ToolsVersion|ツールセットのパス (MSBuildToolsPath ビルド プロパティまたは MSBuildBinPath ビルド プロパティで指定)|  
|------------------|--------------------------------------------------------------------------------------------|  
|2.0|*Windows インストール パス*\Microsoft.Net\Framework\v2.0.50727\|  
|3.5|*Windows インストール パス*\Microsoft.NET\Framework\v3.5\|  
|4.0|*Windows インストール パス*\Microsoft.NET\Framework\v4.0.30319\|  
|15.0|*Visual Studio インストール パス*\MSBuild\15.0\bin|  
  
 `ToolsVersion` の値によって、Visual Studio で生成されたプロジェクトが使用するツールセットが決まります。 Visual Studio 2017 では、既定値は "15.0" です (プロジェクト ファイルにどのバージョンが指定されている場合でも)。ただし、コマンド プロンプトで **/toolsversion** スイッチを使って、この属性を上書きできます。 この属性に関する情報と `ToolsVersion` を指定するその他の方法については、「[ToolsVersion 設定のオーバーライド](../msbuild/overriding-toolsversion-settings.md)」を参照してください。  
  
 Visual Studio 2017 では、MSBuild のパスにレジストリ キーは使われません。 Visual Studio 2017 でインストールされる 15.0 より前のバージョンの MSBuild では、以下のレジストリ キーで MSBuild.exe のインストール パスが指定されます。  
  
|レジストリ キー|キー名|文字列キー値|  
|------------------|--------------|----------------------|  
|\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSBuild\ToolsVersions\2.0\|MSBuildToolsPath|.NET Framework 2.0 インストール パス|  
|\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ MSBuild\ToolsVersions\3.5\|MSBuildToolsPath|.NET Framework 3.5 インストール パス|  
|\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ MSBuild\ToolsVersions\4.0\|MSBuildToolsPath|.NET Framework 4 インストール パス|  
  
### <a name="sub-toolsets"></a>サブツールセット  
 前の表のレジストリ キーにサブキーがある場合、MSBuild はそのサブキーを使って、親ツールセットのパスを上書きするサブツールセットを決定します。 たとえば、次のようなサブキーがあります。  
  
 \HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSBuild\ToolsVersions\12.0\12.0  
  
 基本ツールセットと選択されたサブツールセットの両方でプロパティが定義されている場合、サブツールセットのプロパティ定義が使用されます。 たとえば、MSBuild 4.0 ツールセットで、7.0A SDK を指す `SDK40ToolsPath` が定義されているが、MSBuild 4.0\11.0 ツールセットでは、同じプロパティが 8.0A SDK を指すように定義されているとします。 `VisualStudioVersion` が設定されていない場合、`SDK40ToolsPath` は 7.0A を指しますが、`VisualStudioVersion` が 11.0 に設定されている場合、このプロパティは 7.0A ではなく 8.0A を指します。  
  
 `VisualStudioVersion` ビルド プロパティは、サブツールセットをアクティブにするかどうかを示します。 たとえば、`VisualStudioVersion` の値が "12.0" である場合は、MSBuild 12.0 サブツールセットを指定します。 詳細については、「[ツールセット (ToolsVersion)](../msbuild/msbuild-toolset-toolsversion.md)」の「サブツールセット」のセクションを参照してください。  
  
> [!NOTE]
>  これらの設定は変更しないことをお勧めします。 ただし、独自の設定を追加し、コンピューター全体に適用されるカスタム ツールセットの定義を指定することはできます。その手順については次のセクションで説明します。  
  
## <a name="custom-toolset-definitions"></a>カスタム ツールセット定義  
 標準ツールセットがビルド要件に適合しない場合は、カスタム ツールセットを作成できます。 たとえば、ビルド ラボ シナリオで、[!INCLUDE[vcprvc](../code-quality/includes/vcprvc_md.md)] プロジェクトをビルドするために個別のシステムが必要になる場合があります。 カスタム ツールセットを使用することにより、プロジェクトの作成時や MSBuild.exe の実行時に `ToolsVersion` 属性にカスタム値を割り当てることができます。 これを行うことで、`$(MSBuildToolsPath)` プロパティを使用して、該当のディレクトリから .targets ファイルをインポートできます。また、カスタム ツールセットを使用するすべてのプロジェクトで利用できる独自のカスタム ツールセット プロパティを定義することもできます。  
  
 カスタム ツールセットは、MSBuild.exe の構成ファイルに指定します。ただし、MSBuild エンジンをホストするカスタム ツールを使用している場合は、そのカスタム ツールの構成ファイルに指定します。 たとえば、ToolsVersion 15.0 の既定の動作を上書きする場合、MSBuild.exe の構成ファイルには次のようなツールセット定義を含めることができます。  
  
```xml  
<msbuildToolsets default="15.0">  
   <toolset toolsVersion="15.0">  
      <property name="MSBuildToolsPath"   
        value="C:\SpecialPath" />  
   </toolset>  
</msbuildToolsets>  
```  
  
 また `<msbuildToolsets>` は、構成ファイル内で次のように定義する必要があります。  
  
```xml  
<configSections>  
   <section name="msbuildToolsets"         
       Type="Microsoft.Build.BuildEngine.ToolsetConfigurationSection,   
       Microsoft.Build.Engine, Version=15.1.0.0, Culture=neutral,   
       PublicKeyToken=b03f5f7f11d50a3a"  
   </section>  
</configSections>  
```  
  
> [!NOTE]
>  コードが正しく読み込まれるようにするには、`<configSections>` を `<configuration>` セクション内の最初のサブセクションにする必要があります。  
  
 `ToolsetConfigurationSection` は、どのような MSBuild ホストでもカスタム構成として使用できるカスタム構成セクションです。 カスタム ツールセットを使用した場合、ホストでは、構成ファイル エントリの提供を除き、ビルド エンジンの初期化処理は必要ありません。 レジストリにエントリを定義することにより、コンピューター全体を対象としたツールセットを指定して、そのツールセットを MSBuild.exe、[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]、および MSBuild のすべてのホストに適用できます。  
  
> [!NOTE]
>  レジストリに定義済みの `ToolsVersion` の設定を構成ファイルに定義した場合、2 つの定義はマージされません。 構成ファイル内の定義が優先され、同じ `ToolsVersion` のレジストリ内の設定は無視されます。  
  
 プロジェクトで使用される `ToolsVersion` 値に固有のプロパティを次に示します。  
  
-   **$(MSBuildBinPath)** は、`ToolsVersion` が定義されているレジストリまたは構成ファイルで指定された `ToolsPath` 値に設定されます。 レジストリまたは構成ファイルの `$(MSBuildToolsPath)` 設定は、コア タスクとコア ターゲットの場所を指定します。 プロジェクト ファイルでは、この設定が $(MSBuildBinPath) プロパティにマップされ、さらに $(MSBuildToolsPath) プロパティにもマップされます。  
  
-   `$(MSBuildToolsPath)`: このプロパティは予約済みのプロパティであり、構成ファイルで指定されている MSBuildToolsPath プロパティによって提供されます  (このプロパティは `$(MSBuildBinPath)` に代わるものです。 ただし、`$(MSBuildBinPath)` も互換性のために残されています)。カスタム ツールセットでは、`$(MSBuildToolsPath)` または `$(MSBuildBinPath)` のいずれか一方を定義してください。両方定義する場合は、これらのプロパティは同じ値になる必要があります。  
  
 MSBuildToolsPath プロパティを追加する場合と同じ構文を使用して、ToolsVersion 固有のカスタム プロパティを構成ファイルに追加することもできます。 このようなカスタム プロパティをプロジェクト ファイルで利用できるようにするには、構成ファイルに指定された値の名前と同じ名前を使用します。 構成ファイルではツールセットを定義できますが、サブツールセットは定義できません。  
  
## <a name="see-also"></a>参照  
 [ツールセット (ToolsVersion)](../msbuild/msbuild-toolset-toolsversion.md)