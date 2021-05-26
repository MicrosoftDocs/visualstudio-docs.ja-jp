---
title: 既定のコマンド、グループ、ツール バーの配置 | Microsoft Docs
description: 既定で Visual Studio ユーザー インターフェイスに表示される IDE コマンド、製品コマンド、エディター コマンドについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- commands [Visual Studio], default groups
- toolbars [Visual Studio], default
- commands [Visual Studio], default editor
- command groups
- commands [Visual Studio], default IDE
- commands [Visual Studio], default product
ms.assetid: 35342110-d639-4577-8367-00b21dcc6f07
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 07e93db9ffe79c3c49072b3379def14a3be2852c
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105091007"
---
# <a name="default-command-group-and-toolbar-placement"></a>既定のコマンド、グループ、ツール バーの配置
製品の統一性と安定性を確保するために、UI には特定のコマンド グループが既定で表示され、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] にはコマンドとコマンド グループの定義が用意されています。 VSPackage では、標準のコマンドとコマンド グループを使用することもできます。

 既定のコマンド グループは、IDE コマンド、製品コマンド、エディター コマンドの 3 つのカテゴリに分類されます。

## <a name="default-ide-commands"></a>既定の IDE コマンド
 既定の IDE ツールバーには、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] に含まれるすべての製品によって共有されるコマンドが含まれています。 これには、 **[保存]** コマンドや **[項目の追加]** コマンドなど、一般的なプロジェクト操作に関連するコマンドが含まれます。 VSPackage では、このツールバーでの追加や削除を行うことはできませんが、例外が 1 つあります。製品または VSPackage で新しいツール ウィンドウを追加する場合は、 **[表示]** メニューの使用可能なツール ウィンドウの一覧にウィンドウを追加する必要があります。 新しい製品または VSPackage では、独自のツールバーを追加できます。

## <a name="default-product-commands"></a>既定の製品コマンド
 各製品では、重要で頻繁に使用されるコマンドを含む独自の既定のツールバーを IDE に提供します。 ただし、可能な場合は常に既存のメニューとツールバーを使用し、必要に応じて、他のタスク固有のツールバーでそれらを補完することをお勧めします。

 ツールバーの [優先度] フィールドによって、その行の配置が決まります。 [優先度ゼロ] にすると、メニューバー (行 1) と **[標準]** ツールバー (行 2) の下にある 3 行目にツールバーが配置されます。 そのため、他のツールバーは行 (優先度 + 3) に表示されます。 空きがある場合は、同じ行に後続のツールバーが配置されます。それ以外の場合は、次の行に自動的に移動されます。

## <a name="default-editor-commands"></a>既定のエディター コマンド
 カスタム エディターを提供する VSPackage には、そのエディターで最も重要で頻繁に使用されるコマンドを含む既定のツールバーが用意されています。 エディターがアクティブになっている場合はエディターのツールバーが表示され、エディターがアクティブでない場合は非表示になります。 この表示は *.vsct* ファイルの `VisibilityConstraints` 要素で制御されます。

 エディターのツールバーは、IDE と製品ツールバーの下に配置する必要があります。

## <a name="see-also"></a>関連項目
- [IDE 定義コマンド、メニュー、およびグループ](../../extensibility/internals/ide-defined-commands-menus-and-groups.md)
- [VSPackage でユーザー インターフェイス要素を追加する方法](../../extensibility/internals/how-vspackages-add-user-interface-elements.md)
