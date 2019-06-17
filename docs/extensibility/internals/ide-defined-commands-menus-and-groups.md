---
title: IDE 定義コマンド、メニューのおよびグループ |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- commands, environment-defined
- .vsct files, environment-defined constants
- command groups, environment-defined
ms.assetid: 86b3af13-7163-48c6-986b-7beeedbc26cc
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 5158a9d1a06ec6f08c67777e4f1ce2e4d37220e3
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66315659"
---
# <a name="ide-defined-commands-menus-and-groups"></a>IDE 定義コマンド、メニュー、およびグループ
によって使用される多くのメニューのコマンドおよびコマンド グループが定義済み、 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] IDE。 これらのコマンドを拡張するときにもご利用いただけます[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]します。

## <a name="finding-environment-defined-commands"></a>環境定義コマンドを見つける
 環境のコマンドは、一連の 4 つの .vsct ファイルで定義されます。

- SharedCmdDef.vsct

- SharedCmdPlace.vsct

- ShellCmdDef.vsct

- ShellCmdPlace.vsct

  これらのファイルにある *\<Visual Studio SDK インストール パス >* \VisualStudioIntegration\Common\Inc\\します。 これらのファイルは、定義と、メニューとメニューのグループ、およびコマンドの独自のコンテナーとして、VSPackage のコマンド テーブル (.vsct) の構成ファイルを使用できるグループの Guid を提供します。

## <a name="in-this-section"></a>このセクションの内容
- [Visual Studio メニューの GUID および ID](../../extensibility/internals/guids-and-ids-of-visual-studio-menus.md)

 Visual Studio のメニュー バーでメニューおよびが含まれているグループの GUID と ID 値を示します。

- [Visual Studio ツール バーの GUID および ID](../../extensibility/internals/guids-and-ids-of-visual-studio-toolbars.md)

 Visual Studio IDE でツールバーおよびが含まれているグループの GUID と ID 値を示します。

- [Visual Studio コマンドの GUID および ID](../../extensibility/internals/guids-and-ids-of-visual-studio-commands.md)

 Visual Studio IDE で定義されているコマンドの GUID と ID の値を示します。

## <a name="see-also"></a>関連項目
- [Visual Studio Command Table (.Vsct) ファイル](../../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
- [プロジェクト システムを拡張するための IDE 定義コマンド](../../extensibility/internals/ide-defined-commands-for-extending-project-systems.md)
- [VSPackage でユーザー インターフェイス要素を追加する方法](../../extensibility/internals/how-vspackages-add-user-interface-elements.md)