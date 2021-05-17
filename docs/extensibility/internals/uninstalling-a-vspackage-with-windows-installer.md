---
title: Windows インストーラーによる VSPackage のアンインストール | Microsoft Docs
description: Windows インストーラーでは、インストールを逆にすることで VSPackage をアンインストールできます。 Windows インストーラー パッケージでカスタム アクションを処理する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- packages, uninstalling
- VSPackages, uninstalling
- uninstalling VSPackages
ms.assetid: c4575ac7-82da-4af8-a375-ea756a101fbf
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: bb5d0fe0e4812d66f6981ea58dfb51f19336d98b
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105090721"
---
# <a name="uninstalling-a-vspackage-with-windows-installer"></a>Windows インストーラーによる VSPackage のアンインストール
ほとんどの場合、Windows インストーラーでは、VSPackage をインストールするために実行したことを "元に戻す" だけで、VSPackage をアンインストールできます。 [インストール後に実行する必要のあるコマンド](../../extensibility/internals/commands-that-must-be-run-after-installation.md)に関するページで説明されているカスタム アクションは、アンインストール後にも実行する必要があります。 devenv.exe の呼び出しは、インストールとアンインストールの両方の InstallFinalize 標準アクションの直前に行われるため、CustomAction と InstallExecuteSequence テーブル エントリは両方のケースに対応します。

> [!NOTE]
> MSI パッケージをアンインストールした後で、`devenv /setup` を実行します。

 一般的なルールとして、Windows インストーラー パッケージにカスタム アクションを追加する場合は、アンインストールおよびロールバック時にそれらのアクションを処理する必要があります。 たとえば、VSPackage を自己登録するカスタム アクションを追加する場合は、それを登録解除するカスタム アクションも追加する必要があります。

> [!NOTE]
> ユーザーは、VSPackage をインストールしてから、統合されている [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] のバージョンをアンインストールすることができます。 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] の依存関係があるコードを実行するカスタム アクションを排除することで、そのシナリオで VSPackage のアンインストールが確実に機能するようにすることができます。

## <a name="handling-launch-conditions-at-uninstall-time"></a>アンインストール時に起動条件を処理する
 LaunchConditions 標準アクションは、LaunchCondition テーブルの行を読み取って、条件が満たされていない場合はエラー メッセージを表示します。 起動条件は、一般的にシステム要件が満たされていることを確認するために使用されるため、通常、LaunchCondition テーブルの LaunchConditions 行に条件 `NOT Installed` を追加することによって、アンインストール中に起動条件をスキップできます。

 別の方法は、アンインストール中に重要でない起動条件に `OR Installed` を追加することです。 これにより、アンインストール中に条件が常に true になるため、起動条件のエラー メッセージは表示されません。

> [!NOTE]
> `Installed` は、VSPackage がシステムに既にインストールされていることを検出したときに Windows インストーラーが設定するプロパティです。

## <a name="see-also"></a>関連項目
- [Windows インストーラー](/previous-versions/ee231230(v=vs.100))
- [システム要件の検出](../../extensibility/internals/detecting-system-requirements.md)