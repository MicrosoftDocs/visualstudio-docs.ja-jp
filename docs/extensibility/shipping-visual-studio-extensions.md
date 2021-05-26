---
title: Visual Studio 拡張機能の配布 | Microsoft Docs
description: .vsix ファイルの使用、公開、ローカライズ、更新など、Visual Studio SDK 拡張機能を公開および管理する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- VSIX deployment
- deployment, VSIX
- satellite DLLs, in VSIX packages
ms.assetid: 13cd263d-25f7-488e-9c1a-cff908caedb6
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: c88c80ffbc1e80815b8370a940a75c0eb197ff78
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105090136"
---
# <a name="shipping-visual-studio-extensions"></a>Visual Studio 拡張機能の配布
拡張機能の開発が完了したら、他のコンピューターにインストールしたり、友人や同僚と共有したり、Visual Studio Marketplace に公開したりすることができます。 このセクションでは、拡張機能を公開して管理するために必要なすべてのこと (.vsix ファイルの使用、公開、ローカライズ、更新) について説明します。

## <a name="working-with-vsix-extensions"></a>VSIX 拡張機能の使用
 VSIX 拡張機能を作成するには、空の VSIX プロジェクトを作成してから、別の項目テンプレートを追加します。 詳細については、「[VSIX プロジェクト テンプレート](../extensibility/vsix-project-template.md)」を参照してください。

 VSIX 形式を使用すると、プロジェクト テンプレート、項目テンプレート、VSPackage、Managed Extensibility Framework (MEF) コンポーネント、**ツールボックス** コントロール、アセンブリ、カスタム型 (これには、Visual Studio 2017 のカスタム スタート ページが含まれます) をパッケージ化できます。 VSIX 形式では、ファイル ベースのデプロイが使用されます。 VSIX パッケージの詳細については、「[VSIX パッケージの構造](../extensibility/anatomy-of-a-vsix-package.md)」を参照してください。

 VSIX 形式では、コード スニペットのインストールはサポートされていません。 また、グローバル アセンブリ キャッシュ (GAC) またはシステム レジストリへの書き込みなど、他の特定のシナリオもサポートされません。 インストールで GAC またはレジストリに書き込む必要がある場合は、Windows インストーラーを使用する必要があります。 詳細については、「[Windows インストーラーのデプロイに関する拡張機能を準備する](../extensibility/preparing-extensions-for-windows-installer-deployment.md)」を参照してください。

## <a name="publishing-your-extension-to-the-visual-studio-marketplace"></a>拡張機能を Visual Studio Marketplace に公開する
 拡張機能を他のユーザーに配布するには、単に .vsix ファイルを郵送するかサーバーに配置します。 しかし、コードが多くの人の手に渡るようにする最善の方法は、[Visual Studio Marketplace](https://marketplace.visualstudio.com/vs) に配置することです。 **拡張機能と更新プログラム** を使用して Visual Studio ユーザーが Visual Studio Marketplace 拡張機能を使用できるようになります。 詳細については、「[Visual Studio 拡張機能の検索と使用](../ide/finding-and-using-visual-studio-extensions.md)」を参照してください。

 拡張機能を Visual Studio Marketplace にアップロードする方法を示す完全な例については、「[チュートリアル: Visual Studio の拡張機能を公開する](../extensibility/walkthrough-publishing-a-visual-studio-extension.md)」を参照してください。

## <a name="private-galleries"></a>Private Galleries
 コントロール、テンプレート、ツールを開発するときに、イントラネット上のプライベート ギャラリーに投稿することで、それらを組織と共有できます。 詳細については、「[プライベート ギャラリー](../extensibility/private-galleries.md)」を参照してください。

## <a name="localizing-your-extension"></a>拡張機能のローカライズ
 拡張機能を別のロケールでリリースする予定の場合は、ローカライズすることを検討する必要があります。 何が必要かについては、「[VSIX パッケージのローカライズ](../extensibility/localizing-vsix-packages.md)」を参照してください。

## <a name="updating-and-versioning-your-extension"></a>拡張機能の更新とバージョン管理
 拡張機能を公開した後、更新する必要が生じる時が来ます。 Visual Studio Marketplace で公開されている拡張機能を更新する方法については、「[方法: 拡張機能を更新する](../extensibility/how-to-update-a-visual-studio-extension.md)」を参照してください。

 拡張機能は、複数バージョンの Visual Studio をサポートするように設定できます。 詳細については、「[複数バージョンの Visual Studio をサポートする](../extensibility/supporting-multiple-versions-of-visual-studio.md)」を参照してください。

## <a name="related-topics"></a>関連トピック

|Title|説明|
|-----------|-----------------|
|[VSIX プロジェクトのテンプレートの概要](../extensibility/getting-started-with-the-vsix-project-template.md)|VSIX プロジェクト テンプレートを使用してカスタム プロジェクト テンプレートをインストールする方法について説明します。|
|[VSIX パッケージの構造](../extensibility/anatomy-of-a-vsix-package.md)|VSIX パッケージのコンポーネントについて説明します。|
|[VSIX プロジェクト テンプレート](../extensibility/vsix-project-template.md)|拡張機能をパッケージ化および公開する詳しい手順について説明します。|
|[VSIX パッケージのローカライズ](../extensibility/localizing-vsix-packages.md)|extension.vsixlangpack ファイルを使用して、インストール プロセスのローカライズされたテキストを提供する方法について説明します。|
|[方法: 拡張機能を更新する](../extensibility/how-to-update-a-visual-studio-extension.md)|システムの拡張機能を更新する方法と、既存の Visual Studio 拡張機能に更新プログラムをデプロイする方法について説明します。|
|[方法: VSIX パッケージへの依存関係の追加](../extensibility/how-to-add-a-dependency-to-a-vsix-package.md)|VSIX デプロイ パッケージに参照を追加する方法について説明します。|
|[Windows インストーラーの配置に関する拡張機能を準備する](../extensibility/preparing-extensions-for-windows-installer-deployment.md)|Windows インストーラーを使用して拡張機能をデプロイする方法について説明します。|
|[VSIX パッケージの署名](../extensibility/signing-vsix-packages.md)|VSIX パッケージに署名する方法について説明します。|
|[プライベート ギャラリー](../extensibility/private-galleries.md)|拡張機能用のプライベート ギャラリーを作成する方法について説明します。|
|[複数バージョンの Visual Studio をサポートする](../extensibility/supporting-multiple-versions-of-visual-studio.md)|拡張機能で複数バージョンの Visual Studio をサポートする方法を示します。|
|[Visual Studio の検出](locating-visual-studio.md)|Visual Studio インスタンスでカスタム拡張機能のデプロイを検索する方法について説明します。|
