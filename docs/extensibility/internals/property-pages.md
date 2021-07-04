---
title: プロパティ ページ | Microsoft Docs
description: Visual Studio SDK で新しいプロジェクトの種類のプロパティ ページを操作する方法について説明します。これにより、ユーザーはプロジェクトのプロパティを表示したり変更したりできます。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- configuration options, changing properties
- property pages
- property pages, changing configuration options
ms.assetid: b9b3e6e8-1e30-4c89-9862-330265dcf38c
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 88ebf99ef2361a232c4a5c4c02b9a140155d66e9
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2021
ms.locfileid: "112903412"
---
# <a name="property-pages"></a>[プロパティ ページ]
ユーザーは、プロパティ ページを使用して、プロジェクト構成に依存するプロパティや依存しないプロパティを表示したり変更したりすることができます。 **[プロパティ ページ]** ボタンは、選択されたオブジェクトのプロパティ ページ ビューを提供するオブジェクトに関する **[プロパティ]** ウィンドウまたはソリューション エクスプローラーのツールバーで有効になります。 プロパティ ページは環境によって作成され、ソリューションやプロジェクトに対して使用できます。 ただし、構成に依存するプロパティを使用するプロジェクト項目に対して使用可能にすることもできます。 この機能は、プロジェクト内のファイルを正しくビルドするにはさまざまなコンパイラ スイッチの設定が必要な場合に使用されることがあります。

## <a name="using-property-pages"></a>プロパティ ページの使用
 プロパティ ページが既に表示されていて、その選択が (たとえば、ソリューションからプロジェクトに) 変更された場合、そのページに表示される情報は新しい選択に関するプロパティを表示するように変更されます。 そのオブジェクトにプロパティ ページをサポートするプロパティが存在しない場合、プロパティ ページは空になります。

 複数のオブジェクトが選択されている場合、プロパティ ページには、選択されたすべての項目に関するプロパティの共通部分が表示されます。 選択された項目に構成に依存するプロパティが含まれていないときに、ソリューション エクスプローラーのツールバーの **[プロパティ ページ]** ボタンがクリックされた場合、フォーカスはプロパティ ウィンドウに変更されます。 プロパティ ウィンドウと選択に関連する詳細については、[プロパティの拡張](../../extensibility/internals/extending-properties.md)に関するページを参照してください。

 複数のオブジェクトに関するプロパティが表示されているときに、プロパティ ページの値を変更した場合は、それらのオブジェクトに関するすべての値が新しい値に設定されます。これらの値が最初は異なっていたり、個々のオブジェクトのプロパティが表示されたときにページが空白であったりした場合でも同じです。

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] で使用できる **[プロジェクト プロパティ ページ]** ダイアログ ボックスの一般的な種類には 2 つあります。 最初に (Visual Basic プロジェクトの場合など)、次のスクリーンショットに示すように、プロパティ ページがフィールド形式を使用して表示されます。 2 番目には (このセクションの後の方に示されています)、プロパティ ページがプロパティ ウィンドウにあるのと同様のプロパティ グリッドをホストします。

 ![Visual Basic プロパティ ページ](../../extensibility/internals/media/vsvbproppages.gif "vsVBPropPages") フィールド形式とツリー構造を備えた [プロジェクト プロパティ ページ] ダイアログ ボックス

 [プロパティ ページ] ダイアログ ボックスのツリー構造は、<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> を使用して構築されるわけではありません。 環境が、<xref:Microsoft.VisualStudio.OLE.Interop.ISpecifyPropertyPages> および <xref:Microsoft.VisualStudio.Shell.Interop.IVsPropertyPage> インターフェイスから渡されたレベル名に基づいて、これを構築します。

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] プロパティ ページで使用できる最上位レベルのカテゴリは次の 2 つだけです。

- [共通プロパティ] 選択された 1 つまたは複数のオブジェクトに関する、構成に依存しない情報が表示されます。 その結果、いずれかの [共通プロパティ] サブカテゴリが選択された場合、このダイアログ ボックスの上部にある [構成]、[プラットフォーム]、[構成マネージャー] オプションは使用できなくなります。

