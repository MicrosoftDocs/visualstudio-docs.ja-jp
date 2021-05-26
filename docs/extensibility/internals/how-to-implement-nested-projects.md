---
title: '方法: 入れ子になったプロジェクトの実装 |Microsoft Docs'
description: Visual Studio で入れ子になったプロジェクトを実装する方法について説明します。それには、ソリューションおよび親プロジェクトからイベントを発生させて、プロジェクト階層を構築します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- nested projects, implementing
- projects [Visual Studio SDK], nesting
ms.assetid: d20b8d6a-f0e0-4115-b3a3-edda893ae678
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 49f2e3b971c16b63f900424aa99649e424490d30
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105078865"
---
# <a name="how-to-implement-nested-projects"></a>方法: 入れ子になったプロジェクトの実装

入れ子になったプロジェクト タイプを作成する場合、追加の手順をいくつか実装する必要があります。 親プロジェクトは、ソリューションがその入れ子になった (子) プロジェクトに対して担うものと同じ役割を一部担います。 親プロジェクトは、ソリューションに似た、プロジェクトのコンテナーです。 特に、入れ子になったプロジェクトの階層を構築するために、ソリューションおよび親プロジェクトからいくつかのイベントを発生させる必要があります。 これらのイベントについては、入れ子になったプロジェクトを作成する次のプロセスで説明します。

## <a name="create-nested-projects"></a>入れ子になったプロジェクトの作成

1. 統合開発環境 (IDE) では、<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFactory> インターフェイスが呼び出されて、親プロジェクトのプロジェクト ファイルとスタートアップ情報が読み込まれます。 親 プロジェクトが作成され、ソリューションに追加されます。

    > [!NOTE]
    > 子プロジェクトを作成する前に親プロジェクトを作成する必要があるため、プロセスのこの時点では、親プロジェクトで入れ子になったプロジェクトを作成するのは早すぎます。 このシーケンスに従うことで、親プロジェクトでは設定を子プロジェクトに適用でき、子プロジェクトでは必要に応じて親プロジェクトから情報を取得できます。 このシーケンスは、ソースコード管理 (SCC) や **ソリューション エクスプローラー** などのクライアントによってそれが必要とされる場合を対象としています。

     親プロジェクトでは、IDE によって <xref:Microsoft.VisualStudio.Shell.Interop.IVsParentProject.OpenChildren%2A> メソッドが呼び出されてから、入れ子になった (子) プロジェクト (複数可) を作成する必要があります。

2. IDE では、親プロジェクトで <xref:Microsoft.VisualStudio.Shell.Interop.IVsParentProject> に対して `QueryInterface` が呼び出されます。 この呼び出しが成功した場合、IDE では親の <xref:Microsoft.VisualStudio.Shell.Interop.IVsParentProject.OpenChildren%2A> メソッドが呼び出され、親プロジェクトの入れ子になったプロジェクトがすべて開きます。

3. 親プロジェクトでは <xref:Microsoft.VisualStudio.Shell.Interop.IVsFireSolutionEvents.FireOnBeforeOpeningChildren%2A> メソッドが呼び出されて、入れ子になったプロジェクトが作成されようとしていることがリスナーに通知されます。 たとえば、SCC ではこれらのイベントがリッスンされ、ソリューションとプロジェクトの作成プロセスの手順が順番に実行されているかどうかが確認されます。 手順の順序が正しくない場合、ソリューションはソース コード管理に正しく登録されない可能性があります。

4. 親プロジェクトでは、それぞれの子プロジェクトで <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution.AddVirtualProject%2A> メソッドまたは <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution.AddVirtualProjectEx%2A> メソッドが呼び出されます。

     <xref:Microsoft.VisualStudio.Shell.Interop.__VSADDVPFLAGS> を `AddVirtualProject` メソッドに渡し、仮想 (入れ子になった) プロジェクトのプロジェクト ウィンドウへの追加、ビルドからの除外、ソースコード管理への追加などが必要であることを示します。 `VSADDVPFLAGS` では、入れ子になったプロジェクトの表示を制御し、関連付ける機能を示すことができます。

     プロジェクト GUID が親プロジェクトのプロジェクト ファイルに格納されている既存の子プロジェクトを再読み込みすると、親プロジェクトによって `AddVirtualProjectEx` が呼び出されます。 `AddVirtualProject` と `AddVirtualProjectEX` の唯一の違いは、`AddVirtualProjectEX` には、親プロジェクトを有効化してインスタンスごとに `guidProjectID` を指定するためのパラメーターがあるという点です。このため、子プロジェクトでは <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution.GetProjectOfGuid%2A> と <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution.GetProjectOfProjref%2A> を正しく機能するように有効化できます。

     入れ子になったプロジェクトを新しく追加するときなど、使用可能な GUID がない場合、ソリューションでは、プロジェクトが親に追加されたときに、それ専用のものが作成されます。 そのプロジェクトの GUID をプロジェクト ファイルに保持するのは、親プロジェクトの役割です。 入れ子になったプロジェクトを削除する場合、そのプロジェクトの GUID も削除することができます。

5. IDE では、親プロジェクトのそれぞれの子プロジェクトで <xref:Microsoft.VisualStudio.Shell.Interop.IVsParentProject.OpenChildren> メソッドが呼び出されます。

     プロジェクトを入れ子にする場合は、親プロジェクトで `IVsParentProject` を実装する必要があります。 ただし、下に親プロジェクトがある場合でも、親プロジェクトでは `IVsParentProject` に対して `QueryInterface` が呼び出されることはありません。 ソリューションでは、`IVsParentProject` への呼び出しが処理され、実装されている場合には `OpenChildren` が呼び出されて、入れ子になったプロジェクトが作成されます。 `AddVirtualProjectEX` は常に `OpenChildren` から呼び出されます。 階層作成イベントの順番を保つため、これは親プロジェクトから呼び出さないでください。

