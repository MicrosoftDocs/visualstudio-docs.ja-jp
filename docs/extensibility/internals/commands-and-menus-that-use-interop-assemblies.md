---
title: 相互運用機能アセンブリを使用するコマンドとメニュー | Microsoft Docs
description: 相互運用機能アセンブリを使用して VSPackage でメニューおよびツールバーコマンドを実装するときに完了する必要があるタスクについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- menus, using interop assemblies
- interop assemblies, using in commands and menus
- commands, handling using interop assemblies
- command handling with interop assemblies
ms.assetid: 8f4af525-39e5-4e69-92c8-d3efabe80bb2
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: b5a487c2fe6f97e338924a0b8c682f9dd9798571
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105057235"
---
# <a name="commands-and-menus-that-use-interop-assemblies"></a>相互運用機能アセンブリを使用するコマンドとメニュー
相互運用機能アセンブリを使用してメニューとツールバーのコマンドを実装する VSPackage は、次を行う必要があります。

- [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 統合開発環境 (IDE) にサポートしているコマンドと、現在有効になっているかどうかについて通知します。

- コマンドを処理するためのルール (コントラクト) に従います。

- <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> または <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy> インターフェイスを使用して、コマンド処理を明示的に実装します。

  次のセクションでは、これらのタスクを実行する方法について説明します。

## <a name="in-this-section"></a>このセクションの内容
- [相互運用機能アセンブリを使用してコマンドのステータスを確認する](../../extensibility/internals/determining-command-status-by-using-interop-assemblies.md)

 VSPackage がどのコマンドをサポートしているか、および現在有効になっているかどうかを IDE に通知する方法について説明します。

- [相互運用機能アセンブリでのコマンドのコントラクト](../../extensibility/internals/command-contracts-in-interop-assemblies.md)

 相互運用機能アセンブリを使用してコマンドを実装するすべての Vspackage で使用される基本的なコマンド コントラクトの定義を提供します。

- [コマンドの実装](../../extensibility/internals/command-implementation.md)

 VSPackage によるコマンドの実装方法の概要について説明します。

- [相互運用機能アセンブリ コマンド ハンドラーの登録](../../extensibility/internals/registering-interop-assembly-command-handlers.md)

 VSPackage によりコマンド ハンドラーが提供されることを IDE に通知するために必要なレジストリ エントリについて説明します。

## <a name="related-sections"></a>関連項目
- [コマンドの可用性](../../extensibility/internals/command-availability.md)

 使用できる VSPackage コマンドと、それらを処理するオブジェクトを決定するために IDE によって使用される条件について説明します。

- [VSPackage でユーザー インターフェイス要素を追加する方法](../../extensibility/internals/how-vspackages-add-user-interface-elements.md)

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] コマンド サポートを使用する UI を作成する方法の詳細について説明します。

- [VSPackage のコマンド ルーティング](../../extensibility/internals/command-routing-in-vspackages.md)

 オブジェクトを適切なコマンド要求に関連付けるために使用されるプロセスの概要です。
