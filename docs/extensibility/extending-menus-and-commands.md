---
title: メニューとコマンドの拡張 | Microsoft Docs
description: アクションとプロセスを Visual Studio に追加するコマンドについて説明します。 VSPackage プロジェクト テンプレートは、きわめて基本的なコマンドを実装する方法を示しています。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- menus, common tasks
- VSPackages, menu tasks
- .vsct files, common menu tasks
ms.assetid: 7b2be4b9-e3fe-4412-874f-ae72ebc84c4b
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 6a96978cdad45c669b607c18e12b2e492dcf95bb
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105075212"
---
# <a name="extend-menus-and-commands"></a>メニューとコマンドを拡張する
コマンドは、Visual Studio にアクションとプロセスを追加する方法です。 ほとんどの場合に、コマンドはメニューまたはツールバーに表示されます。 VSPackage プロジェクト テンプレートは、きわめて基本的なコマンドを実装する方法を示しています。 やや長くなりますが、まだ基本的な実装については、「[メニュー コマンドを使用して拡張機能を作成する](../extensibility/creating-an-extension-with-a-menu-command.md)」を参照してください。

 Visual Studio のコマンド、メニュー、およびツール バーの詳細については、「[コマンド、メニュー、およびツール バー](../extensibility/internals/commands-menus-and-toolbars.md)」を参照してください。

 コマンド、メニュー、およびツールバーは、VSPackage プロジェクトの一部である *.vsct* ファイルに定義されます。 Visual Studio IDE と *.vsct* ファイルに関する情報については、「[VSPackage でユーザー インターフェイス要素を追加する方法](../extensibility/internals/how-vspackages-add-user-interface-elements.md)」を参照してください。

 以下のトピックでは、さまざまな種類のコマンド、メニュー、およびツールバーを追加する方法について説明します。

## <a name="in-this-section"></a>このセクションの内容
- 「[メニューを Visual Studio のメニュー バーに追加する](../extensibility/adding-a-menu-to-the-visual-studio-menu-bar.md)」Visual Studio のトップ メニュー バーにメニューを追加する方法について説明します。

- 「[メニュー項目にキーボード ショートカットをバインドする](../extensibility/binding-keyboard-shortcuts-to-menu-items.md)」キーボード ショートカット (Ctrl + 3 など) をメニュー項目に追加する方法について説明します。

- 「[メニューにサブメニューを追加する](../extensibility/adding-a-submenu-to-a-menu.md)」トップ メニューにサブメニューを追加する方法について説明します。

- 「[最近使用した一覧をサブメニューに追加する](../extensibility/adding-a-most-recently-used-list-to-a-submenu.md)」最近使用した一覧を追加する方法について説明します。

- 「[再利用可能なボタンのグループを作成する](../extensibility/creating-reusable-groups-of-buttons.md)」コマンド項目を複数のメニューに含めることができるようにグループ化する方法について説明します。

- 「[メニュー コマンドにアイコンを追加する](../extensibility/adding-icons-to-menu-commands.md)」ツールバーとメニューの両方でコマンドにアイコンを追加する方法について説明します。

- 「[メニュー コマンドのテキストを変更する](../extensibility/changing-the-text-of-a-menu-command.md)」メニュー項目を動的に変更できるようにするための `TextChanges` フラグの使用について説明します。

- 「[コマンドの外観を変更する](../extensibility/changing-the-appearance-of-a-command.md)」コマンドを動的に有効または無効にする方法について説明します。

- 「[ユーザー インターフェイスの更新](../extensibility/updating-the-user-interface.md)」ユーザー インターフェイスを強制的に更新して最新の変更を反映する方法について説明します。

- 「[メニュー コマンドのローカライズ](../extensibility/localizing-menu-commands.md)」メニュー コマンドをローカライズする方法について説明します。
