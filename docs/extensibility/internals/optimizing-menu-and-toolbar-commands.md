---
title: メニューおよびツール バー コマンドの最適化 | Microsoft Docs
description: Visual Studio で、VSPackage とそれらに対応するコマンドを追加するこによって発生するコマンドの混乱を最小限に抑える方法について学習します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- commands [Visual Studio], menus
- commands [Visual Studio], toolbars
- menus [Visual Studio SDK], commands
- menu commands, implementing
- toolbars [Visual Studio], commands
ms.assetid: 8385f1a6-1e98-4dca-83d2-fcbed7177242
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 9c7d289f9dadf7b3442f937c5b50cf038c802516
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105063059"
---
# <a name="optimizing-menu-and-toolbar-commands"></a>メニュー、ツール バー コマンドの最適化
[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] に VSPackage とそれらに対応するコマンドが追加されると、UI が過密になる可能性があります。 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] では、UI コマンドの混乱を最小限に抑えるのに役立つ方法が提供されます。

## <a name="in-this-section"></a>このセクションの内容
- [コマンドを使用可能にする](../../extensibility/internals/making-commands-available.md)

 VSPackage を追加したときに [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] UI の過密を最小限に抑えるための一般的なガイドラインを提供します。

- [配置のガイドライン](../../extensibility/internals/command-placement-guidelines.md)

 コマンド セットのサイズに従って VSPackage を実装するための特定のガイドラインを提供します。

## <a name="related-sections"></a>関連項目
- [コマンド、メニュー、およびツール バー](../../extensibility/internals/commands-menus-and-toolbars.md)

 メニュー、ツール バー、およびコマンド コンボ ボックスが含まれている UI を作成する方法について説明します。
