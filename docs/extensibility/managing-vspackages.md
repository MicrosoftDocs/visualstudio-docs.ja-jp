---
title: VSPackage の管理 | Microsoft Docs
description: Visual Studio によって提供される既定の VSPackage 管理を簡単に使用できるタイミングと、これをカスタマイズする方法とタイミングがわかるように、VSPackage の管理について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- VSPackages, autoloading
- VSPackages, delayed loading
- delay loading
- VSPackages, loading
ms.assetid: 386e0ce5-4107-4164-b0cd-1cf43eb5e7cf
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: a62581e036b70a10db533dc46d0787cd558afe29
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105090630"
---
# <a name="manage-vspackages"></a>VSPackage を管理する
ほとんどの場合、VSpackage の管理について心配する必要はありません。プロジェクトと項目テンプレートによってパッケージが自動的に登録されて読み込まれるためです。 ただし、状況によっては、パッケージを管理するためにもう少し学習が必要になる場合があります。

## <a name="use-the-experimental-instance"></a>実験用インスタンスを使用する
 実験用インスタンスの詳細については、「[実験用インスタンス](../extensibility/the-experimental-instance.md)」を参照してください。

## <a name="register-and-unregister-vspackages"></a>VSpackage を登録および登録解除する
 VSpackage とその他の種類の拡張機能を登録および登録解除する方法については、[VSPackage の登録および登録解除](../extensibility/registering-and-unregistering-vspackages.md)に関するページを参照してください。

## <a name="load-a-vspackage"></a>VSPackage を読み込む
 VSpackage は、特定の CMDUICONTEXT GUID が有効になっている場合に自動読み込みするように設定できます。 詳細については、[VSPackage を読み込む](../extensibility/loading-vspackages.md)に関するページを参照してください。

## <a name="use-asyncpackage-to-load-vspackages-in-the-background"></a>AsyncPackage を使用してバックグラウンドで VSPackage を読み込む
 `AsyncPackage` クラスでは、Visual Studio での UI の応答性を向上させるために、バックグラウンド スレッドでのパッケージの読み込みを有効にします。 詳細については、「[方法: AsyncPackage を使用してバックグラウンドで VSPackage を読み込む](../extensibility/how-to-use-asyncpackage-to-load-vspackages-in-the-background.md)」を参照してください。

## <a name="rule-based-ui-context-for-extensions"></a>拡張機能のルール ベースの UI コンテキスト
 ルール ベースの UI コンテキストを使用すると、拡張機能の作成者は、UI コンテキストがアクティブ化され、関連付けられている VSpackage が読み込まれる正確な条件を定義できます。 詳細については、「[方法: Visual Studio 拡張機能のルール ベースの UI コンテキストを使用する](../extensibility/how-to-use-rule-based-ui-context-for-visual-studio-extensions.md)」を参照してください。

## <a name="diagnose-extension-performance"></a>拡張機能のパフォーマンスを診断する
拡張機能は、起動とソリューションの読み込みのパフォーマンスに影響を与える可能性があります。 Visual Studio 拡張機能の影響がどのように計算されるかと、拡張機能がパフォーマンスに影響する拡張機能として表示されるかどうかをテストするためにローカルで分析する方法について説明します。 詳細については、「[方法: 拡張機能のパフォーマンスを診断する](how-to-diagnose-extension-performance.md)」を参照してください。

## <a name="troubleshoot-vspackages"></a>VSpackage のトラブルシューティング
 読み込まれない、またはエラーが発生している VSpackage のトラブルシューティングの手法については、「[VSPackage のトラブルシューティング](../extensibility/troubleshooting-vspackages.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [VSPackages](../extensibility/internals/vspackages.md)
