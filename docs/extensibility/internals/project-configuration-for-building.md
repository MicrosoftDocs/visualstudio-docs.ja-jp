---
title: ビルドのためのプロジェクト構成 |Microsoft Docs
description: 新しいプロジェクト タイプの [ソリューション構成] ダイアログ ボックスで、特定のソリューションのソリューション構成のリストを管理する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- projects [Visual Studio SDK], configuration for building
- project configurations, building
ms.assetid: 2c83615d-fa4d-4b9f-b315-7a69b3000da0
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: b817607f765626a6b63693e681306309512fdb7d
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105074445"
---
# <a name="project-configuration-for-building"></a>ビルドのためのプロジェクト構成
特定のソリューションのソリューション構成のリストは、[ソリューション構成] ダイアログ ボックスで管理されます。

 ユーザーは、それぞれが独自の一意の名前を持つ追加のソリューション構成を作成できます。 ユーザーが新しいソリューション構成を作成すると、IDE の既定値はプロジェクト内の対応する構成名になり、対応する名前が存在しない場合は Debug になります。 ユーザーは、必要に応じて、特定の要件を満たすように選択項目を変更することができます。 この動作の唯一の例外は、プロジェクトで新しいソリューション構成の名前と一致する構成がサポートされている場合です。 たとえば、ソリューションに Project1 と Project2 が含まれているとします。 Project1 には、Debug、Retail、および MyConfig1 というプロジェクト構成があります。 Project2 には、Debug、Retail、および MyConfig2 というプロジェクト構成があります。

 ユーザーが MyConfig2 という名前の新しいソリューション構成を作成した場合、Project1 ではその Debug 構成が既定でソリューション構成にバインドされます。 また、Project2 では、その MyConfig2 構成が既定でソリューション構成にバインドされます。

> [!NOTE]
> バインドでは大文字と小文字は区別されません。

 ユーザーが構成ドロップダウン リストで **[複数選択]** 項目を選択すると、環境に使用可能な構成の一覧を示すダイアログ ボックスが表示されます。

 ![[複数の構成]](../../extensibility/internals/media/vsmultiplecfgs.gif "vsMultipleCfgs") 複数の構成

 このダイアログ ボックスでは、ユーザーは 1 つまたは複数の構成を選択できます。 選択すると、[プロパティ ページ] ダイアログ ボックスに表示されるプロパティ値に、選択した構成の値の共通部分が反映されます。

 ソリューションとプロジェクトの構成の追加と名前変更に関する詳細については、「[ソリューション構成](../../extensibility/internals/solution-configuration.md)」を参照してください。

 プロジェクトの依存関係とビルドの順序は、ソリューション構成に依存しません。つまり、ソリューション内のすべてのプロジェクトに対して 1 つの依存関係ツリーしか設定できません。 ソリューションまたはプロジェクトを右クリックし、 **[プロジェクトの依存関係]** または **[プロジェクトのビルド順序]** のいずれかのオプションを選択すると、 **[プロジェクトの依存関係]** ダイアログ ボックスが開きます。 これは **[プロジェクト]** メニューから開くこともできます。

 ![[プロジェクトの依存関係]](../../extensibility/internals/media/vsprojdependencies.gif "vsProjDependencies") プロジェクトの依存関係

 プロジェクトの依存関係によって、プロジェクトのビルド順序が決まります。 ソリューション内のプロジェクトがビルドされる正確な順序を確認するには、ダイアログ ボックスの [ビルド順序] タブを使用し、ビルド順序を変更するには [依存関係] タブを使用します。

> [!NOTE]
> リスト内のチェック ボックスがオンになっていても、淡色表示になっているプロジェクトは、<xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildDependency> または <xref:Microsoft.VisualStudio.Shell.Interop.IVsDeployDependency> インターフェイスによって指定された明示的な依存関係があるために環境によって追加されており、変更することはできません。 たとえば、プロジェクト参照を [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)] プロジェクトから別のプロジェクトに追加すると、参照を削除することによってのみ削除できるビルド依存関係が自動的に追加されます。 チェック ボックスがオフで淡色表示になっているプロジェクトは選択できません。そうすると、依存関係のループ (たとえば、Project1 が Project2 に依存し、Project2 が Project1 に依存するなど) が作成され、ビルドが停止するためです。

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ビルド プロセスには、1 つのビルド コマンドで呼び出される一般的なコンパイルとリンクの操作が含まれます。 他にも 2 つのビルド プロセスがサポートされています。前回のビルドからのすべての出力項目を削除するためのクリーン操作と、構成内の出力項目が変更されたかどうかを確認するための最新状態チェックです。

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectCfg2> オブジェクトは、ビルド プロセスを管理するために対応する <xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildableProjectCfg> (<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectCfg2.get_CfgType%2A> から返されます) を返します。 実行中のビルド操作の状態を報告するために、構成により、<xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildStatusCallback> (環境およびビルドの状態イベントに関係するその他のオブジェクトによって実装されたインターフェイス) が呼び出されます。

 ビルドが完了すると、構成設定を使用して、デバッガーの制御下で実行できるかどうかを判断できます。 構成により、デバッグをサポートするために <xref:Microsoft.VisualStudio.Shell.Interop.IVsDebuggableProjectCfg> が実装されます。

 プロジェクトの依存関係を実装した後は、オートメーション モデルを使用して依存関係をプログラムで操作できます。 オートメーション モデルで <xref:EnvDTE.SolutionBuild.BuildDependencies%2A> を呼び出します。 ソリューション ビルド マネージャーの構成とそのプロパティを直接操作できる、使用可能な VSIP API レベルのインターフェイスはありません。

 また、[プロジェクトの依存関係] ウィンドウにグリッドを表示することもできます。 詳細については、「[プロパティ表示グリッド](../../extensibility/internals/properties-display-grid.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [構成オプションの管理](../../extensibility/internals/managing-configuration-options.md)
- [展開の管理のためのプロジェクト構成](../../extensibility/internals/project-configuration-for-managing-deployment.md)
- [出力のためのプロジェクト構成](../../extensibility/internals/project-configuration-for-output.md)
