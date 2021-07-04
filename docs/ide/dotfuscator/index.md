---
title: Dotfuscator Community
ms.date: 03/28/2019
ms.devlang: dotnet
ms.topic: overview
keywords: Dotfuscator, Dotfuscator CE, Dotfuscator Community, PreEmptive, PreEmptive Solutions, PreEmptive Protection, protection, community edition, 難読化, .NET, 無料, Visual Studio 2019, Visual Studio 2017, Visual Studio
helpviewer_keywords:
- PreEmptive Protection Dotfuscator
- Dotfuscator Community Edition
- Dotfuscator CE
- Dotfuscator Community
- Dotfuscator
- obfuscation
- protection
description: Visual Studio に含まれる Dotfuscator Community の無料コピーを使用して .NET アプリケーションを保護する方法について説明します。
ms.assetid: d9550502-0a82-49a6-b005-2caa791fbe02
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.openlocfilehash: 75437af41cec6fd770af9dfcdb399ed51543b7ff
ms.sourcegitcommit: 5fb4a67a8208707e79dc09601e8db70b16ba7192
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/17/2021
ms.locfileid: "112308221"
---
# <a name="dotfuscator-community"></a>Dotfuscator Community

***PreEmptive Protection - Dotfuscator*** は、安全なソフトウェア開発ライフサイクルに容易に適合する、包括的な .NET アプリケーションの保護機能を提供します。
この機能により、デスクトップ、モバイル、サーバー、組み込みのアプリケーションを強化および保護し、余分なものを取り除くことで、企業秘密やその他の知的財産 (IP) を守り、違法コピーや偽造を減らし、改ざんと権限のないデバッグを防止できます。
Dotfuscator はコンパイル済みのアセンブリで動作し、追加のプログラミングやソース コードへのアクセスは不要です。

![PreEmptive Protection - Dotfuscator](media/header.svg)

## <a name="why-protection-matters"></a>保護が必要な理由

**知的財産 (IP) を保護** することは重要です。
アプリケーションのコードに含まれる設計と実装の詳細は、IP であるとみなすことができます。
ただし、.NET Framework で構築されたアプリケーションには[重要なメタデータと高度な中間コードが含まれており][assemblies]、多数存在する無料の自動化ツールのいずれかを使用するだけで、簡単にリバース エンジニアリングを実行できます。
リバース エンジニアリングを中断および停止させることで、許可されていない IP の漏えいを防止できるだけでなく、コードに企業秘密が含まれていることを示すことができます。
Dotfuscator は、元のアプリケーションの動作を維持しながら、.NET アセンブリを[難読化][obfuscation]し、リバース エンジニアリングを防止します。

**アプリケーションの整合性を保護** することも重要です。
リバース エンジニアリングだけでなく、犯罪者がアプリケーションの違法コピーを作成したり、実行時のアプリケーションの動作を変更したり、データを操作したりしようとすることもあります。
Dotfuscator は、改ざん、サード パーティによるデバッグ、ルート化されたデバイスを含め、[許可のない使用を検出し、それに対応する][checks]機能をアプリケーションに注入します。

保護されたソフトウェア開発ライフサイクルに Dotfuscator が適合するしくみの詳細については、PreEmptive Solution の「[SDL App Protection][sdl-protection]」(SDL アプリの保護) のページを参照してください。

## <a name="about-dotfuscator-community"></a>Dotfuscator Community について

Microsoft Visual Studio のコピーには、***PreEmptive Protection - Dotfuscator Community*** の無料ライセンスが含まれています。
(この無料バージョンは、以前は Dotfuscator Community Edition または Dotfuscator CE と呼ばれていました。)Visual Studio に含まれている Dotfuscator Community のバージョンをインストールする方法の手順については、[インストールに関するページ][install]を参照してください。

Dotfuscator Community は、広範な[ソフトウェアの保護と強化][software-protection]のサービスを開発者、アーキテクト、およびテスト担当者に提供します。
[.NET の難読化][obfuscation]および Dotfuscator Community に含まれるその他の[アプリケーションの保護][app-protection]機能の例を以下に挙げます。

* 識別子の *[名前の変更][renaming]* により、コンパイル済みアセンブリのリバース エンジニアリングをさらに難しくします。
* *[改ざん防止][tamper]* 機能により、改ざんされたアプリケーションの実行が検出され、改ざんされたセッションが終了または対処されます。
* *[デバッグ防止][debug]* 機能により、実行中のアプリケーションに対するデバッガーの添付ファイルが検出され、デバッグ セッションが終了または対処されます。
* *[ルート化されたデバイスの防止][root]* 機能により、そのようなルート化された Android デバイスで実行されているアプリケーションが検出され、そのデバイスでのセッションが終了または対処されます。
* *[アプリケーションの有効期限の動作][shelflife]* は、"有効期限" の日付をエンコードし、期限切れのアプリケーション セッションを終了します。

