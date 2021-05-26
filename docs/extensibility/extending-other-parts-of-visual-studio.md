---
title: Visual Studio の他の部分の拡張 | Microsoft Docs
description: 拡張できる Visual Studio UI の部分について説明します。 VSPackage を作成し、アクティビティ ログに書き込み、ツールボックスとステータス バーを拡張することができます。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- user interfaces
ms.assetid: 27d2f1e1-2503-4aca-9cfc-707abd07ccf0
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 193fb335ffd2d57eab1aebedc5ea0114738f72eb
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105075238"
---
# <a name="extend-other-parts-of-visual-studio"></a>Visual Studio の他の部分を拡張する

Visual Studio UI の他の多くの部分を拡張できます。 ここでは、ほんの一部を紹介します。

## <a name="create-a-vspackage"></a>VSPackage を作成する

Visual Studio 機能拡張の基本構成要素は VSPackage です。  VSPackage を追加する方法を確認します。「[VSPackage を使用して拡張機能を作成する](../extensibility/creating-an-extension-with-a-vspackage.md)」

## <a name="extend-the-toolbox"></a>ツールボックスを拡張する

新しいコントロールやその他の項目をツールボックスに追加する方法と、ツールボックス機能の使用方法を確認します。

- [WPF ツールボックス コントロールの作成](../extensibility/creating-a-wpf-toolbox-control.md)

- [Windows フォーム ツールボックス コントロールの作成](../extensibility/creating-a-windows-forms-toolbox-control.md)

## <a name="extend-the-status-bar"></a>ステータス バーを拡張する

ステータス バーと進行状況バーの読み取りと書き込みを行う方法、およびアニメーションとその他の UI を提供する方法を確認します。「[ステータス バーを拡張する](../extensibility/extending-the-status-bar.md)」

::: moniker range="vs-2017"

## <a name="create-custom-start-pages"></a>カスタム スタート ページを作成する

最初から、またはダウンロード可能なスタート ページのサンプルから、独自のスタート ページを作成する方法を確認します。「[カスタム スタート ページの作成](../extensibility/creating-a-custom-start-page.md)」

::: moniker-end

## <a name="write-to-the-activity-log"></a>アクティビティ ログへの書き込み

アクティビティ ログへの書き込み方法について確認します。「[方法: アクティビティ ログを使用する](../extensibility/how-to-use-the-activity-log.md)」
