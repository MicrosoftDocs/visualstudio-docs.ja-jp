---
title: 相互運用機能アセンブリを使用したコマンドのステータスの確認 | Microsoft Docs
description: Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget インターフェイスを使用して、VSPackage で処理されるコマンドのステータスを確認する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- interop assemblies, determining command status
- command handling with interop assemblies, status
ms.assetid: 2f5104d1-7b4c-4ca0-a626-50530a8f7f5c
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: ef6940aef83ad3865385b4e39fd9cfd62b8866d7
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105090903"
---
# <a name="determine-command-status-by-using-interop-assemblies"></a>相互運用機能アセンブリを使用してコマンドのステータスを確認する
VSPackage では、処理可能なコマンドの状態を追跡する必要があります。 環境では、VSPackage 内で処理されたコマンドが有効または無効になるタイミングを判断できません。 **[切り取り]** 、 **[コピー]** 、 **[貼り付け]** などの一般的なコマンドの状態など、コマンドの状態について環境に通知するのは、VSPackage の役割です。

## <a name="status-notification-sources"></a>状態の通知ソース
 環境では、<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> インターフェイスの VSPackage の実装の一部である VSPackage の <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A> メソッドを使用して、コマンドに関する情報を受け取ります。 環境では、次の 2 つの条件下で VSPackage の <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A> メソッドを呼び出します。

- ユーザーがメイン メニューまたはコンテキスト メニュー (右クリック) を開くと、その状態を確認するために、環境でそのメニューのすべてのコマンドに対して <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A> メソッドが実行されます。

- VSPackage により、環境で現在のユーザー インターフェイス (UI) を更新することが要求されたとき。 この更新は、標準ツール バーの **[切り取り]** 、 **[コピー]** 、 **[貼り付け]** のグループ化などの現在ユーザーに表示されているコマンドが、コンテキストとユーザーの操作に応じて有効または無効になると実行されます。

  シェルは複数の VSPackage をホストするため、コマンドのステータスを確認するために各 VSPackage をポーリングする必要がある場合は、シェルのパフォーマンスが許容できないほど低下する可能性があります。 代わりに、VSPackage は、変更時に UI が変更されたときに環境に対して積極的に通知する必要があります。 更新通知の詳細については、[ユーザー インターフェイスの更新](../../extensibility/updating-the-user-interface.md)に関するページを参照してください。

## <a name="status-notification-failure"></a>状態の通知エラー
 VSPackage によりコマンドの状態の変更が環境に通知されないと、UI が不整合な状態になる可能性があります。 メニューまたはコンテキスト メニューのコマンドは、ユーザーがツール バー上に配置できることに注意してください。 そのため、メニューまたはコンテキスト メニューが開いているときにのみ UI を更新するだけでは十分ではありません。

## <a name="see-also"></a>関連項目
- [VSPackage でユーザー インターフェイス要素を追加する方法](../../extensibility/internals/how-vspackages-add-user-interface-elements.md)
- [実装](../../extensibility/internals/command-implementation.md)
