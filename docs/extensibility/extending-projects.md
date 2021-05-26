---
title: プロジェクトの拡張 | Microsoft Docs
description: Visual Studio SDK で独自のカスタム プロジェクト タイプを作成する方法と、さまざまな種類の Visual Studio ソリューションを管理する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- solutions [Visual Studio]
- projects [Visual Studio]
ms.assetid: 096d273d-4fe9-4f24-9b00-470bfbdf4bdf
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: c3d4b962475e2f0705d8a46624a8f47d802ff2f4
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105075160"
---
# <a name="extend-projects"></a>プロジェクトを拡張する
プロジェクトとソリューションは、Visual Studio によって、コードおよびリソース ファイルがコンパイルおよびデプロイ単位に編成される方法です。 プロジェクトの詳細については、「[プロジェクト (Visual Studio SDK)](../extensibility/extending-projects.md)」を参照してください。

 独自のプロジェクト タイプを作成するには、Visual Studio SDK とプロジェクト用 Managed Package Framework を使用します。これは、「[プロジェクト用 Managed Package Framework ](https://github.com/tunnelvisionlabs/MPFProj10)」でダウンロードできます。 カスタム プロジェクトの実装方法を理解するには、「[新しいプロジェクトの生成: 内部的な処理、パート 1](../extensibility/internals/new-project-generation-under-the-hood-part-one.md)」と「[新しいプロジェクトの生成: 内部的な処理、パート 2](../extensibility/internals/new-project-generation-under-the-hood-part-two.md)」を参照してください。

 このセクションのトピックでは、カスタム プロジェクトを作成する方法と、さまざまな種類の Visual Studio ソリューションを管理する方法について説明します。

## <a name="in-this-section"></a>このセクションの内容
- 「[基本プロジェクト システムを作成する (第 1 部)](../extensibility/creating-a-basic-project-system-part-1.md)」カスタム プロジェクト システムを作成する方法について説明します。

- 「[基本的なプロジェクト システムを作成する (第 2 部)](../extensibility/creating-a-basic-project-system-part-2.md)」カスタム プロジェクト システムを作成する方法について説明します。

- 「[プロジェクト ファイルにデータを保存する](../extensibility/saving-data-in-project-files.md)」プロジェクト (<em>.</em>proj*) ファイルに追加する方法について説明します。

- 「[実行時にプロジェクトのサブタイプを確認する](../extensibility/verifying-subtypes-of-a-project-at-run-time.md)」実行時にプロジェクトのサブタイプを確認する方法について説明します。

- 「[プロパティ ページの追加と削除](../extensibility/adding-and-removing-property-pages.md)」カスタム プロジェクトのプロパティ ページをカスタマイズする方法について説明します。

- 「[プロジェクト項目に属性を追加する](../extensibility/adding-an-attribute-to-a-project-item.md)」カスタム プロジェクト項目に属性を追加する方法について説明します。

- 「[プロジェクト項目のプロパティを保持する](../extensibility/persisting-the-property-of-a-project-item.md)」カスタム プロジェクト項目のプロパティを永続化する方法について説明します。

- 「[ユニバーサル Windows プロジェクトを管理する](../extensibility/managing-universal-windows-projects.md)」ユニバーサル プロジェクトを管理する方法について説明します。
