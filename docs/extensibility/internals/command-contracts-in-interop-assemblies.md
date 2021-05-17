---
title: 相互運用機能アセンブリでのコマンドのコントラクト | Microsoft Docs
description: Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget インターフェイスを使用してコマンドを処理するための基本的なコントラクトについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- command handling with interop assemblies, command contracts
- interop assemblies, command contracts
ms.assetid: 57245708-f539-42dc-8963-2754a48f0189
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 36c757faacb7fe3193f9acbbd040468f66b0623a
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105086054"
---
# <a name="command-contracts-in-interop-assemblies"></a>相互運用機能アセンブリでのコマンドのコントラクト
<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> インターフェイスを使用してコマンドを処理するための基本的なコントラクトでは、環境で <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A> メソッドを呼び出してコマンドがサポートされているかどうかが判別され、サポートされている場合はその状態とテキストが判別されます。 次に、環境で <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.Exec%2A> メソッドが呼び出され、コマンドが実行されます。

 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A> メソッドは、すべてのコマンドで同様に処理されます。 必要に応じてさらにやり取りを行う場合 (ドロップダウン リストを使用する場合など) は、適切なパラメーターを指定して <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.Exec%2A> メソッドを呼び出すことによって管理されます。 これらのパラメーターの解釈は、指定されたコマンドによって異なります。

 コマンドのターゲットによって出力パラメーターに値が返される場合、割り当てられたリソースを解放する責任は常に呼び出し元にあります。 このパラメーターはバリアントであるため、バリアントをクリアするとリソースが解放されます。

 コマンドが階層ウィンドウ内で動作する必要がある場合は、<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy> インターフェイスを使用する必要があります。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy> インターフェイスには同様のコントラクトがあり、同様のメソッド (<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy.QueryStatusCommand%2A> と <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy.ExecCommand%2A>) があります。

## <a name="see-also"></a>関連項目
- [VSPackage でユーザー インターフェイス要素を追加する方法](../../extensibility/internals/how-vspackages-add-user-interface-elements.md)
- [VSPackage のコマンド ルーティング](../../extensibility/internals/command-routing-in-vspackages.md)
- [コマンドの実装](../../extensibility/internals/command-implementation.md)
