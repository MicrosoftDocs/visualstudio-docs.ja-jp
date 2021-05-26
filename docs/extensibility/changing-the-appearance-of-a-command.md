---
title: コマンドの外観の変更 | Microsoft Docs
description: コマンドを使用可能/使用不可、表示/非表示、またはオン/オフにするかなど、コマンドの外観を変更することでフィードバックを提供する方法を説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- commands, changing appearance
- menu commands, changing appearance
- menus, changing command appearance
ms.assetid: da2474fa-f92d-4e9e-b8bf-67c61bf249c2
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 8b6911d865b253ff82ffcc6c4911e0989f109f28
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105089824"
---
# <a name="change-the-appearance-of-a-command"></a>コマンドの外観の変更
コマンドの外観を変更することで、ユーザーにフィードバックを提供できます。 たとえば、コマンドを使用できないときは、その外観が変化するようにします。 コマンドの使用可能と使用不可、表示と非表示、メニューでのオンとオフを切り替えることができます。

コマンドの外観を変更するには、次のいずれかの操作を実行します。

- コマンド テーブル ファイルのコマンド定義で、適切なフラグを指定します。

- <xref:Microsoft.VisualStudio.Shell.OleMenuCommandService> サービスを使用します。

- <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> インターフェイスを実装し、未加工のコマンド オブジェクトを変更します。

  次の手順では、マネージド パッケージ フレームワーク (MPF) を使用して、コマンドの外観を検索し、更新する方法を説明します。

### <a name="to-change-the-appearance-of-a-menu-command"></a>メニュー コマンドの外観を変更するには

1. 「[メニュー コマンドのテキストを変更する](../extensibility/changing-the-text-of-a-menu-command.md)」の手順に従って、`New Text` という名前のメニュー項目を作成します。

2. *ConnectMenuText.cs* ファイルで、次の using ステートメントを追加します。

    ```csharp
    using System.Security.Permissions;
    ```

3. *ChangeMenuTextPackageGuids.cs* ファイルで、次の行を追加します。

    ```csharp
    public const string guidChangeMenuTextPackageCmdSet= "00000000-0000-0000-0000-00000000";  // get the GUID from the .vsct file
    ```

4. *ChangeMenuText.cs* ファイルで、ShowMessageBox メソッドのコードを、次の行に置き替えます。

    ```csharp
    private void Execute(object sender, EventArgs e)
    {
        ThreadHelper.ThrowIfNotOnUIThread();
        var command = sender as OleMenuCommand;
        if (command.Text == "New Text")
            ChangeMyCommand(command.CommandID.ID, false);
    }
    ```

5. <xref:Microsoft.VisualStudio.Shell.OleMenuCommandService> オブジェクトから、更新するコマンドを取得し、コマンド オブジェクトで適切なプロパティを設定します。 たとえば、次のメソッドにより、VSPackage コマンド セットの指定されたコマンドが使用可能または使用不可になります。 次のコードにより、`New Text` というメニュー項目が、クリックされた後に使用不可になります。

    ```csharp
    public bool ChangeMyCommand(int cmdID, bool enableCmd)
    {
        bool cmdUpdated = false;
        var mcs = this.package.GetService<IMenuCommandService, OleMenuCommandService>();
        var newCmdID = new CommandID(new Guid(ChangeMenuTextPackageGuids.guidChangeMenuTextPackageCmdSet), cmdID);
        MenuCommand mc = mcs.FindCommand(newCmdID);
        if (mc != null)
        {
            mc.Enabled = enableCmd;
            cmdUpdated = true;
        }
        return cmdUpdated;
    }
    ```

6. プロジェクトをビルドし、デバッグを開始します。 Visual Studio の実験用インスタンスが表示されます。

7. **[ツール]** メニューの **[ChangeMenuText の呼び出し]** コマンドをクリックします。 この時点では、コマンド名が **Invoke ChangeMenuText** であるため、コマンド ハンドラーは **ChangeMyCommand()** を呼び出しません。

8. **[ツール]** メニューに、 **[新しいテキスト]** が表示されます。 **[新しいテキスト]** をクリックします。 コマンドがグレーで表示されます。

## <a name="see-also"></a>関連項目
- [コマンド、メニュー、およびツール バー](../extensibility/internals/commands-menus-and-toolbars.md)
- [VSPackage でユーザー インターフェイス要素を追加する方法](../extensibility/internals/how-vspackages-add-user-interface-elements.md)
- [メニューとコマンドの拡張](../extensibility/extending-menus-and-commands.md)
- [Visual Studio コマンド テーブル (.vsct) ファイル](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
