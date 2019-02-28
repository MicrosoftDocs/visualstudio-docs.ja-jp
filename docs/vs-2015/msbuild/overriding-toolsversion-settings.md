---
title: ToolsVersion 設定のオーバーライド | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: msbuild
ms.topic: conceptual
helpviewer_keywords:
- MSBuild, overriding ToolsVersion setting
- MSBuild, building solutions with
ms.assetid: ccd42c07-0fb6-4e8b-9ebb-a6a6db18aa2e
caps.latest.revision: 27
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: e4cd6d3199d09ffa56c0ac6d2d29fcba613fd280
ms.sourcegitcommit: a83c60bb00bf95e6bea037f0e1b9696c64deda3c
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 02/19/2019
ms.locfileid: "54770711"
---
# <a name="overriding-toolsversion-settings"></a>ToolsVersion 設定のオーバーライド
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
プロジェクトおよびソリューションのツールセットは、次の 3 つの方法のいずれかで変更できます。  
  
1.  コマンド ラインからプロジェクトまたはソリューションをビルドする場合は、`/ToolsVersion` スイッチ (省略形は `/tv`) を使用します。  
  
2.  MSBuild タスクに `ToolsVersion` パラメーターを設定します。  
  
3.  ソリューション内のプロジェクトに `$(ProjectToolsVersion)` プロパティを設定します。 これにより、他のプロジェクトとは異なるツールセットのバージョンを使用して、ソリューション内にプロジェクトをビルドできます。  
  
## <a name="override-the-toolsversion-settings-of-projects-and-solutions-on-command-line-builds"></a>コマンド ラインでのビルドでプロジェクトおよびソリューションの ToolsVersion 設定をオーバーライドする  
 Visual Studio プロジェクトは通常、プロジェクト ファイルに指定された ToolsVersion でビルドされますが、コマンド ラインで `/ToolsVersion` (または `/tv`) スイッチを指定することによって、プロジェクト ファイルの ToolsVersion 値をオーバーライドし、すべてのプロジェクトとそのプロジェクト間依存関係を別のツールセットでビルドできます。 次に例を示します。  
  
```  
msbuild.exe someproj.proj /tv:12.0 /p:Configuration=Debug  
```  
  
 この例では、すべてのプロジェクトが ToolsVersion 12.0 でビルドされます  (後の「優先順位」を参照してください)。  
  
 コマンド ラインで `/tv` スイッチを使用するときには、特定のプロジェクトに `$(ProjectToolsVersion)` プロパティを指定し、ソリューション内の他のプロジェクトとは異なる ToolsVersion 値でビルドすることもできます。  
  
## <a name="override-the-toolsversion-settings-using-the-toolsversion-parameter-of-the-msbuild-task"></a>MSBuild タスクの ToolsVersion パラメーターを使用して ToolsVersion 設定をオーバーライドする  
 MSBuild タスクは、あるプロジェクトで別のプロジェクトをビルドするための主要な手段です。 MSBuild タスクには、プロジェクトに指定された値とは異なる ToolsVersion でプロジェクトをビルドすることが可能となる省略可能なタスク パラメーター `ToolsVersion` が用意されています。 このパラメーターを使用する方法を次の例に示します。  
  
1.  次のコードを含む `projectA.proj` という名前のファイルを作成します。  
  
    ```  
    <Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003"  
    ToolsVersion="12.0">  
  
        <Target Name="go" >   
            <Message Text="projectA.proj" />  
            <Message Text="MSBuildToolsVersion: $(MSBuildToolsVersion)" />  
            <Message Text="MSBuildToolsPath:    $(MSBuildToolsPath)" />  
  
            <MSBuild Projects="projectB.proj"  
                ToolsVersion="2.0"  
                Targets="go" />  
        </Target>  
    </Project>  
    ```  
  
