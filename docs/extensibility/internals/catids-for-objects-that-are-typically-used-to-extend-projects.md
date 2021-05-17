---
title: プロジェクトの拡張に通常使用されるオブジェクトの CATID
description: Visual Basic、Visual C#、Visual C++ プロジェクトの Project および ProjectItem オートメーション オブジェクトを拡張するために使用されるオブジェクトの CATID について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- VSPackages, CATIDs
- GUIDs, VSPackages
- CATIDs for VSPackages
ms.assetid: 0c7fdb66-ed96-4b36-89f6-021bca573572
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 276e7f146858c2de166c0ba20063a0bf4d8b88a0
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105086093"
---
# <a name="catids-for-objects-that-are-typically-used-to-extend-projects"></a>プロジェクトの拡張に通常使用されるオブジェクトの CATID
次の表は、[!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)]、[!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)]、[!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)] の各プロジェクトの `Project` および `ProjectItem` オートメーション オブジェクトを拡張するために使用される CATID の一覧を示しています。 これらの CATID は、*VSLangProj.olb* に定義されています。

## <a name="listing-of-catids"></a>CATID の一覧

|名前|GUID|
|----------|----------|
|<xref:VSLangProj.PrjCATID.prjCATIDProject>|{610D4614-D0D5-11D2-8599-006097C68E81}|
|<xref:VSLangProj.PrjCATID.prjCATIDProjectItem>|{610D4615-D0D5-11D2-8599-006097C68E81}|

## <a name="visual-basic-catids"></a>Visual Basic の CATID
 次の表は、[!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)] の参照オブジェクトを拡張するために使用される CATID の一覧を示しています。 これらはすべて、*VSLangProj.olb* に定義されています。

|名前|GUID|
|----------|----------|
|<xref:VSLangProj.PrjBrowseObjectCATID.prjCATIDVBProjectBrowseObject>|{E0FDC879-C32A-4751-A3D3-0B3824BD575F}|
|<xref:VSLangProj.PrjBrowseObjectCATID.prjCATIDVBProjectConfigBrowseObject>|{67F8DD11-14EB-489b-87F0-F01C52AF3870}|
|<xref:VSLangProj.PrjBrowseObjectCATID.prjCATIDVBFileBrowseObject>|{EA5BD05D-3C72-40A5-95A0-28A2773311CA}|
|<xref:VSLangProj.PrjBrowseObjectCATID.prjCATIDVBFolderBrowseObject>|{932DC619-2EAA-4192-B7E6-3D15AD31DF49}|
|<xref:VSLangProj.PrjBrowseObjectCATID.prjCATIDVBReferenceBrowseObject>|{2289B812-8191-4e81-B7B3-174045AB0CB5}|

## <a name="visual-c-catids"></a>Visual C# の CATID
 次の CATID は、[!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)] の参照オブジェクトを拡張するために使用できます。 これらはすべて、*VSLangProj.olb* に定義されています。

|名前|GUID|
|----------|----------|
|<xref:VSLangProj.PrjBrowseObjectCATID.prjCATIDCSharpProjectBrowseObject>|{4EF9F003-DE95-4d60-96B0-212979F2A857}|
|<xref:VSLangProj.PrjBrowseObjectCATID.prjCATIDCSharpProjectConfigBrowseObject>|{A12CE10A-227F-4963-ADB6-3A43388513CA}|
|<xref:VSLangProj.PrjBrowseObjectCATID.prjCATIDCSharpFileBrowseObject>|{8D58E6AF-ED4E-48B0-8C7B-C74EF0735451}|
|<xref:VSLangProj.PrjBrowseObjectCATID.prjCATIDCSharpFolderBrowseObject>|{914FE278-054A-45DB-BF9E-5F22484CC84C}|
|<xref:VSLangProj.PrjBrowseObjectCATID.prjCATIDCSharpReferenceBrowseObject>|{2F0FA3B8-C855-4a4e-95A5-CB45C67D6C27}|

## <a name="c-catids"></a>C++ の CATID
 次の [!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)] プロジェクト システムの CATID は、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] .NET 2003 のタイプ ライブラリに公開されません。これらのプロジェクト オブジェクトを拡張する場合は、コードに含める必要があります。 これらの CATID は、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] の今後のリリースでタイプ ライブラリに含められます。

|名前|GUID|
|----------|----------|
|`CVCProjectNode`|{EE8299CB-19B6-4f20-ABEA-E1FD9A33B683}|
|`CVCFolderNode`|{EE8299CA-19B6-4f20-ABEA-E1FD9A33B683}|
|`CVCFileNode`|{EE8299C9-19B6-4f20-ABEA-E1FD9A33B683}|

 次のコード例は、コードでこれらの CATID をプログラミングする方法を示しています。

```
const LPOLESTR CVCProjectNode::s_wszCATID = L"{EE8299CB-19B6-4f20-ABEA-E1FD9A33B683}";
const LPOLESTR CVCFolderNode::s_wszCATID = L"{EE8299CA-19B6-4f20-ABEA-E1FD9A33B683}";
const LPOLESTR CVCFileNode::s_wszCATID = L"{EE8299C9-19B6-4f20-ABEA-E1FD9A33B683}";
```

 次の [!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)] プロジェクト システムの CATID も、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] .NET 2003 のタイプ ライブラリに公開されません。これらのプロジェクト オブジェクトを拡張する場合は、コードに含める必要があります。 これらの CATID は [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] .NET 2003 でのみ使用でき、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] の今後のリリースでは使用できません。

|名前|GUID|
|----------|----------|
|`CVCAssemblyReferenceNode`|{FE8299C9-19B6-4f20-ABEA-E1FD9A33B683}|
|`CVCProjectReferenceNode`|{593DCFCE-20A7-48e4-ACA1-49ADE9049887}|
|`CVCActiveXReferenceNode`|{9E8182D3-C60A-44f4-A74B-14C90EF9CACE}|
|`CVCReferences`|{FE8299CA-19B6-4f20-ABEA-E1FD9A33B683}|

 次のコード例は、コードでこれらの CATID をプログラミングする方法を示しています。

```
const LPOLESTR CVCAssemblyReferenceNode::s_wszCATID = L"{FE8299C9-19B6-4f20-ABEA-E1FD9A33B683}";
const LPOLESTR CVCProjectReferenceNode::s_wszCATID = L"{593DCFCE-20A7-48e4-ACA1-49ADE9049887}";
const LPOLESTR CVCActiveXReferenceNode::s_wszCATID = L"{9E8182D3-C60A-44f4-A74B-14C90EF9CACE}";
const LPOLESTR CVCReferences::s_wszCATID = L"{FE8299CA-19B6-4f20-ABEA-E1FD9A33B683}";
```

 次の表は、[!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)] および [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)] のプロジェクトの種類の GUID を示しています。

| プロジェクトの種類 | GUID |
| - | - |
| [!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)] | {FAE04EC0-301F-11D3-BF4B-00C04F79EFBC} |
| [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)] | {F184B08F-C81C-45F6-A57F-5ABD9991F28F} |

## <a name="see-also"></a>関連項目
- [プロジェクト テンプレートとプロジェクト項目テンプレートの追加](../../extensibility/internals/adding-project-and-project-item-templates.md)
- [プロジェクトと項目テンプレートの登録](../../extensibility/internals/registering-project-and-item-templates.md)
