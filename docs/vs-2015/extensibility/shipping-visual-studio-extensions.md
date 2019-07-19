---
title: 拡張機能を出荷 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- VSIX deployment
- deployment, VSIX
- satellite DLLs, in VSIX packages
ms.assetid: 13cd263d-25f7-488e-9c1a-cff908caedb6
caps.latest.revision: 29
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: c7154395be43f6a0b07e9f2557d94fa594ef5ba4
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "68150786"
---
# <a name="shipping-visual-studio-extensions"></a>Visual Studio 拡張機能の配布
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

**注**:Visual Studio ギャラリーは、Visual Studio Marketplace に置き換えられます。 詳細については、このトピックの最新バージョンを参照してください。

拡張機能の開発が完了したらは、他のコンピューターにインストールして、友人や同僚と共有または Visual Studio ギャラリーに発行できます。 このセクションで発行し、拡張機能を維持するために行う必要があるすべての事項を説明します。 .vsix ファイル、公開、ローカライズ、および更新を使用します。

## <a name="working-with-vsix-extensions"></a>VSIX 拡張機能の使用
 VSIX 拡張機能は、空の VSIX プロジェクトを作成し、別の項目テンプレートにして作成できます。 詳細については、次を参照してください。 [VSIX プロジェクト テンプレート](../extensibility/vsix-project-template.md)します。

 VSIX 形式を使用して、パッケージ プロジェクト テンプレート、項目テンプレート、Vspackage、Managed Extensibility Framework (MEF) コンポーネント、**ツールボックス**コントロール、アセンブリ、およびカスタム型 (カスタム スタート ページを含む)。 VSIX 形式では、ファイル ベースの展開を使用します。 VSIX パッケージの詳細については、次を参照してください。 [VSIX パッケージの構造](../extensibility/anatomy-of-a-vsix-package.md)します。

 VSIX 形式は、コード スニペットのインストールをサポートしていません。 グローバル アセンブリ キャッシュ (GAC) またはシステム レジストリへの書き込みなどの他の特定のシナリオもサポートしません。 GAC またはインストールのレジストリに書き込む必要がある場合は、Windows インストーラーを使用する必要があります。 詳細については、次を参照してください。[を準備する拡張機能の Windows インストーラーの配置](../extensibility/preparing-extensions-for-windows-installer-deployment.md)します。

## <a name="publishing-your-extension-to-the-visual-studio-gallery"></a>Visual Studio ギャラリーに、拡張機能を公開します。
 .Vsix ファイルをメールにまたはサーバー上に配置するだけで他のユーザーに拡張機能を配布できます。 多くの人の手でコードを取得する最善の方法で配置するが、 [Visual Studio Marketplace](https://marketplace.visualstudio.com/)します。 Visual Studio ギャラリーの拡張機能での Visual Studio ユーザーに提供**拡張機能と更新**します。 詳細については、「[Visual Studio 拡張機能の検索と使用](../ide/finding-and-using-visual-studio-extensions.md)」を参照してください。

 拡張機能を Visual Studio ギャラリーにアップロードする方法を示す完全な例を参照してください。[チュートリアル。Visual Studio 拡張機能を公開](../extensibility/walkthrough-publishing-a-visual-studio-extension.md)します。

## <a name="private-galleries"></a>Private Galleries
 コントロール、テンプレート、およびツールを開発するときは、イントラネット上のプライベート ギャラリーに投稿することによって、組織と共有することができます。 詳細については、「[プライベート ギャラリー](../extensibility/private-galleries.md)」を参照してください。

## <a name="localizing-your-extension"></a>拡張機能のローカライズ
 さまざまなロケールで、拡張機能をリリースする計画がある場合は、ローカライズすることを検討してください。 手順の詳細については、次を参照してください。 [VSIX パッケージのローカライズ](../extensibility/localizing-vsix-packages.md)します。

## <a name="updating-and-versioning-your-extension"></a>更新とバージョン管理、拡張機能
 拡張機能を公開したら、更新する必要がある場合にして提供されます。 Visual Studio ギャラリーにパブリッシュされている拡張機能を更新する方法を調べるを参照してください。[方法。拡張機能を更新](../extensibility/how-to-update-a-visual-studio-extension.md)します。

 Visual Studio の複数のバージョンをサポートするために、拡張機能を設定することができます。 詳細については、次を参照してください。[をサポートしている複数のバージョンの Visual Studio](../extensibility/supporting-multiple-versions-of-visual-studio.md)します。

## <a name="related-topics"></a>関連トピック

|タイトル|説明|
|-----------|-----------------|
|[VSIX プロジェクトのテンプレートの概要](../extensibility/getting-started-with-the-vsix-project-template.md)|カスタム プロジェクト テンプレートをインストールする VSIX プロジェクト テンプレートを使用する方法について説明します。|
|[VSIX パッケージの構造](../extensibility/anatomy-of-a-vsix-package.md)|VSIX パッケージのコンポーネントについて説明します。|
|[VSIX プロジェクト テンプレート](../extensibility/vsix-project-template.md)|パッケージ化し、拡張機能を公開する方法についての詳細な手順について説明します。|
|[VSIX パッケージのローカライズ](../extensibility/localizing-vsix-packages.md)|Extension.vsixlangpack ファイルを使用して、インストール プロセスのローカライズされたテキストを提供する方法について説明します。|
|[方法: 拡張機能を更新する](../extensibility/how-to-update-a-visual-studio-extension.md)|システムに拡張機能を更新する方法と更新プログラムを既存の Visual Studio 拡張機能をデプロイする方法について説明します。|
|[方法: VSIX パッケージへの依存関係の追加](../extensibility/how-to-add-a-dependency-to-a-vsix-package.md)|VSIX 展開パッケージへの参照を追加する方法について説明します。|
|[Windows インストーラーの配置に関する拡張機能を準備する](../extensibility/preparing-extensions-for-windows-installer-deployment.md)|Windows インストーラーで、拡張機能をデプロイする方法について説明します。|
|[VSIX パッケージの署名](../extensibility/signing-vsix-packages.md)|VSIX パッケージに署名する方法をについて説明します。|
|[プライベート ギャラリー](../extensibility/private-galleries.md)|拡張機能のプライベート ギャラリーを作成する方法について説明します。|
|[複数バージョンの Visual Studio をサポートする](../extensibility/supporting-multiple-versions-of-visual-studio.md)|複数のバージョンの Visual Studio には、拡張機能のサポート方法を示します。|