2.  次のコードを含む `projectB.proj` という名前の別のファイルを作成します。  
  
    ```  
    <Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003"  
    ToolsVersion="12.0">  
  
        <Target Name="go">  
            <Message Text="projectB.proj" />  
            <Message Text="MSBuildToolsVersion: $(MSBuildToolsVersion)" />  
            <Message Text="MSBuildToolsPath:    $(MSBuildToolsPath)" />  
        </Target>  
    </Project>  
    ```  
  
3.  コマンド プロンプトに次のコマンドを入力します。  
  
    ```  
    msbuild projectA.proj /t:go /toolsversion:3.5  
    ```  
  
4.  次のような出力が表示されます。 `projectA` では、コマンド ラインに設定された `/toolsversion:3.5` が、`ToolsVersion=12.0` タグに設定された `Project` をオーバーライドします。  
  
     `ProjectB` は `projectA` 内のタスクによって呼び出されます。 そのタスクには `ToolsVersion=2.0` が設定されており、この設定は、`ToolsVersion` の他の `projectB` 設定をオーバーライドします。  
  
    ```  
    Output:  
      projectA.proj  
      MSBuildToolsVersion: 3.5  
      MSBuildToolsPath:    C:\Windows\Microsoft.NET\Framework\v3.5  
  
      projectB.proj  
      MSBuildToolsVersion: 2.0  
      MSBuildToolsPath:    C:\Windows\Microsoft.NET\Framework\v2.0.50727  
    ```  
  
## <a name="order-of-precedence"></a>優先順位  
 `ToolsVersion` は、次の優先順位に基づいて決定されます (順位の高いものから先に挙げています)。  
  
1.  プロジェクトのビルドに使用される MSBuild タスクの `ToolsVersion` 属性。  
  
2.  msbuild.exe のコマンドで使用される `/toolsversion` (または `/tv`) スイッチ。  
  
3.  環境変数 `MSBUILDTREATALLTOOLSVERSIONSASCURRENT` が設定されている場合は、現在の `ToolsVersion` を使用します。  
  
4.  環境変数 `MSBUILDTREATHIGHERTOOLSVERSIONASCURRENT` が設定され、プロジェクト ファイルで定義されている `ToolsVersion` が現在の `ToolsVersion` よりも大きい場合は、現在の `ToolsVersion` を使用します。  
  
5.  環境変数 `MSBUILDLEGACYDEFAULTTOOLSVERSION` が設定されているか、または `ToolsVersion` が設定されていない場合は、次の手順が使用されます。  
  
    1.  プロジェクト ファイルにある [Project](../msbuild/project-element-msbuild.md) 要素の `ToolsVersion` 属性。 この属性が存在しない場合は、現在のバージョンであると見なされます。  
  
    2.  MSBuild.exe.config ファイルに定義された既定のツール バージョン。  
  
    3.  レジストリに定義された既定のツール バージョン。 詳細については、「[標準ツールセット構成とカスタム ツールセット構成](../msbuild/standard-and-custom-toolset-configurations.md)」を参照してください。  
  
6.  環境変数 `MSBUILDLEGACYDEFAULTTOOLSVERSION` が設定されていない場合は、次の手順が使用されます。  
  
    1.  環境変数 `MSBUILDDEFAULTTOOLSVERSION` が存在する `ToolsVersion` に設定されている場合は、それを使用します。  
  
    2.  `DefaultOverrideToolsVersion` が MSBuild.exe.config で設定されている場合は、それを使用します。  
  
    3.  `DefaultOverrideToolsVersion` がレジストリで設定されている場合は、それを使用します。  
  
    4.  それ以外の場合は、現在の `ToolsVersion` を使用します。  
  
## <a name="see-also"></a>関連項目
 [マルチターゲット](../msbuild/msbuild-multitargeting-overview.md)   
 [MSBuild の概念](../msbuild/msbuild-concepts.md)   
 [ツール セット (ToolsVersion)](../msbuild/msbuild-toolset-toolsversion.md)   
 [標準ツールセット構成とカスタム ツールセット構成](../msbuild/standard-and-custom-toolset-configurations.md)
