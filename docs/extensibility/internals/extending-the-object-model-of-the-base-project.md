---
title: ベース プロジェクトのオブジェクト モデルの拡張 | Microsoft Docs
description: プロジェクトのサブタイプを使用して、Visual Studio で基本プロジェクトのオートメーション オブジェクト モデルを拡張する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 03/22/2018
ms.topic: conceptual
helpviewer_keywords:
- automation object model, extending
- project subtypes, extending automation object model
- automation object model
ms.assetid: 2f95cc53-dff6-476c-bacd-500fb0ff7725
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 7f220d1e0c97647162c621bc565147bc74f40103
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105069622"
---
# <a name="extend-the-object-model-of-the-base-project"></a>ベース プロジェクトのオブジェクト モデルの拡張

プロジェクトのサブタイプでは、基本プロジェクトのオートメーション オブジェクト モデルを次の場所で拡張することができます。

- Project.Extender("\<ProjectSubtypeName>"): プロジェクトのサブタイプで、<xref:EnvDTE.Project> オブジェクトのカスタム メソッドを持つオブジェクトを提供できます。 プロジェクトのサブタイプでは、オートメーション エクステンダーを使用して `Project` オブジェクトを公開できます。 メイン プロジェクトのサブタイプ アグリゲーターに実装された <xref:EnvDTE80.IInternalExtenderProvider> インターフェイスでは、([VSITEMID.Root](<xref:Microsoft.VisualStudio.VSConstants.VSITEMID.Root>) の `itemid` 値に対応する) <xref:Microsoft.VisualStudio.Shell.Interop.__VSSPROPID2> の CATID から `VSHPROPID_ExtObjectCATID` のオブジェクトを提供する必要があります。

- ProjectItem.Extender("\<ProjectSubtypeName>"): プロジェクトのサブタイプで、プロジェクト内の特定の <xref:EnvDTE.ProjectItem> オブジェクトのカスタム メソッドを持つオブジェクトを提供できます。 プロジェクトのサブタイプでは、オートメーション エクステンダーを使用してこのオブジェクトを公開できます。 メイン プロジェクトのサブタイプ アグリゲーターに実装された <xref:EnvDTE80.IInternalExtenderProvider> インターフェイスでは、(希望の <xref:Microsoft.VisualStudio.VSConstants.VSITEMID> に対応する) <xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID2> の CATID から `VSHPROPID_ExtObjectCATID` のオブジェクトを提供する必要があります。

- Project.Properties: このコレクションでは、`Project` オブジェクトの構成非依存のプロパティを公開します。 `Project` プロパティについて詳しくは、「<xref:EnvDTE.Project.Properties%2A>」をご覧ください。 プロジェクトのサブタイプでは、オートメーション エクステンダーを使用して、そのプロパティをこのコレクションに追加できます。 メイン プロジェクトのサブタイプ アグリゲーターに実装された <xref:EnvDTE80.IInternalExtenderProvider> インターフェイスでは、([VSITEMID.Root](<xref:Microsoft.VisualStudio.VSConstants.VSITEMID.Root>) の `itemid` 値に対応する) <xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID2> の CATID から `VSHPROPID_BrowseObjectCATID` のオブジェクトを提供する必要があります。

- Configuration.Properties: このコレクションでは、特定の構成 (たとえば、デバッグ) のためのプロジェクトの構成依存のプロパティを公開します。 詳細については、「<xref:EnvDTE.Configuration>」を参照してください。 プロジェクトのサブタイプでは、オートメーション エクステンダーを使用して、そのプロパティをこのコレクションに追加できます。 メイン プロジェクトのサブタイプ アグリゲーターに実装された <xref:EnvDTE80.IInternalExtenderProvider> インターフェイスでは、([VSITEMID.Root](<xref:Microsoft.VisualStudio.VSConstants.VSITEMID.Root>) の `itemid` 値に対応する) `VSHPROPID_CfgBrowseObjectCATID` のオブジェクトを提供します。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgBrowseObject> インターフェイスは、構成参照オブジェクトを別のものと区別するために使用されます。

## <a name="see-also"></a>関連項目

- <xref:Microsoft.VisualStudio.Shell.Interop.__VSFPROPID>
