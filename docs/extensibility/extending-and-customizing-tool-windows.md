---
title: ツール ウィンドウの拡張とカスタマイズ | Microsoft Docs
description: プロパティ ウィンドウ、出力ウィンドウ、タスク一覧ウィンドウなど、Visual Studio に用意されているツール ウィンドウの拡張とカスタマイズについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- user interfaces, essentials
- tool windows, standard
ms.assetid: 46b2892e-7b2b-4b3f-83a7-b884f1e114ee
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 6e5b5615b8b004dcbdfe860ba4d775a3ace177ed
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105075225"
---
# <a name="extend-and-customize-tool-windows"></a>ツール ウィンドウの拡張とカスタマイズ
Visual Studio には、ツール ウィンドウ、ドキュメント ウィンドウ、ダイアログ ウィンドウなど、いくつかの異なる種類のウィンドウが用意されています。 **プロパティ** ウィンドウ、**出力** ウィンドウ、**タスク一覧** ウィンドウなどのその他のウィンドウも、ツール ウィンドウの種類です。

## <a name="tool-windows"></a>ツール ウィンドウ
 Visual Studio のツール ウィンドウは通常、ファイルベースでない読み取り専用のウィンドウです。 この点で、ツール ウィンドウは、読み取り/書き込みモードでファイルを表示するドキュメント ウィンドウと異なります。 **ツールボックス**、 **ソリューション エクスプローラー**、 **[プロパティ]** ウィンドウ、および **Web ブラウザー** はツール ウィンドウの例です。

 単純なツール ウィンドウを作成する方法については、「[ツール ウィンドウを追加する](../extensibility/adding-a-tool-window.md)」を参照してください。

 ツール ウィンドウを Visual Studio に登録するには、「[ツール ウィンドウを登録する](../extensibility/registering-a-tool-window.md)」を参照してください。

 ツール ウィンドウは、既定では単一インスタンスです、つまり、一度に開くことができるツール ウィンドウのインスタンスは 1 つのみです。 単一インスタンスのツール ウィンドウを開いた後は、IDE が閉じられるまで開いたままです。 単一インスタンスのツール ウィンドウを閉じると、その可視性のみが変更されます。 複数インスタンスのツール ウィンドウを作成して、ウィンドウの複数のインスタンスを同時に開くことも可能です。 詳細については、「[複数インスタンスのツール ウィンドウを作成する](../extensibility/creating-a-multi-instance-tool-window.md)」を参照してください。

 ツール ウィンドウは *動的* にすることができます。つまり、関連する UI コンテキストが適用されるたびに表示されます。 自動表示の使用により、IDE でのウィンドウの煩雑さが軽減されます。 詳細については、「[動的ツール ウィンドウを開く](../extensibility/opening-a-dynamic-tool-window.md)」を参照してください。

 ツール ウィンドウは、ドッキング、フローティング、またはドキュメント フレームのタブ付けが可能です。 ツール ウィンドウの枠は IDE によって提供され、サイズ、位置、ドッキング状態と、その他の永続的なプロパティを制御するために使用します。 ツール ウィンドウのペインには、内容が表示されます。 既定のサイズと位置はツール ウィンドウを最初に開くときにのみ適用されます。その後、ツール ウィンドウの状態は保持されます。

 ツール ウィンドウのペインでは、WPF ユーザー コントロールをホストして、ツールバーをサポートすることができます。 <xref:Microsoft.VisualStudio.Shell.WindowPane.Window%2A> プロパティをオーバーライドして、ホストされるコントロールのハンドルを返すことができます。

 ツール ウィンドウには、多くのさまざまな機能を追加できます。 たとえば、ツールバーを追加したり (「[ツール ウィンドウにツールバーを追加する](../extensibility/adding-a-toolbar-to-a-tool-window.md)」)、またはショートカット メニューを追加したり (「[ツール ウィンドウにショートカット メニューを追加する](../extensibility/adding-a-shortcut-menu-in-a-tool-window.md)」) することができます。 ツール ウィンドウ内の項目を検索できる検索コントロールを追加できます (「[ツール ウィンドウへの検索の追加](../extensibility/adding-search-to-a-tool-window.md)」)。

 ツール ウィンドウ イベントをサブスクライブできます (「[イベントのサブスクライブ](../extensibility/subscribing-to-an-event.md)」)。

## <a name="extend-existing-tool-windows"></a>既存のツール ウィンドウを拡張する
 新しい **[オプション]** ページと、 **[プロパティ]** ページの新しい設定に、ツール ウィンドウに関する情報を追加し、 **[タスク一覧]** ウィンドウと **[出力]** ウィンドウに書き込むことができます。 詳細については、「[プロパティ、タスク一覧、出力、オプション ウィンドウを拡張する](../extensibility/extending-the-properties-task-list-output-and-options-windows.md)」を参照してください。

## <a name="modal-dialog-boxes"></a>モーダル ダイアログ ボックス
 Visual Studio 拡張機能で、モーダル ダイアログ ボックスを作成するには、<xref:Microsoft.VisualStudio.PlatformUI.DialogWindow?displayProperty=fullName> からそれらを派生させる必要があります。これにより、それらと残りの UI を制御できます。 詳細については、「[モーダル ダイアログ ボックスの作成と管理](../extensibility/creating-and-managing-modal-dialog-boxes.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [ツール ウィンドウでの拡張機能の作成](../extensibility/creating-an-extension-with-a-tool-window.md)
- [プロジェクトを拡張する](../extensibility/extending-projects.md)
- [ソリューションを拡張する](../extensibility/extending-solutions.md)
