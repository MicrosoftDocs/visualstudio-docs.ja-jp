---
title: MSBuild の使用 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- VSPackages, compiling with MSBuild
- MSBuild, extensibility
- packages, compiling with MSBuild
ms.assetid: 9d38c388-1f64-430e-8f6c-e88bc99a4260
caps.latest.revision: 21
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: a1ad59e6d8f4cb88004629b0dfd2cdf0631a7824
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2019
ms.locfileid: "74297672"
---
# <a name="using-msbuild"></a>MSBuild の使用
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

MSBuild supplies a well-defined, extensible XML format for creating project files that fully describe project items to be built, build tasks, and build configurations.  
  
 For an end-to-end sample of a language project system based on MSBuild, see the IronPython Sample Deep Dive in the[VSSDK Samples](../../misc/vssdk-samples.md).  
  
## <a name="general-msbuild-considerations"></a>General MSBuild Considerations  
 MSBuild project files, for example, [!INCLUDE[csprcs](../../includes/csprcs-md.md)] .csproj and [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] .vbproj files, contain data that is used at build time, but also can contain data that is used at design time. Build-time data is stored using MSBuild primitives, including [Item Element (MSBuild)](../../msbuild/item-element-msbuild.md) and [Property Element (MSBuild)](../../msbuild/property-element-msbuild.md). Design-time data, which is data specific to the project type and any related project subtypes, is stored in free-form XML reserved for it.  
  
 MSBuild does not have native support for configuration objects, but does provide conditional attributes for specifying configuration-specific data. (例:  
  
```  
<OutputDir Condition="'$(Configuration)'=="release'">Bin\MyReleaseConfig</OutputDir>  
```  
  
 For more information on conditional attributes, see [Conditional Constructs](../../msbuild/msbuild-conditional-constructs.md).  
  
### <a name="extending-msbuild-for-your-project-type"></a>Extending MSBuild for Your Project Type  
 MSBuild interfaces and APIs are subject to change in future versions of [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]. Therefore, it is prudent to use the managed package framework (MPF) classes because they provide shielding from changes.  
  
 The Managed Package Framework for Projects (MPFProj) provides helper classes for creating and managing new project system. You can find the source code and compilation instructions at [MPF for Projects - Visual Studio 2013](https://archive.codeplex.com/?p=mpfproj12).  
  
 The project-specific MPF classes are as follows:  
  
|インスタンス|実装|  
|-----------|--------------------|  
|`Microsoft.VisualStudio.Package.ProjectNode`|<xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3><br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgProvider2><br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IPersistFileFormat><br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents>|  
|`Microsoft.VisualStudio.Package.ProjectFactory`|<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFactory>|  
|`Microsoft.VisualStudio.Package.HierarchyNode`|<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy>|  
|`Microsoft.VisualStudio.Package.ProjectConfig`|<xref:Microsoft.VisualStudio.Shell.Interop.IVsCfg><br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectCfg><br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildableProjectCfg><br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsDebuggableProjectCfg>|  
|`Microsoft.VisualStudio.Package.SettingsPage`|<xref:Microsoft.VisualStudio.OLE.Interop.IPropertyPageSite>|  
  
 `Microsoft.VisualStudio.Package.ProjectElement` class is a wrapper for MSBuild items.  
  
#### <a name="single-file-generators-vs-msbuild-tasks"></a>Single File Generators vs. MSBuild Tasks  
 Single file generators are accessible at design-time only, but MSBuild tasks can be used at design-time and build-time. For maximum flexibility, therefore, use MSBuild tasks to transform and generate code. For more information, see [Custom Tools](../../extensibility/internals/custom-tools.md).  
  
## <a name="see-also"></a>参照  
 [MSBuild リファレンス](../../msbuild/msbuild-reference.md)   
 [MSBuild](https://msdn.microsoft.com/7c49aba1-ee6c-47d8-9de1-6f29a906e20b)   
 [カスタム ツール](../../extensibility/internals/custom-tools.md)
