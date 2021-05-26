---
title: ユーザー インターフェイスの更新 |Microsoft Docs
description: VSPackage で新しいコマンドを実装した後でユーザー インターフェイスを更新するコードを追加する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- user interfaces, updating
- commands, updating UI
ms.assetid: 376e2f56-e7bf-4e62-89f5-3dada84a404b
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: e5aecf97683ff22b8c384acf1c8ffb83e671fa57
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105073730"
---
# <a name="updating-the-user-interface"></a>ユーザー インターフェイスの更新
コマンドを実装した後、新しいコマンドの状態を使用してユーザー インターフェイスを更新するコードを追加できます。

 一般的な Win32 アプリケーションでは、コマンド セットを継続的にポーリングできます。また、個々のコマンドの状態は、ユーザーが表示するときに調整できます。 ただし、[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] シェル でホストできる VSPackage の数に制限がないため、広範なポーリング、特にマネージド コードと COM 間の相互運用アセンブリに対するポーリングによって応答性が低下する可能性があります。

### <a name="to-update-the-ui"></a>UI を更新するには

1. 次のいずれかの操作を実行します。

    - <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.UpdateCommandUI%2A> メソッドを呼び出します。

         次のように、<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell> インターフェイスを <xref:Microsoft.VisualStudio.Shell.Interop.SVsUIShell> サービスから取得できます。

        ```csharp
        void UpdateUI(Microsoft.VisualStudio.Shell.ServiceProvider sp)
        {
            IVsUIShell vsShell = (IVsUIShell)sp.GetService(typeof(IVsUIShell));
            if (vsShell != null)
            {
                int hr = vsShell.UpdateCommandUI(0);
                Microsoft.VisualStudio.ErrorHandler.ThrowOnFailure(hr);
            }
        }

        ```

         <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.UpdateCommandUI%2A> のパラメーターが 0 以外 (`TRUE`) の場合、更新は同期的に直ちに実行されます。 適切なパフォーマンスを維持するために、このパラメーターには 0 (`FALSE`) を渡すことをお勧めします。 キャッシュを回避する場合は、.vsct ファイルでコマンドを作成するときに `DontCache` フラグを適用します。 ただし、フラグは慎重に使用してください。そうしないと、パフォーマンスが低下する可能性があります。 コマンド フラグの詳細については、「[コマンド フラグ要素](../extensibility/command-flag-element.md)」のドキュメントを参照してください。

    - ウィンドウでインプレース アクティブ化モデルを使用して ActiveX コントロールをホストする VSPackage では、<xref:Microsoft.VisualStudio.Shell.Interop.IOleInPlaceComponentUIManager.UpdateUI%2A> メソッドを使用するほうが便利な場合があります。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell> インターフェイスの <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.UpdateCommandUI%2A> メソッドと <xref:Microsoft.VisualStudio.Shell.Interop.IOleInPlaceComponentUIManager> インターフェイスの <xref:Microsoft.VisualStudio.Shell.Interop.IOleInPlaceComponentUIManager.UpdateUI%2A> メソッドは、機能的に同等です。 どちらの場合でも、環境はすべてのコマンドの状態を再クエリします。 通常、更新プログラムはすぐには実行されません。 代わりに、アイドル時間まで更新が遅延されます。 シェルは、良好なパフォーマンスを維持するために、コマンドの状態をキャッシュします。 キャッシュを回避する場合は、.vsct ファイルでコマンドを作成するときに `DontCache` フラグを適用します。 ただし、パフォーマンスが低下する可能性があるためフラグは慎重に使用してください。

         <xref:Microsoft.VisualStudio.Shell.Interop.IOleInPlaceComponentUIManager> インターフェイスを取得するには、<xref:Microsoft.VisualStudio.Shell.Interop.IOleComponentUIManager> オブジェクトで `QueryInterface` メソッドを呼び出すか、または <xref:Microsoft.VisualStudio.Shell.Interop.SOleComponentUIManager> サービスからインターフェイスを取得します。

## <a name="see-also"></a>関連項目
- [VSPackage でユーザー インターフェイス要素を追加する方法](../extensibility/internals/how-vspackages-add-user-interface-elements.md)
- [実装](../extensibility/internals/command-implementation.md)
