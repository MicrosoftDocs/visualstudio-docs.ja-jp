---
title: Windows インストーラーを使用した VSPackage のインストール | Microsoft Docs
description: Microsoft Windows インストーラーを使用して、VSPackage とその依存ファイルをインストールし、それらを登録して Visual Studio に統合する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- installation [Visual Studio SDK], with Windows Installer
- VSPackages, deploying
ms.assetid: 41d2c72c-0a97-4fcd-b3aa-33a8d3aa962a
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 1638f6d041dda28ca79492ba2c8e6ef772ce8bc7
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105074667"
---
# <a name="installing-vspackages-with-windows-installer"></a>Windows インストーラーによる VSPackage のインストール
VSPackage を [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] に統合するには、ユーザーのコンピューターにファイルをコピーするだけでは不十分です。 VSPackage のインストーラーで VSPackage とその依存ファイルをインストールし、それらを登録して [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] に統合する必要があります。 VSPackage では、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] スプラッシュ スクリーンと [バージョン情報] ダイアログ ボックスでのアイコンの表示などの統合機能を利用できます。

 Microsoft Windows インストーラーのファイルは、VSPackage を配布するための推奨される方法です。 使いやすい Windows インストーラー パッケージは、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] でサポートされているどの Windows オペレーティング システムでも実行できます。 詳細については、「[Windows インストーラー](/previous-versions/2kt85ked(v=vs.120))」を参照してください。

## <a name="in-this-section"></a>このセクションの内容
- [Windows インストーラーの基本事項](../../extensibility/internals/windows-installer-basics.md)

 Windows インストーラーの概要について示します。

- [VSPackage のセットアップ シナリオ](../../extensibility/internals/vspackage-setup-scenarios.md)

 VSPackage と [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] の両方のサイドバイサイド インストールをサポートするための、さまざまな方法について説明します。

- [Windows インストーラー パッケージの編集](../../extensibility/internals/authoring-a-windows-installer-package.md)

 インストーラーで VSPackage を正しくインストールして [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] に統合するために従う一般的な手順の概要について説明します。

- [システム要件の検出](../../extensibility/internals/detecting-system-requirements.md)

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]VSPackage の要件が満たされていない場合に、インストーラーでコンポーネントとそのコンポーネントを検出し、セットアップをキャンセルする方法について説明します。

- [コンポーネント管理](../../extensibility/internals/component-management.md)

 以前の製品バージョンの整合性を維持するインストーラーを開発する方法について説明します。

- [VSPackage のインストール ディレクトリの選択](../../extensibility/internals/choosing-the-installation-directory-for-a-vspackage.md)

 VSPackage を検索するためのオプションの概要を示します。

- [VSPackage の登録](../../extensibility/internals/vspackage-registration.md)

 インストール時に VSPackage を登録する方法と、自己登録が適切ではない理由について説明します。

- [プロジェクト タイプの配置](../../extensibility/internals/deploying-project-types.md)

 マネージドコード プロジェクト タイプに新しいプロジェクトタイプ アグリゲーターを使用する方法について説明します。

- [方法: インストーラー向けの登録情報の生成](../../extensibility/internals/how-to-generate-registry-information-for-an-installer.md)

 RegPkg.exe を使用して、マネージド VSPackage の登録マニフェストを生成する方法について説明します。

- [インストール後に実行する必要があるコマンド](../../extensibility/internals/commands-that-must-be-run-after-installation.md)

 インストール後のコマンドを実行して VSPackage を [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] に統合する方法について説明します。

- [Windows インストーラーによる VSPackage のアンインストール](../../extensibility/internals/uninstalling-a-vspackage-with-windows-installer.md)

 ユーザーが VSPackage をアンインストールするときにインストーラーで実行する必要がある手順について説明します。