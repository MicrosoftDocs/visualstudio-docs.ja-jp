---
title: ドキュメント ウィンドウ | Microsoft Docs
description: Visual Studio のドキュメント ウィンドウについて説明します。これには、ドキュメント ウィンドウの実装方法と実行中のドキュメント テーブル (RDT) の状態を追跡する方法が含まれます。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Visual Studio SDK, document windows
ms.assetid: 50081d48-987f-43db-8bf9-51b7cf76e9c0
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 79706c98e98be55e69aaeeed7320c8b13bfd2a9c
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105061278"
---
# <a name="document-windows"></a>ドキュメント ウィンドウ
Visual Studio の "*ドキュメント ウィンドウ*" は、マルチドキュメント インターフェイス (MDI) ウィンドウに関連付けられているフレーム化された子ウィンドウです。 通常、ドキュメント ウィンドウはソース コードまたはテキストを表示および変更するために使用されますが、それらによって他の機能の種類をホストすることもできます。 ドキュメント ウィンドウ:

- 親 MDI の中で別個の水平または垂直タブ グループに整理して、複数のファイルを同時に表示できます。

- 親 MDI の中で任意の順序でドッキングできます。

- 自由にフローティングできます。

- タブの順序で他の MDI ウィンドウにリンクされています。

  グループ化、ドッキング、フローティングのコマンドは、ドキュメント ウィンドウ タブのショートカット メニューにあります。

  Visual Studio でのウィンドウの動作の詳細については、「[ウィンドウ レイアウトをカスタマイズする](../../ide/customizing-window-layouts-in-visual-studio.md)」を参照してください。

## <a name="document-window-implementation"></a>ドキュメント ウィンドウの実装
 ドキュメント ウィンドウは、エディターを実装すると作成されます。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory> インターフェイスで、エディターのインスタンス化の一部としてドキュメント ウィンドウが作成されます。 詳細については、「[エディターのレガシ インターフェイス](/previous-versions/visualstudio/visual-studio-2015/extensibility/legacy-interfaces-in-the-editor?preserve-view=true&view=vs-2015)」を参照してください。

> [!NOTE]
> ウィンドウに前方と後方のナビゲーション ポイントを提供するには、<xref:Microsoft.VisualStudio.Shell.Interop.IVsBackForwardNavigation> インターフェイスを実装します。 テキスト エディターでは、テキスト マーカーを使用してドキュメント内のナビゲーション ポイントを識別します。

## <a name="the-running-document-table"></a>実行中のドキュメント テーブル
 IDE では、実行中のドキュメント テーブル (RDT) を使用して、すべてのドキュメントウィンドウの状態を追跡します。 RDT は、ソリューションが閉じられた場合やファイルが編集された場合などのイベントをドキュメント ウィンドウに通知するためのメカニズムです。 詳細については、「[実行中のドキュメント テーブル](../../extensibility/internals/running-document-table.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [ドキュメントの読み込みの遅延](../../extensibility/internals/delayed-document-loading.md)
