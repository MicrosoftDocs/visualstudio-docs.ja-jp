---
title: サイド バイ サイド IDE 用のファイル名拡張子の登録
description: サイド バイ サイド配置のためにファイル名拡張子を登録する方法について説明します。これにより、ユーザーは適切なバージョンの Visual Studio でファイルを開くことができます。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- file extensions, registering for side-by-side
ms.assetid: 9ab046a2-147d-4167-aa14-7d661b1eaaa5
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: ad6b5715b767729715403d064cd46b4556fa17e3
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105056559"
---
# <a name="register-file-name-extensions-for-side-by-side-deployments"></a>サイド バイ サイドの配置に対してファイル名拡張子を登録する
サイド バイ サイドの環境で配置された VSPackage では、ファイル名拡張子を登録して、ファイルを正しいバージョンの [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] に関連付ける必要があります。 バージョン固有のファイル名拡張子を使用しない限り、登録によって、ユーザーは適切なバージョンの [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] でプロジェクトおよびプロジェクト項目ファイルを開くことができます。

## <a name="in-this-section"></a>このセクションの内容
- [ファイル名拡張子について](../extensibility/about-file-name-extensions.md)では、ファイル名拡張子の登録方法について説明します。

- [ファイル名拡張子のファイル ハンドラーを指定する](../extensibility/specifying-file-handlers-for-file-name-extensions.md)では、特定のファイル名拡張子を開いたり、編集したりできるアプリケーションを登録する方法について説明します。

- [ファイル名拡張子に動詞を登録する](../extensibility/registering-verbs-for-file-name-extensions.md)では、動詞を登録する方法について説明します。

- [サイド バイ サイドのファイルの関連付けの管理](../extensibility/managing-side-by-side-file-associations.md)では、ファイルを開くために、特定のバージョンの [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] を呼び出すサイド バイ サイド インストールを処理する方法について説明します。

## <a name="related-sections"></a>関連項目
- [複数バージョンの Visual Studio をサポートする](../extensibility/supporting-multiple-versions-of-visual-studio.md)では、開発中やエンド ユーザーへの配置中に発生する、複数のバージョンの [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] や VSPackage に関連する問題について説明します。
