---
title: コマンドの可用性 | Microsoft Docs
description: 現在のプロジェクト、現在のエディター、およびその他の要因に基づいて変更されるコマンド コンテキストにより、Visual Studio で使用できるコマンドがどのように決まるかについて説明します。
ms.custom: SEO-VS-2020
ms.date: 03/22/2018
ms.topic: conceptual
helpviewer_keywords:
- commands, context
- menu items, visibility contexts
ms.assetid: c74e3ccf-d771-48c8-a2f9-df323b166784
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 738e326c0e6300520d66d64fda4bb5040f231c75
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105074744"
---
# <a name="command-availability"></a>コマンドの可用性

Visual Studio のコンテキストにより、使用可能なコマンドが決まります。 コンテキストは、現在のプロジェクト、現在のエディター、読み込まれている VSPackage、および統合開発環境 (IDE) のその他の側面によって変わります。

## <a name="command-contexts"></a>コマンド コンテキスト

最も一般的なコマンド コンテキストは、次のとおりです。

- IDE: IDE によって提供されるコマンドは常に使用可能です。

- VSPackage: VSPackage では、コマンドをいつ表示または非表示にするかを定義できます。

- プロジェクト: プロジェクト コマンドは、現在選択されているプロジェクトにのみ表示されます。

- エディター: エディターは、一度に 1 つしかアクティブにできません。 アクティブなエディターのコマンドは使用可能です。 エディターは言語サービスと密接に連携します。 言語サービスは、関連付けられているエディターのコンテキストでコマンドを処理する必要があります。

- ファイルの種類: エディターは、複数の種類のファイルを読み込むことができます。 使用可能なコマンドは、ファイルの種類によって変わることがあります。

- アクティブ ウィンドウ: 直前のアクティブなドキュメント ウィンドウでは、キー バインドのユーザー インターフェイス (UI) コンテキストを設定します。 ただし、内部 Web ブラウザーに似たキー バインド テーブルがあるツール ウィンドウでは、UI コンテキストを設定することもできます。 HTML エディターなどの複数のタブ付きのドキュメント ウィンドウでは、すべてのタブに異なるコマンド コンテキスト GUID があります。 ツール ウィンドウは、登録された後は常に **[表示]** メニューで使用可能です。

- UI コンテキスト: UI コンテキストは、<xref:Microsoft.VisualStudio.VSConstants.UICONTEXT> クラスの値によって識別されます。たとえば、ソリューションがビルドされているときは <xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.SolutionBuilding_guid>、デバッガーがアクティブになっているときは <xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.Debugging_guid> です。 複数の UI コンテキストを同時にアクティブにすることができます。

## <a name="define-custom-context-guids"></a>カスタム コンテキスト GUID を定義する

適切なコマンド コンテキスト GUID がまだ定義されていない場合は、VSPackage で定義してから、コマンドの表示を制御するために必要に応じてアクティブまたは非アクティブになるようにプログラムすることができます。

1. <xref:Microsoft.VisualStudio.Shell.Interop.IVsMonitorSelection.GetCmdUIContextCookie%2A> メソッドを呼び出して、コンテキスト GUID を登録します。

2. <xref:Microsoft.VisualStudio.Shell.Interop.IVsMonitorSelection.IsCmdUIContextActive%2A> メソッドを呼び出して、コンテキスト GUID の状態を取得します。

3. <xref:Microsoft.VisualStudio.Shell.Interop.IVsMonitorSelection.SetCmdUIContext%2A> メソッドを呼び出して、コンテキスト GUID のオンとオフを切り替えます。

> [!CAUTION]
> 他の VSPackage が既存のコンテキスト GUID に依存している可能性があるため、ご使用の VSPackage がそれらに影響しないことを確認してください。

## <a name="see-also"></a>関連項目

- [選択コンテキスト オブジェクト](../../extensibility/internals/selection-context-objects.md)
- [VSPackage でユーザー インターフェイス要素を追加する方法](../../extensibility/internals/how-vspackages-add-user-interface-elements.md)
