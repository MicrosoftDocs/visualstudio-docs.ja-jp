---
title: プロパティ表示グリッド | Microsoft Docs
description: プロパティ ウィンドウのグリッド内のどこにプロパティ名とプロパティ値のフィールドがあるか、またプロパティの拡張でグリッドをどのように操作するかについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- properties [Visual Studio SDK], grid
ms.assetid: 318e41b0-acf5-4842-b85e-421c9d5927c5
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: ee3d7d8d6277f9cfa0352cb4961644e4860b46bb
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2021
ms.locfileid: "112899655"
---
# <a name="properties-display-grid"></a>プロパティ表示グリッド

**[プロパティ]** ウィンドウでは、グリッド内にフィールドが表示されます。 左の列にはプロパティ名が含まれ、右の列にはプロパティ値が含まれています。

## <a name="work-with-the-grid"></a>グリッドを操作する

2 列の一覧には、デザイン時に変更することができる、構成に依存しないプロパティとその現在の設定が表示されます。 すべてのプロパティは表示されていない可能性があることに注意してください。 たとえば、<xref:Microsoft.VisualStudio.Shell.Interop.IVsPerPropertyBrowsing.HideProperty%2A> メソッドを実装することによって、プロパティを非表示として設定できます。 具体的には、子プロパティを持つプロパティを非表示にするには、次のようにします。

1. <xref:Microsoft.VisualStudio.Shell.Interop.IVsPerPropertyBrowsing.DisplayChildProperties%2A> の `pfDisplay` パラメーターを `FALSE` に設定します。

2. <xref:Microsoft.VisualStudio.Shell.Interop.IVsPerPropertyBrowsing.HideProperty%2A> の `pfHide` パラメーターを `TRUE` に設定します。

**[プロパティ]** ウィンドウに情報をプッシュするために、IDE では <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer> を使用します。 <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer> は、 **[プロパティ]** ウィンドウに表示される関連プロパティを持つ選択可能なオブジェクトが含まれているウィンドウごとに VSPackage によって呼び出されます。 **ソリューション エクスプローラー** の実装の <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer> では、階層内の参照可能なオブジェクトを取得するために、プロジェクト階層内の [__VSHPROPID.VSHPROPID_BrowseObject](<xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID.VSHPROPID_BrowseObject>) を使用して `GetProperty` を呼び出します。

VSPackage で [__VSHPROPID.VSHPROPID_BrowseObject](<xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID.VSHPROPID_BrowseObject>) がサポートされていない場合、IDE では、1 つまたは複数の階層項目によって提供される [__VSHPROPID.VSHPROPID_SelContainer](<xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID.VSHPROPID_SelContainer>) の値を使用して <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.GetProperty%2A> を使用しようとします。

プロジェクト VSPackage で <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer> を作成する必要はありません。それを実装している、IDE によって提供されるウィンドウ パッケージ (**ソリューション エクスプローラー** など) が、代わりに <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer> を構築するためです。

<xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer> は、IDE によって呼び出される次の 3 つのメソッドで構成されています。

- <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer.CountObjects%2A> には、 **[プロパティ]** ウィンドウに表示されるように選択されているオブジェクトの数が含まれています。

- <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer.GetObjects%2A> は、 **[プロパティ]** ウィンドウに表示されるように選択されている `IDispatch` オブジェクトを返します。

- <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer.SelectObjects%2A> は、<xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer.GetObjects%2A> によって返される任意のオブジェクトをユーザーが選択できるようにします。 これにより、UI でユーザーに表示される選択項目を VSPackage で視覚的に更新できるようになります。

**[プロパティ]** ウィンドウでは、参照されるプロパティを取得するために `IDispatch` オブジェクトから情報を抽出します。 [プロパティ] ブラウザーでは、`IDispatch` を使用して (`IDispatch::GetTypeInfo` から取得される) `ITypeInfo` をクエリすることによって、そのオブジェクトにどのようなプロパティをサポートしているかをたずねます。 このブラウザーでは次に、これらの値を使用して **[プロパティ]** ウィンドウを設定したり、グリッドに表示される個々のプロパティの値を変更したりします。 これらのプロパティ情報は、そのオブジェクト自体の中に保持されます。

返されたオブジェクトは `IDispatch` をサポートしているため、呼び出し元は、目的の情報を表す定義済みのディスパッチ識別子 (DISPID) を指定して `IDispatch::Invoke` または `ITypeInfo::Invoke` を呼び出すことによって、そのオブジェクトの名前などの情報を取得できます。 宣言される DISPID は、ユーザー定義の識別子と競合しないように負の値になっています。

**[プロパティ]** ウィンドウには、選択されたオブジェクトの特定のプロパティの属性に応じて、さまざまな種類のフィールドが表示されます。 これらのフィールドには、編集ボックス、ドロップダウン リストのほか、カスタム エディター ダイアログ ボックスへのリンクが含まれます。

- 列挙された一覧に含まれている値は、`IDispatch` への <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer.GetObjects%2A> クエリによって取得されます。 列挙された一覧から取得された値は、フィールド名をダブルクリックするか、またはその値をクリックし、ドロップダウン リストから新しい値を選択することによってプロパティ グリッドで変更できます。 列挙された一覧にある定義済みの設定を持つプロパティの場合は、[プロパティ] 一覧のプロパティ名をダブルクリックすると、使用可能な選択肢が順番に切り替わります。 2 つの選択肢 (true/false など) しかない定義済みのプロパティの場合は、プロパティ名をダブルクリックして、これらの選択肢を切り替えます。

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsPerPropertyBrowsing.HasDefaultValue%2A> が `false` である場合 (この値が変更されたことを示します) は、値が太字で表示されます。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPerPropertyBrowsing.CanResetPropertyValue%2A> は、この値を元の値にリセットできるかどうかを判定するために使用されます。 その場合は、その値を右クリックし、表示されるメニューから **[リセット]** を選択することによって元の既定値に変更できます。 そうでない場合は、その値を手動で元の既定値に変更する必要があります。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPerPropertyBrowsing> では、デザイン時に表示されるプロパティの名前をローカライズしたり、非表示にしたりすることもできますが、実行時に表示されるプロパティ名には影響を与えません。

- 省略記号 (...) ボタンをクリックすると、ユーザーが選択できるプロパティ値の一覧 (カラー ピッカーやフォントの一覧など) が表示されます。 これらの値は <xref:Microsoft.VisualStudio.Shell.Interop.IProvidePropertyBuilder> によって提供されます。

## <a name="see-also"></a>関連項目

- [プロパティを拡張する](../../extensibility/internals/extending-properties.md)
