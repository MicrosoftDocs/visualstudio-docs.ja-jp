---
title: 入れ子になったプロジェクトのアンロードと再読み込み
description: Visual Studio で入れ子になったプロジェクトをアンロードおよび再読み込みするときに実行する必要がある追加の手順について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- nested projects, unloading and reloading
- projects [Visual Studio SDK], unloading and reloading nested
ms.assetid: 06c3427e-c874-45b1-b9af-f68610ed016c
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 9852454d487ab2a7ee08218c9712aa0afc1467ad
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105057072"
---
# <a name="considerations-for-unloading-and-reloading-nested-projects"></a>入れ子になったプロジェクトのアンロードと再ロードに関する考慮事項

入れ子になったプロジェクト タイプを実装する場合は、プロジェクトをアンロードして再読み込みするときに、追加の手順を実行する必要があります。 リスナーにソリューション イベントを正しく通知するには、`OnBeforeUnloadProject` と `OnAfterLoadProject` イベントを正しく発生させる必要があります。

これらのイベントを発生させる理由の 1 つは、ソース コード管理 (SCC) 用です。 SCC からの `Get` 操作がある場合は、SCC によるサーバーからの項目削除の後に、*新規* としての再追加は望ましくありません。 その場合は、新しいファイルが SCC から読み込まれます。 ファイルが異なっている場合は、すべてのファイルをアンロードして再読み込みする必要があります。

ソース コード管理により `ReloadItem` が呼びだれます。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFireSolutionEvents> インターフェイスを実装して、`OnBeforeUnloadProject` と `OnAfterLoadProject` を呼び出し、プロジェクトの削除と再作成をします。 この方法でインターフェイスを実装すると、SCC には、プロジェクトが一時的に削除され、再び追加されたことが通知されます。 そのため、SCC は、*実際* にプロジェクトが削除され、再追加されたかのように、プロジェクトに対して動作しません。

## <a name="reload-projects"></a>プロジェクトの再読み込み

入れ子になったプロジェクトの再読み込みをサポートするには、<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem2.ReloadItem%2A> メソッドを実装します。 `ReloadItem` の実装では、入れ子になったプロジェクトを閉じてから再作成します。

通常、プロジェクトが再読み込みされると、IDE によって <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents3.OnBeforeUnloadProject%2A> と <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents3.OnAfterLoadProject%2A> イベントが発生します。 ただし、削除、再読み込みされた入れ子になったプロジェクトの場合、IDE ではなく親プロジェクトによってプロセスが開始されます。 親プロジェクトはソリューション イベントを発生させず、IDE にはプロセスの初期化に関する情報がないため、イベントは発生しません。

このプロセスを処理するために、親プロジェクトにより `QueryInterface` インターフェイスで <xref:Microsoft.VisualStudio.Shell.Interop.IVsFireSolutionEvents> が呼び出されます。 `IVsFireSolutionEvents` には、`OnBeforeUnloadProject` イベントを発生させて入れ子になったプロジェクトをアンロードし、`OnAfterLoadProject` イベントを発生させて同じプロジェクトを再読み込みするように IDE に指示する機能があります。

## <a name="see-also"></a>関連項目

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents3>
- [プロジェクトを入れ子にする](../../extensibility/internals/nesting-projects.md)
