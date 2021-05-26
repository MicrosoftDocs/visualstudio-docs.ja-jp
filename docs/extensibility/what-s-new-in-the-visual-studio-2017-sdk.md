---
title: Visual Studio 2017 SDK の新機能 | Microsoft Docs
description: Visual Studio SDK には、更新された VSIX バージョン 3 形式を含む、Visual Studio 2017 の新機能と更新された機能があります。
ms.custom: SEO-VS-2020
ms.date: 10/31/2017
ms.topic: conceptual
ms.assetid: 9efcf0a3-dbde-4cab-8ed3-425826a48b2e
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 5a1e34ac23a0e6c298dae14c1613e7af0fc7b25d
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105061928"
---
# <a name="what39s-new-in-the-visual-studio-2017-sdk"></a>Visual Studio 2017 SDK の新機能

Visual Studio SDK には、Visual Studio 2017 の次の新機能と更新された機能があります。

## <a name="vsix-v3-format"></a>VSIX v3 形式

Visual Studio 2017 の新しい軽量インストールをサポートするため、VSIX 拡張機能マニフェストの形式がバージョン 3 (VSIX v3) に更新されました。

新しい形式では、次がサポートされます。

* VSIXInstaller によって検出およびインストールされる前提条件の明示的な宣言。
* 拡張機能のインストール時のアセンブリの Ngen。
* 通常の拡張機能ルートの外部への資産のインストール。

これらの変更の詳細については、次の各トピックを参照してください。

* [Visual Studio 2017 の機能拡張の変更点](breaking-changes-2017.md)
* [VSIX v3 での Ngen のサポート](ngen-support.md)
* [拡張機能フォルダー外でのインストール](set-install-root.md)
* [Visual Studio 2017 の機能拡張に関してよく寄せられる質問 (FAQ)](faq-2017.md)

## <a name="migrate-extensibility-project-to-visual-studio-2017"></a>機能拡張プロジェクトの Visual Studio 2017 への移行

拡張機能プロジェクトとその VSIX マニフェストを Visual Studio 2017 に更新する方法については、「[方法: 機能拡張プロジェクトを Visual Studio 2017 に移行する](how-to-migrate-extensibility-projects-to-visual-studio-2017.md)」を参照してください。

## <a name="custom-project-and-item-templates"></a>プロジェクトと項目のカスタム テンプレート

Visual Studio 2017 以降では、プロジェクトと項目のカスタム テンプレートのスキャンは実行されなくなりました。 代わりに、拡張機能で、これらのテンプレートのインストール場所を記述するテンプレート マニフェスト ファイルを提供する必要があります。 Visual Studio 2017 を使用して VSIX 拡張機能を更新できます。 MSI を使用して拡張機能を展開する場合は、テンプレート マニフェスト ファイルを手動で生成する必要があります。 詳細については、[Visual Studio 2017 用のプロジェクトと項目のカスタム テンプレートのアップグレード](../extensibility/upgrading-custom-project-and-item-templates-for-visual-studio-2017.md)に関する記事をご覧ください。 テンプレート マニフェスト スキーマについては、「[Visual Studio テンプレート マニフェスト スキーマ リファレンス](../extensibility/visual-studio-template-manifest-schema-reference.md)」で説明されています。

## <a name="updated-extension-performance-guidelines"></a>拡張機能のパフォーマンス ガイドラインの更新

「[VSPackage を管理する](managing-vspackages.md)」の新しい記事「[方法: 拡張機能のパフォーマンスを診断する](how-to-diagnose-extension-performance.md)」では、Visual Studio の起動とソリューション読み込みの時間に対する拡張機能の影響を検出して分析する方法について説明しています。
