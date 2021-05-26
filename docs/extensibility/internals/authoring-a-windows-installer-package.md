---
title: Windows インストーラー パッケージの編集 | Microsoft Docs
description: ファイルとレジストリのデータを含むデータベース テーブルで構成される Visual Studio の Windows インストーラー パッケージを編集する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- .msi files, VSPackages
- msi files, VSPackages
ms.assetid: 0ce7c21d-0d3f-47fe-a0bb-eed506e32609
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: afc21237b72d76b73e619740cab0b196e29e928d
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105078956"
---
# <a name="author-a-windows-installer-package"></a>Windows インストーラー パッケージを編集する
Windows インストーラー モデルは、データに基づいて処理されます。 たとえば、ファイルをコピーしてレジストリ エントリを書き込むための手続き型スクリプトを記述するのではなく、ファイルとレジストリのデータを含むデータベース テーブルの行と列を編集します。

## <a name="database-entries"></a>データベース エントリ
VSPackage をインストールするには、Windows インストーラー パッケージに次のタスクを実行するためのデータベース エントリが含まれている必要があります。

- システムを検索して、VSPackage でサポートされる [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] のバージョンを探します (AppSearch、CompLocator、RegLocator、DrLocator、Signature を含む Windows インストーラー テーブルを使用します)。

- サポートされているバージョンの [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] がインストールされていない場合、または VSPackage の別のシステム要件が満たされていない場合、インストールをキャンセルします (LaunchCondition テーブルを使用)。

- VSPackage ファイルと依存ファイルをインストールします (ディレクトリ、コンポーネント、ファイル テーブルを使用)。

- VSPackage の適切な情報をレジストリに追加します (レジストリ テーブルを使用)。

- **devenv.exe /setup** を呼び出して、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] に VSPackage を統合します (CustomAction テーブルを使用)。

詳細については、「[Windows インストーラー](/windows/desktop/Msi/windows-installer-portal)」を参照してください。

## <a name="setup-tools"></a>セットアップ ツール
さまざまなサードパーティ製セットアップ ツールによって、Windows インストーラー パッケージの開発環境が提供されます。 次の無料のツールを使用できます。

- InstallShield Limited Edition

   Visual Studio の **[新しいプロジェクト]** ダイアログ ボックスでは、InstallShield の限定バージョンを取得できます。 **[その他のプロジェクトの種類]** を展開し、 **[セットアップと配置]** を選択します。 InstallShield テンプレートを選択します。

- Windows インストーラー XML (WiX) ツールセット

   Windows インストーラー XML (WiX) ツールセットでは、XML ソース ファイルから Windows インストーラー パッケージをビルドします。 WiX ツールセットは、Microsoft オープンソース プロジェクトです。 [Wix ツールセット](https://sourceforge.net/projects/wix/)からソース コードと実行可能ファイルをダウンロードできます。

   [!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)] を使用して [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] に統合する商用製品の場合は、「[Visual Studio Marketplace](https://marketplace.visualstudio.com/)」を参照してください。

## <a name="see-also"></a>関連項目
- [Windows インストーラーによる VSPackage のインストール](../../extensibility/internals/installing-vspackages-with-windows-installer.md)
