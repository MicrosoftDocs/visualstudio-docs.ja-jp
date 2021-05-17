---
title: 入れ子になったプロジェクトのコマンド処理の実装 | Microsoft Docs
description: Visual Studio 統合開発環境 (IDE) で入れ子になったプロジェクトのコマンド処理を実装する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- nested projects, implementing command handling
ms.assetid: 48a9d66e-d51c-4376-a95a-15796643a9f2
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: fad154fd3739369b0ccf7e5d896d1b9f1728c68e
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105085781"
---
# <a name="implementing-command-handling-for-nested-projects"></a>入れ子になったプロジェクト向けのコマンド処理の実装
IDE では、<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy> および <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> インターフェイスを介して渡されたコマンドを入れ子になったプロジェクトに渡すことができます。または、親プロジェクトでコマンドをフィルター処理またはオーバーライドできます。

> [!NOTE]
> 通常、親プロジェクトによって処理されるコマンドのみをフィルター処理できます。 IDE によって処理される **Build** や **Deploy** などのコマンドは、フィルター処理できません。

 次の手順では、コマンド処理を実装するプロセスについて説明します。

## <a name="procedures"></a>手順

#### <a name="to-implement-command-handling"></a>コマンド処理を実装するには

1. 入れ子になったプロジェクトまたは入れ子になったプロジェクト内のノードをユーザーが選択すると、次のようになります。

   1. IDE によって <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A> メソッドが呼び出されます。

      または

   2. ソリューション エクスプローラーのショートカット メニュー コマンドなどの階層ウィンドウでコマンドが生成された場合、IDE によってプロジェクトの親の <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy.QueryStatusCommand%2A> メソッドが呼び出されます。

2. 親プロジェクトでは、`QueryStatus` に渡されるパラメーター (`pguidCmdGroup` や `prgCmds` など) を調べて、コマンドをフィルター処理する必要があるかどうかを判断できます。 コマンドをフィルター処理するように親プロジェクトを実装する場合は、次のように設定する必要があります。

   ```
   prgCmds[0].cmdf = OLECMDF_SUPPORTED;
   // make sure it is disabled
   prgCmds[0].cmdf &= ~MSOCMDF_ENABLED;
   ```

    その場合、親プロジェクトから `S_OK` が返されます。

    親プロジェクトでコマンドをフィルター処理しない場合は、単に `S_OK` が返されます。 この場合は、IDE によってコマンドが子プロジェクトに自動的にルーティングされます。

    親プロジェクトで、コマンドを子プロジェクトにルーティングする必要はありません。 このタスクは IDE によって実行されます。

## <a name="see-also"></a>関連項目
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy>
- [コマンド、メニュー、およびツール バー](../../extensibility/internals/commands-menus-and-toolbars.md)
- [入れ子になったプロジェクト](../../extensibility/internals/nesting-projects.md)
