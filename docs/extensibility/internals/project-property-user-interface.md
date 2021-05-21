---
title: プロジェクトのプロパティのユーザー インターフェイス | Microsoft Docs
description: プロジェクト サブタイプで、ベース プロジェクトに用意されているプロジェクトの [プロパティ ページ] ダイアログ ボックスを変更する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 03/22/2018
ms.topic: conceptual
helpviewer_keywords:
- project properties [Visual Studio], user interface
- projects [Visual Studio SDK], properties UI
- project properties UI
ms.assetid: b6aec634-8533-476c-9ebd-36536a2288e2
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 051c373b85eff4483012dec5b264fa09fe7d962e
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105064476"
---
# <a name="project-property-user-interface"></a>プロジェクト プロパティのユーザー インターフェイス

プロジェクト サブタイプで、プロジェクトの **[プロパティ ページ]** ダイアログ ボックスにある項目を、ベース プロジェクトに用意されているものをそのまま使用することができます。また、コントロールやページ全体をそのまま読み取り専用または非表示にしたり、 **[プロパティ ページ]** ダイアログ ボックスにプロジェクト サブタイプ固有のページを追加したりできます。

## <a name="extending-the-project-property-dialog-box"></a>[プロジェクトのプロパティ] ダイアログ ボックスを拡張する

プロジェクト サブタイプで、オートメーション エクステンダーとプロジェクト構成参照オブジェクトが実装されます。 これらのエクステンダーには、特定のプロパティを非表示または読み取り専用にするための <xref:EnvDTE.IFilterProperties> インターフェイスが実装されています。 ベース プロジェクトによって実装されたベース プロジェクトの **[プロパティ ページ]** ダイアログ ボックスでは、オートメーション エクステンダーによって実行されるフィルター処理が優先されます。

**[プロジェクトのプロパティ]** ダイアログ ボックスを拡張するプロセスを以下に示します。

- ベース プロジェクトで <xref:EnvDTE80.IInternalExtenderProvider> インターフェイスを実装することにより、プロジェクト サブタイプからエクステンダーを取得します。 ベース プロジェクトの参照、プロジェクト オートメーション、プロジェクト構成参照オブジェクトには、このインターフェイスが実装されます。

- プロジェクト参照オブジェクトおよびプロジェクト オートメーション オブジェクトでの <xref:EnvDTE80.IInternalExtenderProvider> の実装は、プロジェクト サブタイプ アグリゲーターの <xref:EnvDTE80.IInternalExtenderProvider> 実装に委任されます (つまり、<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> プロジェクト オブジェクトに対し <xref:EnvDTE80.IInternalExtenderProvider> の `QueryInterface` を呼び出します)。

- ベース プロジェクト構成参照オブジェクトには、プロジェクト サブタイプ構成オブジェクトからオートメーション エクステンダーに直接接続するための <xref:EnvDTE80.IInternalExtenderProvider> も実装されます。 その実装は、プロジェクト サブタイプ アグリゲーターで実装される <xref:EnvDTE80.IInternalExtenderProvider> インターフェイスに委任されます。

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgBrowseObject.GetProjectItem%2A> は、プロジェクト構成参照オブジェクトによって実装され、<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> オブジェクトが返されます。

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgBrowseObject.GetCfg%2A> も、プロジェクト構成参照オブジェクトによって実装され、<xref:Microsoft.VisualStudio.Shell.Interop.IVsCfg> オブジェクトが返されます。

- プロジェクト サブタイプで、次の <xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID2> の値の取得により、実行時にベース プロジェクトのさまざまな拡張可能オブジェクトに適切な CATID を確認できます。

  - <xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID2.VSHPROPID_ExtObjectCATID>

  - <xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID2.VSHPROPID_BrowseObjectCATID>

  - <xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID2.VSHPROPID_CfgBrowseObjectCATID>

プロジェクト スコープの CATID を確認するために、プロジェクト サブタイプで `VSITEMID typedef` から [VSITEMID.Root](<xref:Microsoft.VisualStudio.VSConstants.VSITEMID#Microsoft_VisualStudio_VSConstants_VSITEMID_Root>) の上記のプロパティを取得します。 プロジェクト サブタイプには、構成に依存するものと依存しないものの両方について、プロジェクトに対して表示される **[プロパティ ページ]** ダイアログ ボックスのページを制御する必要がある場合もあります。 一部のプロジェクト サブタイプには、組み込みのページを削除し、プロジェクト サブタイプに固有のページを追加する必要がある場合があります。 これを可能にするために、マネージド クライアント プロジェクトから、次のプロパティの <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.GetProperty%2A> メソッドを呼び出します。

- `VSHPROPID_PropertyPagesCLSIDList` - 構成に依存しないプロパティ ページの CLSID をセミコロンで区切った一覧。

- `VSHPROPID_CfgPropertyPagesCLSIDList —` 構成に依存するプロパティ ページの CLSID をセミコロンで区切った一覧。

プロジェクト サブタイプによって <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> オブジェクトが集約されるため、これらのプロパティの定義をオーバーライドして、どの **[プロパティ ページ]** ダイアログ ボックスを表示するかを制御できます。 プロジェクト サブタイプで、これらのプロパティを内部のベース プロジェクトから取得し、必要に応じて CLSID を追加または削除できます。

プロジェクト サブタイプによって追加された新しいプロパティ ページには、ベース プロジェクトの実装からプロジェクト構成参照オブジェクトが渡されます。 このプロジェクト構成参照オブジェクトは、オートメーション エクステンダーをサポートします。 オートメーション エクステンダーの詳細については、「[オートメーション エクステンダーの実装と使用](/previous-versions/0y92k2w2(v=vs.140))」を参照してください。 プロジェクト サブタイプによって実装されるプロパティ ページは、<xref:EnvDTE.Project.Extender%2A> を呼び出して、ベース プロジェクト構成参照オブジェクトを拡張する独自のプロジェクト サブタイプ構成参照オブジェクトを取得します。

## <a name="see-also"></a>こちらもご覧ください

- <xref:EnvDTE.IFilterProperties>
- [[プロパティ ページ] ダイアログ ボックス](/previous-versions/visualstudio/visual-studio-2010/as5chysf(v=vs.100))