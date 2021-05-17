---
title: コマンド ルーティング アルゴリズム |Microsoft Docs
description: コマンドはさまざまなコンポーネントによって処理され、最も内側から最も外側のコンテキストにルーティングされるため、Visual Studio でのコマンドの解決順序について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- commands, routing
- command routing
ms.assetid: 998b616b-bd08-45cb-845f-808efb8c33bc
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 0e02493cbb2f872806ade33d77609d45d1938ccd
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105057313"
---
# <a name="command-routing-algorithm"></a>コマンド ルーティング アルゴリズム
Visual Studio のコマンドは、さまざまなコンポーネントによって処理されます。 コマンドは、現在の選択内容に基づいて最も内側のコンテキストから最も外側のコンテキスト (グローバルとも呼ばれます) にルーティングされます。 詳細については、「[コマンドの可用性](../../extensibility/internals/command-availability.md)」をご覧ください。

## <a name="order-of-command-resolution"></a>コマンドの解決順序
 コマンドは、次のレベルのコマンド コンテキストを通じて渡されます。

1. アドイン: 環境では、まず、存在するすべてのアドインに対してコマンドが提供されます。

2. 優先順位コマンド: これらのコマンドは、<xref:Microsoft.VisualStudio.Shell.Interop.IVsRegisterPriorityCommandTarget> を使用して登録されます。 これらは、Visual Studio のすべてのコマンドに対して呼び出され、登録された順序で呼び出されます。

3. コンテキスト メニュー コマンド: コンテキスト メニューに配置されたコマンドは、まずはコンテキスト メニューに用意されているコマンド ターゲット、その後は通常のルーティングに提供されます。

4. ツール バーのコマンド ターゲットの設定: これらのコマンド ターゲットは、<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell4.SetupToolbar2%2A> を呼び出すと登録されます。 `pCmdTarget` パラメーターは、`null` に設定できます。 `null` でない場合は、このコマンド ターゲットを使用して、設定しているツール バーにあるすべてのコマンドが更新されます。 シェルでツール バーが設定されている場合は、ウィンドウ フレームが `pCmdTarget` として渡されます。これにより、ツール バーのコマンドに対するすべての更新が、フォーカスされていない場合でも、ウィンドウ フレームを通過します。

5. ツール ウィンドウ: 通常、<xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowPane> インターフェイスを実装するツール ウィンドウは、ツール ウィンドウがアクティブなウィンドウの場合に Visual Studio がコマンド ターゲットを取得できるように、<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> インターフェイスも実装する必要があります。 ただし、フォーカスのあるツール ウィンドウが **プロジェクト** ウィンドウである場合は、選択された項目の共通の親である <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy> インターフェイスにコマンドがルーティングされます。 この選択範囲が複数のプロジェクトにまたがる場合、コマンドは <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution> 階層にルーティングされます。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy> インターフェイスには、<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> インターフェイスの対応するコマンドに似た <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy.QueryStatusCommand%2A> と <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy.ExecCommand%2A> メソッドが含まれています。

6. ドキュメント ウィンドウ: コマンドの *.vsct* ファイルに `RouteToDocs` フラグが設定されている場合、Visual Studio ではドキュメント ビュー オブジェクトでコマンド ターゲットが検索されます。これは、<xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowPane> インターフェイスのインスタンスか、ドキュメント オブジェクトのインスタンス (通常は <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLines> インターフェイスまたは <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBuffer> インターフェイス) です。 ドキュメント ビュー オブジェクトがコマンドをサポートしていない場合、Visual Studio により、返された <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> インターフェイスにコマンドがルーティングされます。 (これは、ドキュメント データ オブジェクトの省略可能なインターフェイスです)。

7. 現在の階層: 現在の階層は、アクティブなドキュメント ウィンドウを所有するプロジェクトまたは **ソリューション エクスプローラー** で選択されている階層にすることができます。 Visual Studio により、現在の、またはアクティブな階層に実装されている <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> インターフェイスが検索されます。 階層では、プロジェクト項目のドキュメント ウィンドウにフォーカスがある場合でも、階層がアクティブなときは常に有効なコマンドをサポートする必要があります。 ただし、**ソリューション エクスプローラー** にフォーカスがある場合にのみ適用されるコマンドは、<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy> インターフェイスとその <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy.QueryStatusCommand%2A> と <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy.ExecCommand%2A> メソッドを使用してサポートする必要があります。

     **Cut**、**Copy**、**Paste**、**Delete**、**Rename**、**Enter**、**DoubleClick** の各コマンドでは、特別な処理が必要です。 階層内の **Delete** および **Remove** コマンドを処理する方法の詳細については、<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchyDeleteHandler> インターフェイスを参照してください。

8. グローバル: コマンドが前に説明したコンテキストによって処理されていない場合、Visual Studio により、<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> インターフェイスを実装するコマンドを所有する VSPackage へのルーティングが試みられます。 VSPackage がまだ読み込まれていない場合は、Visual Studio により <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A> メソッドが呼び出されたときに読み込まれません。 VSPackage は、<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.Exec%2A> メソッドが呼び出されたときにのみ読み込まれます。

## <a name="see-also"></a>関連項目
- [コマンド デザイン](../../extensibility/internals/command-design.md)