6. IDE では、<xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents3.OnAfterOpenProject%2A> メソッドは子プロジェクトで呼び出されます。

7. 親プロジェクトでは、<xref:Microsoft.VisualStudio.Shell.Interop.IVsFireSolutionEvents.FireOnAfterOpeningChildren%2A> メソッドが呼び出されて、親の子プロジェクトが作成されたことがリスナーに通知されます。

8. IDE では、すべての子プロジェクトが開いた後に、<xref:Microsoft.VisualStudio.Shell.Interop.IVsFireSolutionEvents.FireOnAfterOpenProject%2A> メソッドが親プロジェクトで呼び出されます。

     存在しない場合、親プロジェクトでは `CoCreateGuid` が呼び出されて、入れ子になった各プロジェクトの GUID が作成されます。

    > [!NOTE]
    > `CoCreateGuid` は、GUID の作成時に呼び出される COM API です。 詳細については、MSDN ライブラリの `CoCreateGuid` と GUID を参照してください。

     親プロジェクトでは、この GUID がプロジェクト ファイルに保存され、IDE で次にこれを開いたときに取得されます。 `AddVirtualProjectEX` を呼び出して子プロジェクトの `guidProjectID` を取得する際の詳細情報については、手順 4 を参照してください。

9. 次に、慣例では入れ子になったプロジェクトに委譲する親 ItemID に対して <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.GetProperty%2A> メソッドが呼び出されます。 親で <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.GetProperty%2A> が呼び出されるときに、委譲先のプロジェクトを入れ子にするノードのプロパティが取得されます。

     親と子の各プロジェクトはプログラムによってインスタンス化されるため、この時点で入れ子になったプロジェクトのプロパティを設定できます。

    > [!NOTE]
    > 入れ子になったプロジェクトからコンテキスト情報を受け取るだけでなく、[__VSHPROPID.VSHPROPID_UserContext](<xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID.VSHPROPID_UserContext>) をチェックすることによって、親プロジェクトにその項目のコンテキストがあるかどうかも確認できます。 このようにして、入れ子になった個々のプロジェクトに固有の動的なヘルプ属性とメニュー オプションをさらに追加できます。

10. 階層は、<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.GetNestedHierarchy%2A> メソッドを呼び出すことによって **ソリューション エクスプローラー** に表示されるように構築されます。

     `GetNestedHierarchy` を使用して階層を環境に渡し、ソリューション エクスプローラーに表示する階層を構築します。 このようにして、プロジェクトが存在し、ビルド マネージャーで構築するためにそれを管理できること、またはプロジェクト内のファイルをソース コード管理下に配置できることがソリューションにおいて認識されます。

11. Project1 の入れ子になったプロジェクトがすべて作成されると、コントロールがソリューションに戻され、Project2 でもそのプロセスが繰り返されます。

     入れ子になったプロジェクトを作成するこのプロセスと同じプロセスが、子を持つ子プロジェクトについても実行されます。 このとき、Project1 の子である BuildProject1 に子プロジェクトがある場合は、BuildProject1 の後、Project2 の前に作成されます。 プロセスは再帰的で、階層は上から順に構築されます。

     ユーザーがソリューションまたは特定のプロジェクト自体を閉じたために入れ子になったプロジェクトが閉じた場合、`IVsParentProject` のもう 1 つのメソッドである <xref:Microsoft.VisualStudio.Shell.Interop.IVsParentProject.CloseChildren%2A> が呼び出されます。 親プロジェクトでは、<xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution.RemoveVirtualProject%2A> メソッドへの呼び出しが <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents3.OnBeforeClosingChildren%2A> と <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents3.OnAfterClosingChildren%2A> の各メソッドでラップされ、入れ子になったプロジェクトが閉じられていることがソリューション イベントのリスナーに通知されます。

次のトピックでは、入れ子になったプロジェクトを実装する際に考慮する必要があるいくつかの概念について説明します。

- [入れ子になったプロジェクトのアンロードと再ロードに関する考慮事項](../../extensibility/internals/considerations-for-unloading-and-reloading-nested-projects.md)
- [入れ子になったプロジェクト向けのウィザード サポート](../../extensibility/internals/wizard-support-for-nested-projects.md)
- [入れ子になったプロジェクト向けのコマンド処理の実装](../../extensibility/internals/implementing-command-handling-for-nested-projects.md)に関するページ
- [入れ子になったプロジェクトの [AddItem] ダイアログ ボックスをフィルター処理する](../../extensibility/internals/filtering-the-additem-dialog-box-for-nested-projects.md)

## <a name="see-also"></a>関連項目

- [[新しい項目の追加] ダイアログ ボックスへの項目の追加](../../extensibility/internals/adding-items-to-the-add-new-item-dialog-boxes.md)
- [プロジェクトと項目テンプレートの登録](../../extensibility/internals/registering-project-and-item-templates.md)
- [チェックリスト: 新しいプロジェクト タイプの作成](../../extensibility/internals/checklist-creating-new-project-types.md)
- [コンテキスト パラメーター](../../extensibility/internals/context-parameters.md)
- [ウィザード (.Vsz) ファイル](../../extensibility/internals/wizard-dot-vsz-file.md)
