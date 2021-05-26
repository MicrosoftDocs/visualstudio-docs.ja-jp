---
title: コマンドの実装 | Microsoft Docs
description: Visual Studio でのコマンドの実装、VSPackage でコマンド グループを設定する方法、コマンドを追加する方法、コマンドを登録する方法、実装する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- commands, implementation
ms.assetid: c782175c-cce4-4bd0-8374-4a897ceb1b3d
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 93c99b131340d2e53b931619d4e5742d9e19f570
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105091140"
---
# <a name="command-implementation"></a>コマンドの実装
VSPackage でコマンドを実装するには、次のタスクを実行する必要があります。

1. *.vsct* ファイルで、コマンド グループを設定し、コマンドを追加します。 詳細については、「[Visual Studio コマンド テーブル (.vsct) ファイル](../../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)」を参照してください。

2. コマンドを Visual Studio に登録します。

3. コマンドを実装します。

次のセクションでは、コマンドを登録して実装する方法について説明します。

## <a name="register-commands-with-visual-studio"></a>コマンドを Visual Studio に登録する
 メニューにコマンドが表示されるようにするには、<xref:Microsoft.VisualStudio.Shell.ProvideMenuResourceAttribute> を VSPackage に追加し、メニューの名前またはそのリソース ID のいずれかを値として使用する必要があります。

```
[ProvideMenuResource("Menus.ctmenu", 1)]
...
    public sealed class MyPackage : Package
    {.. ..}

```

 また、コマンドを <xref:Microsoft.VisualStudio.Shell.OleMenuCommandService> に登録する必要があります。 VSPackage が <xref:Microsoft.VisualStudio.Shell.Package> から派生している場合は、<xref:Microsoft.VisualStudio.Shell.Package.GetService%2A> メソッドを使用してこのサービスを取得できます。

```
OleMenuCommandService mcs = GetService(typeof(IMenuCommandService)) as OleMenuCommandService;
if ( null != mcs )
{
    // Create the command for the menu item.
    CommandID menuCommandID = new CommandID(guidCommandGroup, myCommandID);
    MenuCommand menuItem = new MenuCommand(MenuItemCallback, menuCommandID );
    mcs.AddCommand( menuItem );
}

```

## <a name="implement-commands"></a>コマンドを実装する
 コマンドを実装するにはいくつかの方法があります。 常に同じように表示されるコマンドである静的メニュー コマンドが必要な場合は、前のセクションの例に示すように、<xref:System.ComponentModel.Design.MenuCommand> を使用してコマンドを作成します。 静的コマンドを作成するには、コマンドを実行するイベント ハンドラーを指定する必要があります。 コマンドは常に有効で表示されているため、Visual Studio にその状態を指定する必要はありません。 特定の条件に応じてコマンドの状態を変更する場合は、<xref:Microsoft.VisualStudio.Shell.OleMenuCommand> クラスのインスタンスとしてコマンドを作成し、そのコンストラクターで、コマンドを実行するためのイベント ハンドラーと、コマンドの状態が変化したときに Visual Studio に通知する `QueryStatus` ハンドラーを指定します。 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> をコマンド クラスの一部として実装することも、プロジェクトの一部としてコマンドを指定する場合は <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> を実装することもできます。 2 つのインターフェイスと <xref:Microsoft.VisualStudio.Shell.OleMenuCommand> クラスにはすべて、コマンドの状態の変更を Visual Studio に通知するメソッドと、コマンドを実行するその他のメソッドがあります。

 コマンドは、コマンド サービスに追加されると、コマンドのチェーンの 1 つになります。 コマンドの状態通知と実行メソッドを実装する場合は、その特定のコマンドについてだけ指定し、その他のすべてのケースをチェーン内の他のコマンドに渡すように注意してください。 (通常は <xref:Microsoft.VisualStudio.OLE.Interop.Constants.OLECMDERR_E_NOTSUPPORTED> を返すことで) コマンドを渡すことができない場合、Visual Studio は正常に動作しなくなる可能性があります。

## <a name="querystatus-methods"></a>QueryStatus メソッド
 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A> メソッドまたは <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy.QueryStatusCommand%2A> メソッドのいずれかを実装する場合は、コマンドが属するコマンド セットの GUID とコマンドの ID を確認します。 次のガイドラインに従ってください。

- GUID が認識されない場合、いずれかのメソッドの実装では <xref:Microsoft.VisualStudio.OLE.Interop.Constants.OLECMDERR_E_UNKNOWNGROUP> を返す必要があります。

- いずれかのメソッドの実装で GUID が認識されていても、コマンドが実装されていない場合、メソッドでは <xref:Microsoft.VisualStudio.OLE.Interop.Constants.OLECMDERR_E_NOTSUPPORTED> を返す必要があります。