お客様のアプリケーション保護戦略にどのように適合するかを含めた、これらの機能の詳細については、[機能に関するページ][capabilities]を参照してください。

Dotfuscator Community には、すぐに利用できる基本的な保護機能が用意されています。
Dotfuscator Community の登録済みのユーザー、***PreEmptive Protection - Dotfuscator Professional*** のユーザー、および世界トップレベルの [.NET Obfuscator][net-obfuscator] のユーザーは、さらに多くのアプリケーションの保護対策を利用できます。
Dotfuscator の拡張方法については、[アップグレードに関するページ][upgrades]を参照してください。

## <a name="getting-started"></a>作業の開始

::: moniker range=">=vs-2019"

Visual Studio から Dotfuscator Community の使用を開始するには、**検索ボックス** (Ctrl + Q) に `dotfuscator` と入力します。

* Dotfuscator Community が既にインストールされている場合、**検索ボックス** の *[メニュー]* 見出しの下に Dotfuscator Community を開始するオプションが表示されます。 詳細については、[Dotfuscator Community の完全なユーザー ガイドの概要ページ][get-started]を参照してください。
* Dotfuscator Community がまだインストールされていない場合、**検索ボックス** の *[個別のコンポーネント]* 見出しに、代わりに **[Install PreEmptive Protection - Dotfuscator]\(PreEmptive Protection - Dotfuscator のインストール\)** が表示されます。 詳細については、[インストールに関するページ][install]を参照してください。

::: moniker-end

::: moniker range="vs-2017"

Visual Studio から Dotfuscator Community の使用を開始するには、**クイック起動** (Ctrl + Q) 検索バーに `dotfuscator` と入力します。

* Dotfuscator Community が既にインストールされている場合は、**クイック起動** によって、Dotfuscator Community ユーザー インターフェイスを起動する *[メニュー]* オプションが表示されます。 詳細については、[Dotfuscator Community の完全なユーザー ガイドの概要ページ][get-started]を参照してください。
* Dotfuscator Community がまだインストールされていない場合は、**クイック起動** によって、関連する *[インストール]* オプションが表示されます。 詳細については、[インストールに関するページ][install]を参照してください。

::: moniker-end

**最新バージョン** の Dotfuscator Community も、[preemptive.com の Dotfuscator Downloads ページ][download]からダウンロードできます。

## <a name="full-documentation"></a>すべてのドキュメント

このページとそのサブページでは、Dotfuscator Community 機能の概略に加え、[ツールをインストールする方法][install]について説明しています。

[Dotfuscator Community ユーザー インターフェイスの使用を開始する方法][get-started]を含めた、詳細な使用方法の説明については、[Dotfuscator Community の完全なユーザー ガイド (preemptive.com)][full] を参照してください。

<!-- Copyright © 2019 PreEmptive Solutions, LLC -->

[assemblies]:  /dotnet/standard/assembly-format
[software-protection]:  https://www.preemptive.com/software-protection
[obfuscation]:  https://www.preemptive.com/obfuscation
[app-protection]:  https://www.preemptive.com/application-protection
[sdl-protection]:  https://www.preemptive.com/solutions/SDL-App-Protection
[net-obfuscator]:  https://www.preemptive.com/products/dotfuscator/overview
[download]:  https://www.preemptive.com/products/dotfuscator/downloads

[install]:  install.md
[capabilities]:  capabilities.md
[upgrades]:  upgrades.md

[get-started]:  https://www.preemptive.com/dotfuscator/ce/docs/help/gui_getstarted.html

[renaming]:  https://www.preemptive.com/dotfuscator/ce/docs/help/obfuscation_renaming.html

[checks]:  https://www.preemptive.com/dotfuscator/ce/docs/help/checks_overview.html
[tamper]:  https://www.preemptive.com/dotfuscator/ce/docs/help/checks_tamper.html
[debug]:  https://www.preemptive.com/dotfuscator/ce/docs/help/checks_debug.html
[root]: https://www.preemptive.com/dotfuscator/ce/docs/help/checks_root.html
[shelflife]:  https://www.preemptive.com/dotfuscator/ce/docs/help/checks_shelflife.html

[full]:  https://www.preemptive.com/dotfuscator/ce/docs/help/index.html
