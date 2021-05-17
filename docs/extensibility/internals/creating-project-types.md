---
title: プロジェクト タイプの作成 | Microsoft Docs
description: プログラミング タスクをサポートする新しいプロジェクト タイプを設計、作成、および登録して、Visual Studio を拡張する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- project types, new
- projects [Visual Studio SDK], new project types
ms.assetid: bdb2d22e-d622-450c-bb2d-98152a745fcf
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 5984afd2879f94a73ef02f77a85501c50f55bc93
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105056819"
---
# <a name="create-project-types"></a>プロジェクト タイプの作成
新しいプロジェクト タイプを作成して、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] を拡張できます。 新しいプロジェクト タイプを作成するには、いくつかの概念を理解し、いくつかの手順を完了する必要があります。 次のトピックでは、プロジェクト タイプの作成方法の概要を示します。

## <a name="in-this-section"></a>このセクションの内容
- [プロジェクト タイプのデザインの方針](../../extensibility/internals/project-type-design-decisions.md)

 項目、プロジェクト ファイルの永続化、およびコミットメントのメカニック設計の決定について説明します。これらの決定は、新しいプロジェクト タイプを作成する前に行う必要があります。

- [チェック リスト: 新しいプロジェクト タイプの作成](../../extensibility/internals/checklist-creating-new-project-types.md)

 プロジェクトでのコードの編集、アプリケーションのコンパイル、ビルド、デバッグ、デプロイなどのようなプログラミング タスクをサポートする新しいプロジェクト タイプを作成するために従う必要がある手順の概要を示します。

- [プロジェクト ファクトリを使用したプロジェクト インスタンスの作成](../../extensibility/internals/creating-project-instances-by-using-project-factories.md)

 プロジェクト ファクトリを提供および使用して、新しいプロジェクトのインスタンスを作成する方法について説明します。

- [プロジェクト タイプの登録](../../extensibility/internals/registering-a-project-type.md)

 既定のパスとデータを提供する、レジストリからのステートメントのコード サンプルと、各ステートメントのレジストリ スクリプトからのエントリを含む表を示します。

- [プロジェクトの永続化](../../extensibility/internals/project-persistence.md)

 ファイルベースと非ファイルベースの両方のプロジェクト オブジェクトを永続化するための、`IPersistFileFormat` の使用方法について説明します。

- [MSBuild の使用](../../extensibility/internals/using-msbuild.md)

 プロジェクト タイプでは、[!INCLUDE[vstecmsbuild](../../extensibility/internals/includes/vstecmsbuild_md.md)] ビルド エンジンを使用でき、ユーザーは [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] からおよびコマンド ラインでビルドを行えるようになります。この方法について説明します。

## <a name="related-sections"></a>関連項目
- [シンボル参照ツールのサポート](../../extensibility/internals/supporting-symbol-browsing-tools.md)

 **オブジェクト ブラウザー**、**クラス ビュー** ウィンドウなどのコード表示ツールのアーキテクチャについて説明します。 VSPackage にオブジェクトの参照を実装するために使用されるインターフェイスとメソッドについて説明します。

- [プロジェクト テンプレートとプロジェクト項目テンプレートの追加](../../extensibility/internals/adding-project-and-project-item-templates.md)

 プロジェクト項目が開かれたときにどのエディターが使用されるのかと、プロジェクト リソースをどのように操作できるのかを決定するときに、プロジェクトが果たす意義について説明します。

- [Windows インストーラーによる VSPackage のインストール](../../extensibility/internals/installing-vspackages-with-windows-installer.md)

 お客様へのデプロイのために、VSPackage に独自の一意の ID を付与する方法と、VSPackage の DLL およびその他の情報を Windows インストーラー パッケージ ( *.MSI* ファイル) にラップする方法について説明します。

- [Visual Studio での階層](../../extensibility/internals/hierarchies-in-visual-studio.md)

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] によって、階層が表示および処理される方法について説明します。

- [VSPackages](../../extensibility/internals/vspackages.md)

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 環境を拡張するインストール可能な COM オブジェクトである、VSPackage の概要を示し、独自の VSPackage の実装方法について説明します。

- [プロジェクト タイプ](../../extensibility/internals/project-types.md)

 プロジェクトを使用してコードの変更、コードのコンパイルとビルド、コードの実行とデバッグを行う方法について説明します。また、プロジェクト タイプの作成方法に関する詳細なトピックへのリンクも提供します。
