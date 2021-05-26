---
title: IDE 定義コマンド、メニュー、およびグループ | Microsoft Docs
description: Visual Studio 統合開発環境 (IDE) で定義されているメニュー、コマンド、およびコマンド グループについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- commands, environment-defined
- .vsct files, environment-defined constants
- command groups, environment-defined
ms.assetid: 86b3af13-7163-48c6-986b-7beeedbc26cc
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 5b88bbab9c92cdd8627521eaa58284fd33964b7e
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105085950"
---
# <a name="ide-defined-commands-menus-and-groups"></a>IDE 定義コマンド、メニュー、およびグループ
多くのメニュー、コマンド、およびコマンド グループが、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] IDE で使用するために既に定義されています。 これらのコマンドは、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] を独自に拡張するときにも使用できます。

## <a name="finding-environment-defined-commands"></a>環境定義コマンドの検索
 環境のコマンドは、次に示す 4 つの .vsct ファイルのセットで定義されます。

- SharedCmdDef.vsct

- SharedCmdPlace.vsct

- ShellCmdDef.vsct

- ShellCmdPlace.vsct

  これらのファイルは *\<Visual Studio SDK installation path>* \VisualStudioIntegration\Common\Inc\\ にあります。 これらのファイルには、メニューとグループの定義および GUID が指定されます。これらのメニューとグループは、VSPackage のコマンド テーブル構成 (.ctc) ファイルで、独自のメニュー、グループ、およびコマンドのコンテナーとして使用できます。

## <a name="in-this-section"></a>このセクションの内容
- [Visual Studio メニューの GUID および ID](../../extensibility/internals/guids-and-ids-of-visual-studio-menus.md)

 Visual Studio のメニュー バーにあるメニューおよびそれらに含まれるグループの、GUID と ID の値を示します。

- [Visual Studio ツール バーの GUID および ID](../../extensibility/internals/guids-and-ids-of-visual-studio-toolbars.md)

 Visual Studio IDE のツール バーおよびそれらに含まれるグループの、GUID と ID の値を示します。

- [Visual Studio コマンドの GUID および ID](../../extensibility/internals/guids-and-ids-of-visual-studio-commands.md)

 Visual Studio IDE で定義されているコマンドの GUID と ID の値を示します。

## <a name="see-also"></a>関連項目
- [Visual Studio Command Table (.Vsct) ファイル](../../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
- [プロジェクト システムを拡張するための IDE 定義コマンド](../../extensibility/internals/ide-defined-commands-for-extending-project-systems.md)
- [VSPackage でユーザー インターフェイス要素を追加する方法](../../extensibility/internals/how-vspackages-add-user-interface-elements.md)
