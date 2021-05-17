---
title: VSPackage のオートメーションの提供 | Microsoft Docs
description: VSPackage 固有のオブジェクトと標準オートメーション オブジェクトを実装することによって VSPackage のオートメーションを提供する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- VSPackages, automation [Visual Studio SDK]
- automation [Visual Studio SDK], VSPackages
ms.assetid: 104c4c55-78b8-42f4-b6b0-9a334101aaea
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 1f9a19b5e0e543052dad492ab319595c8ef76dfe
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105060953"
---
# <a name="providing-automation-for-vspackages"></a>VSPackage でのオートメーションの提供
VSPackage のオートメーションを提供するには、VSPackage 固有のオブジェクトを実装する方法と、標準オートメーション オブジェクトを実装する方法の 2 つがあります。 一般に、環境のオートメーション モデルを拡張するために、これらは一緒に使用されます。

## <a name="vspackage-specific-objects"></a>VSPackage 固有のオブジェクト
 オートメーション モデル内の特定の場所では、VSPackage 固有のオートメーション オブジェクトを提供する必要があります。 たとえば、新しいプロジェクトには、その VSPackage でしか提供されない個別のオブジェクトが必要です。 これらのオブジェクトの名前はレジストリに入力され、環境の `DTE` オブジェクトの呼び出しを使用して取得されます。

 VSPackage 固有のオブジェクトはまた、オートメーション コンシューマーが、標準オブジェクトの Object プロパティによって提供されるオブジェクトを使用するときにも取得できます。 たとえば、標準の `Window` オブジェクトには、一般には `Windows.Object` プロパティとして知られる `Object` プロパティがあります。 VSPackage で実装されたウィンドウでコンシューマーが `Window.Object` を呼び出した場合は、独自の設計の特定のオートメーション オブジェクトを戻します。

#### <a name="projects"></a>プロジェクト
 VSPackage では、独自の VSPackage 固有のオブジェクトを通して、新しいプロジェクトの種類のオートメーション モデルを拡張できます。 VSPackage の新しいオートメーション オブジェクトを提供する主な目的は、固有のプロジェクト オブジェクトを <xref:Microsoft.VisualStudio.VCProjectEngine.VCProject> または <xref:VSLangProj80.VSProject2> オブジェクトと区別することです。 この区別は、いくつかのプロジェクトの種類がソリューションで並べて表示されている場合に、あるプロジェクトの種類を他から切り離して選択したり、反復処理したりする方法を提供したいときに便利です。 詳細については、[プロジェクト オブジェクトの公開](../../extensibility/internals/exposing-project-objects.md)に関するページを参照してください。

#### <a name="events"></a>イベント
 環境のイベント アーキテクチャは、独自の VSPackage 固有のオブジェクトを追加するための別の場所を提供します。 たとえば、独自の固有のイベント オブジェクトを作成することによって、プロジェクトのための環境のイベント モデルを拡張できます。 独自のプロジェクトの種類に新しい項目が追加されたときに独自のイベントを提供することもできます。 詳細については、[イベントの公開](../../extensibility/internals/exposing-events-in-the-visual-studio-sdk.md)に関するページを参照してください。

#### <a name="window-objects"></a>ウィンドウ オブジェクト
 ウィンドウは、呼び出されたときに、環境に VSPackage 固有のオートメーション オブジェクトを戻すことができます。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsExtensibleObject>、<xref:EnvDTE.IExtensibleObject>、またはプロパティを戻す `IDispatch` から派生したオブジェクトを実装することにより、そのオブジェクトが配置されているウィンドウ オブジェクトを拡張します。 たとえば、このアプローチを使用すると、ウィンドウ フレームに配置されているコントロールのオートメーションを提供できます。 このオブジェクトや、拡張される可能性があるその他のすべてのオブジェクトのセマンティクスはユーザーが設計します。 詳細については、[方法: ウィンドウのオートメーションの提供](../../extensibility/internals/how-to-provide-automation-for-windows.md)に関するページを参照してください。

#### <a name="options-pages-on-the-tools-menu"></a>[ツール] メニュー上のオプション ページ
 ページを実装し、独自のオプションを作成するための情報をレジストリに追加することによって、[ツール]、[オプション] オートメーション モデルを拡張するためのページを作成できます。 その後、他のすべてのオプション ページと同様に、環境オブジェクト モデルからこのページを呼び出すことができます。 VSPackage から環境に追加している機能の設計にオプション ページが必要な場合は、オートメーションのサポートも追加する必要があります。 詳細については、「[オプション ページのオートメーションのサポート](../../extensibility/internals/automation-support-for-options-pages.md)」を参照してください。

## <a name="standard-automation-objects"></a>標準オートメーション オブジェクト
 プロジェクトのオートメーションを拡張するには、他のプロジェクト オブジェクトの横にあり、標準のメソッドとプロパティを実装している (`IDispatch` から派生した) 標準オートメーション オブジェクトも実装します。 標準オブジェクトの例には、ソリューション階層に挿入されるプロジェクト オブジェクト (`Projects`、`Project`、`ProjectItem`、`ProjectItems` など) が含まれます。 新しいプロジェクトの種類ではすべて、これらのオブジェクトを (さらに、可能性としてプロジェクトのセマンティクスによっては他のオブジェクトも) 実装する必要があります。

 ある意味では、これらのオブジェクトは VSPackage 固有のプロジェクト オブジェクトの反対の利点を提供します。 標準オートメーション オブジェクトを使用すると、同じオブジェクトをサポートしている他のすべてのプロジェクトと同様の汎用的な方法でプロジェクトを使用できます。 そのため、一般的な `Project` および `ProjectItem` オブジェクトに対して記述されたアドインは、任意の種類のプロジェクトに対して機能できます。 詳細については、「[プロジェクトのモデリング](../../extensibility/internals/project-modeling.md)」を参照してください。
