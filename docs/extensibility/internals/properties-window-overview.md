---
title: プロパティ ウィンドウの概要 | Microsoft Docs
description: この概要では、Visual Studio IDE でプロパティ ウィンドウを操作するために使用されるインターフェイスについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- Properties window
ms.assetid: 289ed4f2-02ac-4899-855e-42dfe57ee05f
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: e0b775cbc96303f53bcd795b2121d10af83714e6
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2021
ms.locfileid: "112899668"
---
# <a name="properties-window-overview"></a>プロパティ ウィンドウの概要
**[プロパティ]** ウィンドウは、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 統合開発環境 (IDE) で使用できる 2 つの主な種類のウィンドウで選択されたオブジェクトに関するプロパティを表示するために使用されます。 これらの 2 種類のウィンドウは次のとおりです。

- ソリューション エクスプローラー、クラス ビュー、オブジェクト ブラウザーなどのツール ウィンドウ

- フォーム デザイナー、XML エディター、HTML エディターなどのエディターやデザイナーを含むドキュメント ウィンドウ

## <a name="using-the-properties-window"></a>プロパティ ウィンドウの使用
 **[プロパティ]** ウィンドウには、選択された 1 つまたは複数の項目のプロパティが表示されます。 複数の項目が選択されている場合は、選択されたすべてのオブジェクトに関するすべてのプロパティの共通部分が表示されます。

 COM+ メタデータを使用しているフォーム デザイン ウィンドウまたは HTML エディター内の選択されたオブジェクトに関連したイベントは、 **[プロパティ]** ウィンドウに表示されます。 たとえば、あるボタンを選択し、そのボタンにリンクできるそれに関連付けられたイベント (`OnClick` イベントなど) を表示することができます。

 **[プロパティ]** ウィンドウに表示されるイベントは主に、コードにバインドされているオブジェクトで使用されます。 コードとは関係のないファイル形式を編集している場合、イベントは発生しません。 イベントが **[プロパティ]** ウィンドウに表示されるのは、実行中のコードと、特定のオブジェクトに関連付けられた特定のイベントの間にバインドが存在する場合だけです。 この例として、選択されたオブジェクトがアクティブ化されたときに実行される、そのオブジェクトの背後にあるコードが考えられます。

 次の表は、 **[プロパティ]** ウィンドウによって使用される主なインターフェイスの一覧を示しています。

|Interface Name|説明|
|--------------------|-----------------|
|<xref:Microsoft.VisualStudio.Shell.Interop.ICategorizeProperties>|**[プロパティ]** ウィンドウにカテゴリの一覧を提供し、各プロパティをカテゴリにマップします。|
|[IDispatch インターフェイス](/previous-versions/windows/desktop/api/oaidl/nn-oaidl-idispatch)|オートメーションをサポートするプログラミング ツールやその他のアプリケーションにオブジェクトのメソッドとプロパティを公開します。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IProvidePropertyBuilder>|オブジェクト自体によって実装されたモーダル ダイアログ ウィンドウを開く "*ビルダー*" と呼ばれる省略記号 (...) ボタンを提供します。 ユーザーがテキスト フィールドに簡単に値を入力できない場合に使用されます。 たとえば、RGB 値を自動的に決定するカラー ピッカーを開くために使用されることがあります。|
|<xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer>|**[プロパティ]** ウィンドウに表示される情報を更新するために使用されるオブジェクトへのアクセスを提供します。 <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer> は、表示される関連プロパティを持つ選択可能なオブジェクトが含まれているウィンドウごとに VSPackage によって実装されます。|
|<xref:Microsoft.VisualStudio.OLE.Interop.ITypeInfo>|インターフェイスのメソッドや構造体のフィールドなどのオブジェクトの種類に関する情報を提供します。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsMonitorSelection>|VSPackage で選択イベントの通知を受信したり、現在のプロジェクト階層、項目、要素の値、コマンド UI コンテキストに関する情報を取得したりできるようにします。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsMultiItemSelect>|複数選択にアクセスできる環境を提供します。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsPerPropertyBrowsing>|**[プロパティ]** ウィンドウに表示される一部のプロパティでローカライズされた名前を提供するために使用されます。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsSelectionEvents>|登録されている VSPackage に現在の選択、要素の値、またはコマンド UI コンテキストの変更を通知します。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackSelectionEx>|環境に現在の選択の変更を通知し、新しい選択に関連した階層と項目に関する情報へのアクセスを提供します。|

 `IDispatch` の詳細については、MSDN ライブラリを参照してください。

## <a name="see-also"></a>関連項目
- [プロパティの拡張](../../extensibility/internals/extending-properties.md)
- [プロパティ ウィンドウのフィールドとインターフェイス](../../extensibility/internals/properties-window-fields-and-interfaces.md)