- [構成プロパティ] ソリューションまたはプロジェクトの [デバッグ]、[最適化]、[ビルド] パラメーターに関連した、構成に依存する情報が含まれています。

  最上位レベルのカテゴリを追加で作成することはできませんが、`IVsPropertyPage` の実装でどちらかが表示されないように選択することは可能です。 たとえば、あるオブジェクトに関して表示する、構成に依存しないプロパティが存在しない場合は、[共通プロパティ] カテゴリが表示されないように選択できます。 構成オブジェクト (`IVsCfg`、`IVsProjectCfg`、関連するインターフェイスを実装しているオブジェクト) で `ISpecifyPropertyPages` を実装するときに、`ISpecifyPropertyPages` が項目の参照オブジェクトと構成プロパティから実装されている場合は [共通プロパティ] を表示します。

  最上位レベルのカテゴリの下に表示されている各カテゴリは、個別のプロパティ ページを表します。 このダイアログ ボックスで使用できるカテゴリとサブカテゴリのエントリは、`ISpecifyPropertyPages` と `IVsPropertyPage` の実装によって決定されます。

  プロパティ ページにプロパティが表示されている選択コンテナー内の項目の `IDispatch` オブジェクトによって、クラス ID の一覧を列挙するための `ISpecifyPropertyPages` が実装されます。 これらのクラス ID は変数として `ISpecifyPropertyPages` に渡され、プロパティ ページをインスタンス化するために使用されます。 クラス ID の一覧は、このダイアログ ボックスの左側にあるツリー構造を作成するために `IVsPropertyPage` にも渡されます。 その後、プロパティ ページでは、`ISpecifyPropertyPages` を実装して各ページの情報を入力する `IDispatch` オブジェクトに情報を戻します。

  参照オブジェクトのプロパティは、選択コンテナー内の各オブジェクトの `IDispatch` を使用して取得されます。

  VSPackage で `Help::DisplayTopicFromF1Keyword` を実装すると、[ヘルプ] ボタンの機能が提供されます。

  詳細については、MSDN ライブラリの `IDispatch` と `ISpecifyPropertyPages` を参照してください。

  サンプルに表示される 2 番目の種類のプロパティ ページでは、次のスクリーンショットに示すように、プロパティ グリッドのフォームをホストします。

  ![VC プロパティ ページ](../../extensibility/internals/media/vsvcproppages.gif "vsVCPropPages") プロパティ グリッドを備えた [プロパティ ページ] ダイアログ ボックス

  インターフェイス `IVSMDPropertyBrowser` と `IVSMDPropertyGrid` (vsmanaged.h で宣言されています) は、ダイアログ ボックスまたはウィンドウ内にプロパティ グリッドを作成して設定するために使用されます。

  プロジェクトのアーキテクチャは、以前のバージョンの [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] から大幅に変更されています。 特に、どのプロジェクトがアクティブであるかの概念が変更されています。 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] には、アクティブなプロジェクトの概念はありません。 以前の開発環境では、アクティブなプロジェクトは、コンテキストに関係なく、ビルドおよび配置コマンドが既定で実行されるプロジェクトでした。 現在は、どのビルドおよび配置コマンドがどのプロジェクトに適用されるかをソリューションで制御および調整します。

  以前にアクティブなプロジェクトであったものは、現在、次の 3 つの異なる方法のいずれかでキャプチャされます。

- スタートアップ プロジェクト

   ソリューションのプロパティ ページから、ユーザーが F5 キーを押すか、または [ビルド] メニューから [実行] を選択したときに起動される 1 つまたは複数のプロジェクトを指定できます。 これは、その名前がソリューション エクスプローラーに太字のフォントで表示されるという意味で、以前のアクティブなプロジェクトと同様の方法で機能します。

   スタートアップ プロジェクトは、`DTE.Solution.SolutionBuild.StartupProjects` を呼び出すことによってオートメーション モデルのプロパティとして取得できます。 VSPackage では、<xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionBuildManager2.get_StartupProject%2A> または <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionBuildManager2.get_StartupProject%2A> メソッドを呼び出します。 `IVsSolutionBuildManager` は、SID_SVsSolutionBuildManager で `QueryService` によるサービスとして使用できます。 詳細については、「[プロジェクト構成オブジェクト](../../extensibility/internals/project-configuration-object.md)」および「[ソリューション構成](../../extensibility/internals/solution-configuration.md)」を参照してください。

- アクティブなソリューション ビルド構成

   [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] には、`DTE.Solution.SolutionBuild.ActiveConfiguration` を実装することによってオートメーション モデルで使用できるアクティブなソリューション構成があります。 ソリューション構成は、ソリューション内のプロジェクトごとに 1 つのプロジェクト構成を含むコレクションです (各プロジェクトには、複数のプラットフォーム上の、異なる名前を持つ、複数の構成を含めることができます)。 ソリューションのプロパティ ページに関連する詳細については、「[ソリューション構成](../../extensibility/internals/solution-configuration.md)」を参照してください。

- 現在選択されているプロジェクト

   選択されているプロジェクト階層と 1 つまたは複数のプロジェクト項目を取得するには、<xref:Microsoft.VisualStudio.Shell.Interop.IVsMonitorSelection.GetCurrentSelection%2A> メソッドを実装します。 DTE からは、`SelectedItems.SelectedItem.Project` および `SelectedItems.SelectedItem.ProjectItem` メソッドを使用します。 コアの [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ドキュメントでは、これらの見出しの下にサンプル コードがあります。

## <a name="see-also"></a>関連項目
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsPropertyPage>
- [構成オプションの管理](../../extensibility/internals/managing-configuration-options.md)
- [プロジェクト構成オブジェクト](../../extensibility/internals/project-configuration-object.md)
- [ソリューション構成](../../extensibility/internals/solution-configuration.md)
