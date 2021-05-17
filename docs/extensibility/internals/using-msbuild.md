---
title: MSBuild の使用 | Microsoft Docs
description: MSBuild には、ビルドするプロジェクト項目、ビルド タスク、およびビルド構成を完全に記述するプロジェクト ファイルを作成するための、拡張性のある XML 形式が用意されています。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- VSPackages, compiling with MSBuild
- MSBuild, extensibility
- packages, compiling with MSBuild
ms.assetid: 9d38c388-1f64-430e-8f6c-e88bc99a4260
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 8891d9674a952f0272855c8b9203109ad2e22468
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105090695"
---
# <a name="using-msbuild"></a>MSBuild の使用
MSBuild には、ビルドするプロジェクト項目、ビルド タスク、およびビルド構成を完全に記述するプロジェクト ファイルを作成するための、適切に定義された拡張性のある XML 形式が用意されています。

## <a name="general-msbuild-considerations"></a>MSBuild に関する一般的な考慮事項
 MSBuild プロジェクト ファイル ([!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)] の .csproj や [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)] の .vbproj ファイルなど) には、ビルド時に使用されるデータが含まれていますが、設計時に使用されるデータを含めることもできます。 ビルド時のデータは、[Item 要素 (MSBuild)](../../msbuild/item-element-msbuild.md) や [Property 要素 (MSBuild)](../../msbuild/property-element-msbuild.md)などの MSBuild プリミティブを使用して格納されます。 設計時のデータは、プロジェクトの種類や関連するプロジェクトのサブタイプに固有のデータであり、そのために予約された自由形式の XML で格納されます。

 MSBuild には構成オブジェクトのネイティブ サポートはありませんが、構成固有のデータを指定するための条件付き属性が用意されています。 次に例を示します。

```xml
<OutputDir Condition="'$(Configuration)'=="release'">Bin\MyReleaseConfig</OutputDir>
```

 条件付き属性の詳細については、「[条件構造](../../msbuild/msbuild-conditional-constructs.md)」を参照してください。

### <a name="extending-msbuild-for-your-project-type"></a>プロジェクトの種類についての MSBuild の拡張
 MSBuild のインターフェイスと API は、将来のバージョンの [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] で変更される可能性があります。 そのため、マネージド パッケージ フレームワーク (MPF) クラスは変更からのシールドを提供するため、それらを使用することをお勧めします。

 プロジェクト用 Managed Package Framework (MPFProj) には、新しいプロジェクト システムを作成および管理するためのヘルパー クラスが用意されています。 ソース コードとコンパイルの手順については、[Visual Studio 2013 のプロジェクト用 MPF](https://github.com/tunnelvisionlabs/MPFProj10) に関する記事を参照してください。

 プロジェクト固有の MPF クラスは次のとおりです。

|クラス|実装|
|-----------|--------------------|
|`Microsoft.VisualStudio.Package.ProjectNode`|<xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3><br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgProvider2><br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IPersistFileFormat><br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents>|
|`Microsoft.VisualStudio.Package.ProjectFactory`|<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFactory>|
|`Microsoft.VisualStudio.Package.HierarchyNode`|<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy>|
|`Microsoft.VisualStudio.Package.ProjectConfig`|<xref:Microsoft.VisualStudio.Shell.Interop.IVsCfg><br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectCfg><br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildableProjectCfg><br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsDebuggableProjectCfg>|
|`Microsoft.VisualStudio.Package.SettingsPage`|<xref:Microsoft.VisualStudio.OLE.Interop.IPropertyPageSite>|

 `Microsoft.VisualStudio.Package.ProjectElement` クラスは、MSBuild 項目のラッパーです。

#### <a name="single-file-generators-vs-msbuild-tasks"></a>単一ファイル ジェネレーターと MSBuild タスク
 単一ファイル ジェネレーターには設計時しかアクセスできませんが、MSBuild タスクは設計時とビルド時に使用できます。 そのため、柔軟性を最大限に高めるために、コードを変換および生成するには MSBuild タスクを使用します。 詳細については、[カスタム ツール](../../extensibility/internals/custom-tools.md)に関するページを参照してください。

## <a name="see-also"></a>関連項目
- [MSBuild リファレンス](../../msbuild/msbuild-reference.md)
- [MSBuild](../../msbuild/msbuild.md)
- [カスタム ツール](../../extensibility/internals/custom-tools.md)
