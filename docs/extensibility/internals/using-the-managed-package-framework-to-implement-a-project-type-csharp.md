---
title: プロジェクトの種類 (C#) に合わせて Managed Package Framework を使用する
description: Managed Package Framework について説明します。これには、独自のプロジェクトの種類を実装するために使用または継承できる .NET クラスが用意されています。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- projects [Visual Studio SDK], creating with MPF
- MPF projects
- managed package framework, creating projects
ms.assetid: 926de536-eead-415b-9451-f1ddc8c44630
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: cb047c9ef8c5c47c6509a6a5947be77a488e22f5
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105060732"
---
# <a name="using-the-managed-package-framework-to-implement-a-project-type-c"></a>マネージド パッケージ フレームワークを使用したプロジェクト タイプの実装 (C#)
Managed Package Framework (MPF) には、独自のプロジェクトの種類を実装するために使用または継承できる C# クラスが用意されています。 Visual Studio からプロジェクトの種類に対して期待されるインターフェイスの多くが MPF に実装されているため、プロジェクトの種類の特定の部分の実装に集中することができます。

## <a name="using-the-mpf-project-source-code"></a>MPF プロジェクトのソース コードの使用
 プロジェクト用 Managed Package Framework (MPFProj) には、新しいプロジェクト システムを作成および管理するためのヘルパー クラスが用意されています。 MPF の他のクラスとは異なり、プロジェクト クラスは Visual Studio に付属のアセンブリには含まれていません。 代わりに、プロジェクト クラスは [MPF for Projects 2013](https://github.com/tunnelvisionlabs/MPFProj10) のソース コードとして用意されています。

 このプロジェクトを VSPackage ソリューションに追加するには、次の手順を実行します。

1. MPFProj ファイルを *MPFProjectDir* にダウンロードします。

2. *MPFProjectDir*\Dev10\Src\CSharp\ProjectBase.file で、次のブロックを変更します。

```
<!-- Provide a default value for $(ProjectBasePath) -->
  <PropertyGroup>
    <ProjectBasePath >MPFProjDir\Dev10\Src\CSharp</ProjectBasePath>
  </PropertyGroup>
```

1. VSPackage プロジェクトを作成します。

2. VSPackage プロジェクトをアンロードします。

3. 他の `<Import>` ブロックの前に次のブロックを追加して、VSPackage.csproj ファイルを編集します。

```
<Import Project="MPFProjectDir\Dev10\Src\CSharp\ProjectBase.files" />
  <PropertyGroup>
    <!--To specify a different registry root to register your package, uncomment the TargetRegistryRoot tag and specify a registry root in it.
    <TargetRegistryRoot></TargetRegistryRoot>-->
    <RegisterOutputPackage>true</RegisterOutputPackage>
    <RegisterWithCodebase>true</RegisterWithCodebase>
  </PropertyGroup>
```

1. プロジェクトを保存します。

2. VSPackage ソリューションを閉じて再度開きます。

3. VSPackage プロジェクトを再度開きます。 ProjectBase という名前の新しいディレクトリが表示されます。

4. VSPackage プロジェクトに次の参照を追加します。

     Microsoft.Build.Tasks.4.0

5. プロジェクトをビルドします。

## <a name="hierarchy-classes"></a>階層クラス
 次の表は、プロジェクト階層をサポートする MPFProj のクラスをまとめたものです。 詳細については、「[階層と選択](../../extensibility/internals/hierarchies-and-selection.md)」を参照してください。

|クラス名|
|----------------|
|`Microsoft.VisualStudio.Package.HierarchyNode`|
|`Microsoft.VisualStudio.Package.ProjectNode`|
|`Microsoft.VisualStudio.Package.ProjectContainerNode`|
|`Microsoft.VisualStudio.Package.FileNode`|
|`Microsoft.VisualStudio.Package.FolderNode`|
|`Microsoft.VisualStudio.Package.ReferenceContainerNode`|
|`Microsoft.VisualStudio.Package.ReferenceNode`|
|`Microsoft.VisualStudio.Package.ProjectReferenceNode`|
|`Microsoft.VisualStudio.Package.ComReferenceNode`|
|`Microsoft.VisualStudio.Package.AssemblyReferenceNode`|
|`Microsoft.VisualStudio.Package.BuildDependency`|

## <a name="document-handling-classes"></a>ドキュメント処理クラス
 次の表は、ドキュメント処理をサポートする MPF のクラスの一覧です。 詳細については、「[プロジェクト項目のオープンと保存](../../extensibility/internals/opening-and-saving-project-items.md)」を参照してください。

|クラス名|
|----------------|
|`Microsoft.VisualStudio.Package.DocumentManager`|
|`Microsoft.VisualStudio.Package.FileDocumentManager`|

## <a name="configuration-and-output-classes"></a>構成と出力のクラス
 次の表は、プロジェクトの種類で、デバッグやリリース、プロジェクト出力のコレクションなどの複数の構成をサポートできるようになる MPF のクラスの一覧です。 詳細については、「[構成オプションの管理](../../extensibility/internals/managing-configuration-options.md)」を参照してください。

|クラス名|
|----------------|
|`Microsoft.VisualStudio.Package.ConfigProvider`|
|`Microsoft.VisualStudio.Package.ProjectConfig`|
|`Microsoft.VisualStudio.Package.BuildableProjectConfig`|
|`Microsoft.VisualStudio.Package.OutputGroup`|
|`Microsoft.VisualStudio.Package.ProjectElement`|

## <a name="automation-support-classes"></a>自動化サポート クラス
 次の表は、プロジェクトの種類のユーザーがアドインを記述できるようにする自動化をサポートする MPF のクラスの一覧です。

|クラス名|
|----------------|
|`Microsoft.VisualStudio.Package.Automation.OAProject`|
|`Microsoft.VisualStudio.Package.Automation.OANavigableProjectItems`|
|`Microsoft.VisualStudio.Package.Automation.OAProjectItems`|
|`Microsoft.VisualStudio.Package.Automation.OAProjectItem`|
|`Microsoft.VisualStudio.Package.Automation.OANestedProjectItem`|

## <a name="properties-classes"></a>プロパティ クラス
 次の表は、ユーザーがプロパティ ブラウザーで参照および変更できるプロパティをプロジェクトの種類に追加できるようにする MPF のクラスの一覧です。

|クラス名|
|----------------|
|`Microsoft.VisualStudio.Package.LocalizableProperties`|
|`Microsoft.VisualStudio.Package.NodeProperties`|
|`Microsoft.VisualStudio.Package.FileNodeProperties`|
|`Microsoft.VisualStudio.Package.ProjectNodeProperties`|
|`Microsoft.VisualStudio.Package.FolderNodeProperties`|
|`Microsoft.VisualStudio.Package.ReferenceNodeProperties`|
