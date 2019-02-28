---
title: MarkupCompilePass2 タスク | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: msbuild
ms.topic: reference
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- performing second-pass markup [WPF MSBuild], MarkupCompilePass2 task
- MarkupCompilePass2 task [WPF MSBuild]
- MarkupCompilePass2 task [WPF MSBuild], parameters
ms.assetid: 1d25689a-d21f-4b05-be26-95aa0ed4fd03
caps.latest.revision: 11
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 87c31551541bc949a98ec2dd7a15da5a86b36d21
ms.sourcegitcommit: a83c60bb00bf95e6bea037f0e1b9696c64deda3c
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 02/19/2019
ms.locfileid: "54777093"
---
# <a name="markupcompilepass2-task"></a>MarkupCompilePass2 タスク
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
<xref:Microsoft.Build.Tasks.Windows.MarkupCompilePass2> タスクは、同じプロジェクト内で型を参照する [!INCLUDE[TLA#tla_xaml](../includes/tlasharptla-xaml-md.md)] ファイルの 2 回目のマークアップのコンパイルを実行します。  
  
## <a name="task-parameters"></a>タスク パラメーター  
  
|パラメーター|説明|  
|---------------|-----------------|  
|`AlwaysCompileMarkupFilesInSeparateDomain`|省略可能な **Boolean** 型のパラメーターです。<br /><br /> 別の <xref:System.AppDomain> でタスクを実行するかどうかを指定します。 このパラメーターが **false** を返す場合、タスクは [!INCLUDE[TLA#tla_msbuild](../includes/tlasharptla-msbuild-md.md)] と同じ <xref:System.AppDomain> 内で、より高速に実行されます。 このパラメーターが **true** を返す場合、タスクは [!INCLUDE[TLA2#tla_msbuild](../includes/tla2sharptla-msbuild-md.md)] から分離された 2 番目の <xref:System.AppDomain> 内で実行され、動作はより低速になります。|  
|`AssembliesGeneratedDuringBuild`|省略可能な **String[]** 型のパラメーターです。<br /><br /> ビルド処理時に変更されるアセンブリへの参照を指定します。 たとえば、[!INCLUDE[TLA#tla_visualstu2005](../includes/tlasharptla-visualstu2005-md.md)] ソリューションには、別のプロジェクトのコンパイル済み出力を参照するプロジェクトが含まれていることがあります。 この場合、別のプロジェクトのコンパイル済み出力を **AssembliesGeneratedDuringBuild** に追加できます。<br /><br /> 注: **AssembliesGeneratedDuringBuild** は、ビルド ソリューションによって生成されるアセンブリの完全なセットへの参照を含んでいる必要があります。|  
|`AssemblyName`|必須の **String** 型のパラメーターです。<br /><br /> プロジェクトのために生成されるアセンブリの短い名前を指定します。 たとえば、プロジェクトが **WinExeAssembly.exe** という名前の [!INCLUDE[TLA#tla_win](../includes/tlasharptla-win-md.md)] 実行可能ファイルを生成する場合、**AssemblyName** パラメーターの値は **WinExeAssembly** になります。|  
|`GeneratedBaml`|省略可能な **ITaskItem[]** 型の出力パラメーターです。<br /><br /> [!INCLUDE[TLA2#tla_xaml](../includes/tla2sharptla-xaml-md.md)] バイナリ形式で生成されたファイルの一覧を含みます。|  
|`KnownReferencePaths`|省略可能な **String[]** 型のパラメーターです。<br /><br /> ビルド処理時に変更されないアセンブリへの参照を指定します。 [!INCLUDE[TLA#tla_gac](../includes/tlasharptla-gac-md.md)]、[!INCLUDE[TLA#tla_netframewk](../includes/tlasharptla-netframewk-md.md)] インストール ディレクトリなどにあるアセンブリが含まれます。|  
|`Language`|必須の **String** 型のパラメーターです。<br /><br /> コンパイラがサポートするマネージド言語を指定します。 有効なオプションは **C#**、**VB**、**JScript**、**C++** です。|  
|`LocalizationDirectivesToLocFile`|省略可能な **String** 型のパラメーターです。<br /><br /> 各ソース [!INCLUDE[TLA2#tla_xaml](../includes/tla2sharptla-xaml-md.md)] ファイルのローカリゼーション情報を生成する方法を指定します。 有効なオプションは、**None**、**CommentsOnly**、および **All** です。|  
|`OutputPath`|必須の **String** 型のパラメーターです。<br /><br /> [!INCLUDE[TLA2#tla_xaml](../includes/tla2sharptla-xaml-md.md)] バイナリ形式ファイルが生成されるディレクトリを指定します。|  
|`OutputType`|必須の **String** 型のパラメーターです。<br /><br /> プロジェクトで生成されるアセンブリの型を指定します。 有効なオプションは、**winexe**、**exe**、**library**、および **netmodule** です。|  
|`References`|省略可能な **ITaskItem[]** パラメーターです。<br /><br /> [!INCLUDE[TLA2#tla_xaml](../includes/tla2sharptla-xaml-md.md)] ファイル内で使用される型を含む、ファイルからアセンブリへの参照の一覧を指定します。 そのうちの 1 つは、<xref:Microsoft.Build.Tasks.Windows.GenerateTemporaryTargetAssembly> タスクによって生成されたアセンブリへの参照です。このタスクは、<xref:Microsoft.Build.Tasks.Windows.MarkupCompilePass2> タスクの前に実行しておく必要があります。|  
|`RootNamespace`|省略可能な **String** 型のパラメーターです。<br /><br /> プロジェクト内部にあるクラスのルート名前空間を指定します。 **RootNamespace** は、対応する [!INCLUDE[TLA2#tla_xaml](../includes/tla2sharptla-xaml-md.md)] ファイルが `x:Class` 属性を含まない場合に、生成されるマネージド コード ファイルの既定の名前空間としても使用されます。|  
|`XAMLDebuggingInformation`|省略可能な **Boolean** 型のパラメーターです。<br /><br /> **true** の場合、デバッグを支援するための診断情報が生成され、コンパイルされた [!INCLUDE[TLA2#tla_xaml](../includes/tla2sharptla-xaml-md.md)] 内に追加されます。|  
  
## <a name="remarks"></a>解説  
 **MarkupCompilePass2** を実行する前に、マークアップ コンパイル パスが延期された [!INCLUDE[TLA2#tla_xaml](../includes/tla2sharptla-xaml-md.md)] ファイルによって使用される型を含む、一時アセンブリを生成する必要があります。 一時アセンブリを生成するには、**GenerateTemporaryTargetAssembly** タスクを実行します。  
  
 <xref:Microsoft.Build.Tasks.Windows.MarkupCompilePass2> の実行時には、生成された一時アセンブリへの参照を指定します。これにより、最初のマークアップ コンパイル パスでコンパイルが延期された [!INCLUDE[TLA2#tla_xaml](../includes/tla2sharptla-xaml-md.md)] ファイルをバイナリ形式にコンパイルできるようになります。  
  
## <a name="example"></a>例  
 <xref:Microsoft.Build.Tasks.Windows.MarkupCompilePass2> タスクを使用して 2 番目のコンパイル パスを実行する方法を次の例に示します。  
  
```  
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">  
  <UsingTask   
    TaskName="Microsoft.Build.Tasks.Windows.MarkupCompilePass2"   
    AssemblyFile="C:\Program Files\Reference Assemblies\Microsoft\Framework\v3.0\PresentationBuildTasks.dll" />  
  <Target Name="MarkupCompilePass2Task">  
    <MarkupCompilePass2   
      AssemblyName="WPFMSBuildSample"  
      Language="C#"  
      OutputType="WinExe"  
      OutputPath="obj\Debug\"  
      References=".\obj\debug\WPFMSBuildSample.exe;c:\windows\Microsoft.net\Framework\v2.0.50727\System.dll;C:\Program Files\Reference Assemblies\Microsoft\WinFx\v3.0\PresentationCore.dll;C:\Program Files\Reference Assemblies\Microsoft\WinFx\v3.0\PresentationFramework.dll;C:\Program Files\Reference Assemblies\Microsoft\WinFx\v3.0\WindowsBase.dll" />  
  </Target>  
</Project>  
```  
  
## <a name="see-also"></a>関連項目
 [WPF MSBuild リファレンス](../msbuild/wpf-msbuild-reference.md)   
 [Task Reference (タスク リファレンス)](../msbuild/wpf-msbuild-task-reference.md)   
 [MSBuild リファレンス](../msbuild/msbuild-reference.md)   
 [Task Reference (タスク リファレンス)](../msbuild/msbuild-task-reference.md)   
 [WPF アプリケーション (WPF) のビルド](http://msdn.microsoft.com/library/a58696fd-bdad-4b55-9759-136dfdf8b91c)   
 [WPF XAML ブラウザー アプリケーションの概要](http://msdn.microsoft.com/library/3a7a86a8-75d5-4898-96b9-73da151e5e16)
