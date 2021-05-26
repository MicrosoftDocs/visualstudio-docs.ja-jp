---
title: 'チェック リスト: 新しいプロジェクト タイプの作成 | Microsoft Docs'
description: Visual Studio で新しいプロジェクト タイプを作成して表示するために実行する必要があるタスクについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- projects [Visual Studio SDK], creating new types
- project types, checklist for creating
ms.assetid: 29eb9c3b-1933-4741-aa85-65a33f0825ba
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: ac6495a6c2d5edcde00a3eb002f2fc41211a27e3
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105074770"
---
# <a name="checklist-create-new-project-types"></a>チェック リスト: 新しいプロジェクト タイプの作成
新しいプロジェクト タイプを作成するには、いくつかのタスクを実行する必要があります。 次のチェックリストに、それらのタスクのガイドを示します。

1. 新しいプロジェクト タイプの機能をデザインします。 詳細については、「[プロジェクト タイプのデザインの方針](../../extensibility/internals/project-type-design-decisions.md)」を参照してください。

2. コードおよびその他のプロジェクト要素に使用されるエディターを決定します。 コア エディターまたは標準エディターを使用することも、プロジェクト固有のエディターを作成して使用することもできます。 詳細については、「[カスタム エディターとデザイナーを作成する](../../extensibility/creating-custom-editors-and-designers.md)」および「[方法: プロジェクト固有のエディターを開く](../../extensibility/how-to-open-project-specific-editors.md)」を参照してください。

3. **クラス ビュー** と **オブジェクト ブラウザー** で使用するプロジェクト項目の参加のレベルを決定します。 詳細については、「[シンボル参照ツールのサポート](../../extensibility/internals/supporting-symbol-browsing-tools.md)」を参照してください。

4. プロジェクトおよびプロジェクト項目に対して以前に行った設計上の決定事項に基づいて、新しいクラスを派生させます。

5. 次のプロジェクト タイプのコンポーネントのコードを記述します。

    - プロジェクト ファクトリ。新しいプロジェクトの作成と既存のプロジェクトの開始を管理します。 詳細については、「[プロジェクト ファクトリを使用したプロジェクト インスタンスの作成](../../extensibility/internals/creating-project-instances-by-using-project-factories.md)」を参照してください。

    - プロジェクト階層とコマンド処理。 詳細については、「[HierUtil7 プロジェクト クラスを使用したプロジェクト タイプの実装 (C++)](/previous-versions/bb166212(v=vs.100))」、「[プロジェクト モデルの要素](../../extensibility/internals/elements-of-a-project-model.md)」、「[プロジェクト モデルのコア コンポーネント](../../extensibility/internals/project-model-core-components.md)」、および「[MenuCommands と OleMenuCommands](/previous-versions/visualstudio/visual-studio-2015/misc/menucommands-vs-olemenucommands?preserve-view=true&view=vs-2015)」を参照してください。

    - プロジェクト項目の管理。 **[新しいプロジェクト]** ダイアログ ボックスへのプロジェクトの追加が含まれます。 詳細については、「[プロジェクトおよびプロジェクト項目テンプレートの追加](../../extensibility/internals/adding-project-and-project-item-templates.md)」および「[プロジェクトと項目テンプレートの登録](../../extensibility/internals/registering-project-and-item-templates.md)」を参照してください。

    - プロジェクトの状態と個々の項目の永続性。 詳細については、「[プロジェクト項目のオープンと保存](../../extensibility/internals/opening-and-saving-project-items.md)」を参照してください。 ソリューション情報の永続性については、[ソリューション](../../extensibility/internals/solutions-overview.md)に関するページを参照してください。

    - プロパティ ウィンドウに表示する構成に依存しないプロパティ。 詳細については、「[プロパティの拡張](../../extensibility/internals/extending-properties.md)」を参照してください。

    - 構成に依存するプロパティを表示するプロパティ ページに実装されている、プロジェクト構成プロパティ。 詳細については、「[構成オプションの管理](../../extensibility/internals/managing-configuration-options.md)」を参照してください。

    - デプロイの出力の列挙。 詳細については、「[出力のためのプロジェクト構成](../../extensibility/internals/project-configuration-for-output.md)」を参照してください。

    - プロジェクト スタートアップ サービス。 詳細については、「[プロジェクト モデルの要素](../../extensibility/internals/elements-of-a-project-model.md)」および「[プロジェクト モデルのコア コンポーネント](../../extensibility/internals/project-model-core-components.md)」を参照してください。

    - オートメーションに使用できるオブジェクト、または `IDispatch` から派生したクラス。

    - XML コマンド テーブル ( *.vsct*) ファイル。 詳細については、「[Visual Studio コマンド テーブル (.vsct) ファイル](../../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)」を参照してください。

6. プロジェクト タイプをテスト、デバッグ、および開始します。

7. `VSHPROPID_ShowProjInSolutionPage` の値として、`VARIANT_TRUE` を設定して、 **[参照の追加]** ダイアログ ボックスの **[プロジェクト]** タブにプロジェクトを表示します。 詳細については、次のトピックを参照してください。 <xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID> および <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.GetProperty%2A>

8. VSPackage をインストールするための Microsoft インストーラー ( *.msi*) ファイルを作成します。 詳細については、「[Windows インストーラーによる VSPackage のインストール](../../extensibility/internals/installing-vspackages-with-windows-installer.md)」、「[プロジェクト タイプの登録](../../extensibility/internals/registering-a-project-type.md)」、および「[VSPackage](../../extensibility/internals/vspackages.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [Visual Studio での階層](../../extensibility/internals/hierarchies-in-visual-studio.md)
- [プロジェクト タイプを作成する状況](../../extensibility/internals/when-to-create-project-types.md)
- [プロジェクト タイプの作成](../../extensibility/internals/creating-project-types.md)