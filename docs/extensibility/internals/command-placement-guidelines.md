---
title: コマンド配置のガイドライン |Microsoft Docs
description: Visual Studio 統合開発環境 (IDE) でコマンドを配置するためのガイドラインとベスト プラクティスについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- commands, small command sets
- small command sets
- command sets
ms.assetid: 63b3478e-e08a-420b-a0ec-76767e0cb289
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 46aa6c341313a9d7c9d0a6d1666130d799ddc277
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105057326"
---
# <a name="command-placement-guidelines"></a>コマンド配置のガイドライン
Visual Studio 統合開発環境 (IDE) でのコマンドの配置に関するベストプラクティスは、コマンド セットのサイズによって異なります。 コマンドは、 *.vsct* ファイル内の情報に従って定義され、配置されます。

## <a name="best-practices-for-all-command-sets"></a>すべてのコマンド セットのベスト プラクティス
 コマンドのすべてのセットについて、次のガイドラインに従ってください。

- コマンド構造のグラフを事前に準備します。 複数の場所で使用されるコマンド、コンボ ボックス、コマンド グループ、およびショートカット メニューを識別します。

- 同じグループに表示されるコマンドは、関連付けられている必要があります。

- 1 つのコマンドだけを含むグループは許容されます。

- パッケージでは、既存の Visual Studio メニューに多数のコマンドを追加することはできません。 代わりに、新しいコマンドをホストするメニューまたはサブメニューを作成する必要があります。

- 既存のメニューにコマンドを配置する場合は、その目的が明確になるよう名前を付け、既存のコマンドと混同しないようにします。

## <a name="best-practices-for-small-command-sets"></a>小さなコマンド セットのベスト プラクティス
 いくつかのコマンドを含む VSPackage を開発している場合は、次のガイドラインに従うこともできます。

- 可能であれば、コマンド、コンボ ボックス、グループ、または子メニューの[親](../../extensibility/parent-element.md)要素を使用して、適切なグループに配置します。

- これらのグループを VSPackage によって表示されるメニューに割り当てます。

- 子メニューまたはコマンドの親は、[Group](../../extensibility/group-element.md) 要素である必要があります。 コマンドと子メニューをグループに割り当ててから、そのグループを親メニューに割り当てます。

- コマンドの定義の後に [CommandPlacements](../../extensibility/commandplacements-element.md) 要素セクションを追加し、`CommandPlacements` 要素に追加の各グループの [CommandPlacements](../../extensibility/commandplacement-element.md) 要素を追加することで、コマンドを追加のグループに配置できます。

## <a name="best-practices-for-large-command-sets"></a>大きなコマンド セットのベスト プラクティス
 VSPackage に複数のコンテキストで表示される多数のコマンドが含まれる場合は、次のガイドラインにも従います。

- メニュー、グループ、コマンドをセルフ ペアレンティングします。 つまり、項目の定義に `Parent` 要素を割り当てないでください。

- `CommandPlacements` 要素セクションの `CommandPlacement` 要素エントリを使用して、メニュー、グループ、およびコマンドを親メニューおよびグループに配置します。

- `CommandPlacements` 要素セクションでは、特定のメニューまたはグループに入力するエントリを互いに隣接させる必要があります。 これにより、読みやすさが向上し、`Priority` 優先度付けがより簡単に判断できるようになります。

## <a name="see-also"></a>関連項目
- [VSPackage でユーザー インターフェイス要素を追加する方法](../../extensibility/internals/how-vspackages-add-user-interface-elements.md)
- [Visual Studio コマンド テーブル (.vsct) ファイル](../../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
