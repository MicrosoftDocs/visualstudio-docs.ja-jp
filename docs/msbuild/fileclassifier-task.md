---
title: FileClassifier タスク | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- classifying a resource set to embed in an assembly [WPF MSBuild]
- non-localizable resources [WPF MSBuild], classifying to embed in an assembly
- FileClassifier task [WPF MSBuild]
ms.assetid: 14e03310-fcc0-4bb2-a84d-cda12be66367
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 9dccb229712d173e847a7205f03aad308fab224d
ms.sourcegitcommit: 01334abf36d7e0774329050d34b3a819979c95a2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/07/2019
ms.locfileid: "55853194"
---
# <a name="fileclassifier-task"></a>FileClassifier タスク
<xref:Microsoft.Build.Tasks.Windows.FileClassifier> タスクは、ソース リソースのセットをアセンブリに埋め込まれるリソースとして分類します。 ローカライズできないリソースは、メイン アプリケーション アセンブリに埋め込まれます。ローカライズ可能なリソースは、サテライト アセンブリに埋め込まれます。

## <a name="task-parameters"></a>タスク パラメーター

|パラメーター|説明|
|---------------|-----------------|
|`CLREmbeddedResource`|使用されません。|
|`CLRResourceFiles`|使用されません。|
|`CLRSatelliteEmbeddedResource`|使用されません。|
|`Culture`|省略可能な **String** 型のパラメーターです。<br /><br /> ビルドのカルチャを指定します。 ローカライズできないビルドの場合は、この値に **null** を指定できます。 **null** の場合、既定値は **CultureInfo.InvariantCulture** から返される小文字の値になります。|
|`MainEmbeddedFiles`|省略可能な **ITaskItem[]** 型の出力パラメーターです。<br /><br /> メイン アセンブリに埋め込まれる、ローカライズできないリソースを指定します。|
|`OutputType`|必須の **String** 型のパラメーターです。<br /><br /> 指定したソース ファイルが埋め込まれるファイルの種類を指定します。 有効な値は、**exe**、**winexe**、または **library** です。|
|`SatelliteEmbeddedFiles`|省略可能な **ITaskItem[]** 型の出力パラメーターです。<br /><br /> **Culture** パラメーターで指定されたカルチャのサテライト アセンブリに埋め込まれる、ローカライズ可能なファイルを指定します。|
|`SourceFiles`|必須の **ITaskItem[]** 型のパラメーターです。<br /><br /> 分類するファイルのリストを指定します。|

## <a name="remarks"></a>コメント
**Culture** パラメーターを設定しない場合、**SourceFiles** パラメーターを使用して指定したリソースは、すべてローカライズできないリソースになります。それ以外の場合は、**Localizable** 属性が **false** に設定されていない限り、ローカライズ可能なリソースになります。

## <a name="example"></a>例
次の例では、単一のソース ファイルをリソースとして分類し、French-Canadian (fr-CA) カルチャのサテライト アセンブリに埋め込みます。

```xml
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
  <UsingTask
    TaskName="Microsoft.Build.Tasks.Windows.FileClassifier"
    AssemblyFile="C:\Program Files\Reference Assemblies\Microsoft\Framework\v3.0\PresentationBuildTasks.dll" />
  <ItemGroup>
    <Resource Include="Resource1.bmp" />
  </ItemGroup>
  <Target Name="FileClassifierTask">
    <FileClassifier
      SourceFiles="Resource1.bmp"
      Culture="fr-CA"
      OutputType="exe" />
  </Target>
</Project>
```

## <a name="see-also"></a>関連項目
[WPF MSBuild のリファレンス](../msbuild/wpf-msbuild-reference.md)  
[タスク リファレンス](../msbuild/wpf-msbuild-task-reference.md)  
[MSBuild リファレンス](../msbuild/msbuild-reference.md)  
[タスク リファレンス](../msbuild/msbuild-task-reference.md)  
[WPF アプリケーション (WPF) のビルド](/dotnet/framework/wpf/app-development/building-a-wpf-application-wpf)