- いずれのメソッドの実装でも GUID とコマンドの両方が認識されている場合、メソッドでは、次の <xref:Microsoft.VisualStudio.OLE.Interop.OLECMDF> フラグを使用して、(`prgCmds` パラメーター内の) すべてのコマンドのコマンド フラグ フィールドを設定する必要があります。

  - `OLECMDF_SUPPORTED`: コマンドはサポートされます。

  - `OLECMDF_INVISIBLE`: コマンドを参照可能にすることはできません。

  - `OLECMDF_LATCHED`: コマンドはオンに切り替えられ、チェック済みのように表示されます。

  - `OLECMDF_ENABLED`: コマンドは有効です。

  - `OLECMDF_DEFHIDEONCTXTMENU`: ショートカット メニューに表示されている場合は、コマンドを非表示にする必要があります。

  - `OLECMDF_NINCHED`: コマンドはメニュー コントローラーであり、有効になっていませんが、ドロップダウン メニュー リストが空ではなく、引き続き使用できます。 (このフラグはほとんど使用されません)。

- `TextChanges` フラグを使用してコマンドが *.vsct* ファイルで定義されている場合は、次のパラメーターを設定します。

  - `pCmdText` パラメーターの `rgwz` 要素をコマンドの新しいテキストに設定します。

  - `pCmdText` パラメーターの `cwActual` 要素をコマンド文字列のサイズに設定します。

また、コマンドの目的が特にオートメーション関数を処理することである場合を除き、現在のコンテキストがオートメーション関数でないことを確認してください。

特定のコマンドをサポートしていることを示すには、<xref:Microsoft.VisualStudio.VSConstants.S_OK> を返します。 それ以外のすべてのコマンドについては、<xref:Microsoft.VisualStudio.OLE.Interop.Constants.OLECMDERR_E_NOTSUPPORTED> を返します。

次の例の `QueryStatus` メソッドでは、最初にコンテキストがオートメーション関数でないことを確認し、次に正しいコマンド セット GUID とコマンド ID を検索します。 コマンド自体は有効に設定され、サポートされます。 その他のコマンドがサポートされません。

```csharp
public int QueryStatus(ref Guid pguidCmdGroup, uint cCmds, OLECMD[] prgCmds, IntPtr pCmdText)
{
    if (!VsShellUtilities.IsInAutomationFunction(m_provider.ServiceProvider))
    {
        if (pguidCmdGroup == VSConstants.VSStd2K && cCmds > 0)
        {
            // make the Right command visible
            if ((uint)prgCmds[0].cmdID == (uint)VSConstants.VSStd2KCmdID.RIGHT)
            {
                prgCmds[0].cmdf = (int)Microsoft.VisualStudio.OLE.Interop.Constants.MSOCMDF_ENABLED | (int)Microsoft.VisualStudio.OLE.Interop.Constants.MSOCMDF_SUPPORTED;
                return VSConstants.S_OK;
            }
        }
        return Constants.OLECMDERR_E_NOTSUPPORTED;
    }
}
```

## <a name="execution-methods"></a>実行メソッド
 `Exec` メソッドの実装は、`QueryStatus` メソッドの実装に似ています。 まず、コンテキストがオートメーション関数ではないことを確認します。 次に、GUID とコマンド ID の両方をテストします。 GUID またはコマンド ID が認識されない場合は、<xref:Microsoft.VisualStudio.OLE.Interop.Constants.OLECMDERR_E_NOTSUPPORTED> を返します。

 コマンドを処理するには、これを実行して、実行が成功した場合は <xref:Microsoft.VisualStudio.VSConstants.S_OK> を返します。 コマンドでは、エラーの検出と通知を行います。そのため、実行が失敗した場合は、エラー コードを返します。 次の例は、実行メソッドを実装する方法を示しています。

```csharp
public int Exec(ref Guid pguidCmdGroup, uint nCmdID, uint nCmdexecopt, IntPtr pvaIn, IntPtr pvaOut)
{
    if (!VsShellUtilities.IsInAutomationFunction(m_provider.ServiceProvider))
    {
        if (pguidCmdGroup == VSConstants.GUID_VSStandardCommandSet97)
        {
             if (nCmdID ==(uint) uint)VSConstants.VSStd2KCmdID.RIGHT)
            {
                //execute the command
                return VSConstants.S_OK;
            }
        }
    }
    return Constants.OLECMDERR_E_NOTSUPPORTED;
}
```

## <a name="see-also"></a>関連項目

- [VSPackage でユーザー インターフェイス要素を追加する方法](../../extensibility/internals/how-vspackages-add-user-interface-elements.md)
