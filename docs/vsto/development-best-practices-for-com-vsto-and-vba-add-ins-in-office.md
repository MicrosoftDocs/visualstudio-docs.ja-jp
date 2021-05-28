---
title: '開発のベスト プラクティス: Office での COM、VSTO、VBA アドイン'
description: Microsoft Office 用の COM、VSTO、VBA アドインを開発するときに推奨されるベスト プラクティスについて説明します。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 07/25/2017
ms.topic: conceptual
dev_langs:
- ''
helpviewer_keywords:
- ''
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: d5470c138d4339356ca9f8c79cb5ab274dd99019
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99897556"
---
# <a name="development-best-practices-for-com-vsto-and-vba-add-ins-in-office"></a>Office での COM、VSTO、VBA アドインの開発に関するベスト プラクティス
  Office 用の COM、VSTO、または VBA アドインを開発している場合は、この記事で説明されている開発に関するベスト プラクティスに従ってください。   これにより、次のメリットが得られます。

- Office の異なるバージョンまたは配置の間でのアドインの互換性。
- ユーザーや IT 管理者にとってのアドイン配置の複雑さの軽減。
- アドインのインストールまたは実行の意図しない失敗が発生しない。

>注: Windows ストア用の COM、VSTO、または VBA アドインの[デスクトップ ブリッジ](/windows/uwp/porting/desktop-to-uwp-root)を使用した準備は、サポートされていません。 COM、VSTO、VBA アドインを Windows ストアまたは Office ストアに配布することはできません。

## <a name="do-not-check-for-office-during-installation"></a>インストールの間に Office をチェックしない
 アドインのインストール プロセスの間に、Office がインストールされているかどうかをアドインで検出することはお勧めしません。 Office がインストールされていない場合でもアドインをインストールでき、ユーザーは Office のインストール後にそれにアクセスできるようになります。

## <a name="use-embedded-interop-types-nopia"></a>埋め込まれた相互運用機能型 (NoPIA) を使用する
ソリューションで .NET 4.0 以降を使用する場合は、Office プライマリ相互運用機能アセンブリ (PIA) の再頒布可能パッケージに依存するのではなく、埋め込まれた相互運用機能型 (NoPIA) を使用します。 型の埋め込みを使用すると、ソリューションのインストール サイズが小さくなり、将来の互換性が保証されます。 Office 2010 は、PIA 再頒布可能パッケージが付属する Office の最後のバージョンでした。 詳細については、「[チュートリアル: Microsoft Office アセンブリからの型情報の埋め込み](/previous-versions/ee317478(v=vs.140))」および[型の等価性と埋め込まれた相互運用機能型](/windows/uwp/porting/desktop-to-uwp-root)に関する記事を参照してください。

ソリューションで以前のバージョンの .NET を使用する場合は、.NET 4.0 以降を使用するようにソリューションを更新することをお勧めします。 .NET 4.0 以降を使用すると、新しいバージョンの Windows での実行時の前提条件が減ります。

## <a name="avoid-depending-on-specific-office-versions"></a>Office の特定のバージョンに依存しない
新しいバージョンの Office でのみ使用できる機能をソリューションで使用する場合は、実行時に (たとえば、例外処理を使用するか、バージョンをチェックすることで) 機能が存在することを確認します (可能であれば、機能レベルで)。 オブジェクト モデルでサポートされている API を使用して、特定のバージョンではなく最小バージョンを検証します ([Application.Version プロパティ](<xref:Microsoft.Office.Interop.Excel._Application.Version%2A>)など)。 Office バイナリ メタデータ、インストール パス、またはレジストリ キーは、インストール、環境、およびバージョン間で変わる可能性があるため、使用しないことをお勧めします。

## <a name="enable-both-32-bit-and-64-bit-office-usage"></a>32 ビットと 64 ビット両方の Office の使用を有効にする
ソリューションが特定のビットでのみ使用できるライブラリに依存している場合を除き、既定のビルド ターゲットでは 32 ビット (x86) と 64 ビット (x64) の両方をサポートする必要があります。 64 ビット バージョンの Office は、特にビッグ データ環境で、導入が増えています。 32 ビットと 64 ビットの両方をサポートすることにより、ユーザーは、Office の 32 ビット バージョンと 64 ビット バージョンの間を簡単に移行できます。

VBA コードを記述するときは、64 ビット セーフの宣言ステートメントを使用し、必要に応じて変数を変換します。 また、各ビットのコードを提供することで、32 ビットまたは 64 ビットのバージョンの Office を実行しているユーザー間でドキュメントを共有できるようにします。 詳細については、「[64 ビット Visual Basic for Applications の概要](/office/vba/Language/Concepts/Getting-Started/64-bit-visual-basic-for-applications-overview)」を参照してください。

## <a name="support-restricted-environments"></a>制限された環境をサポートする
ソリューションで、ユーザー アカウントの昇格または管理者特権を要求してはなりません。 また、ソリューションは、次のものの設定または変更に依存しないようにする必要があります。

- 現在の作業ディレクトリ
- DLL の読み込みディレクトリ。
- PATH 変数。

## <a name="change-the-save-location-of-shared-data-and-settings"></a>共有データと設定の保存場所を変更する
ソリューションがアドインと Office の外部にあるプロセスで構成されている場合は、アドインと外部プロセスの間でのデータや設定の交換に、ユーザーのアプリケーション データ フォルダーまたはレジストリを使用しないでください。 代わりに、ユーザーの一時フォルダー、ドキュメント フォルダー、またはソリューションのインストール ディレクトリを使用することを検討します。

## <a name="increment-the-version-number-with-each-update"></a>更新のたびにバージョン番号をインクリメントする
ソリューションでバイナリのバージョン番号を設定し、更新ごとにインクリメントします。 これにより、ユーザーはバージョン間の変更を識別し、互換性を評価することが容易になります。

## <a name="provide-support-statements-for-the-latest-versions-of-office"></a>Office の最新バージョンのサポートに関する声明を提供する
お客様は、Office で実行される COM、VSTO、VBA アドインについてのサポートに関する声明の提供を ISV に依頼しています。 サポートに関する声明を明示的に記載しておくと、お客様は、エンタープライズ対応ツール用の Microsoft 365 アプリを使用して、サポートを理解することができます。

Office クライアント アプリケーション (Word、Excel など) のサポートに関する声明を提供するには、まず、アドインが現在の Office リリースで実行されていることを確認した後、将来のリリースでアドインが破損した場合に、更新プログラムを提供することを表明します。 Microsoft によって Office の新しいビルドまたは更新プログラムがリリースされたときに、アドインをテストする必要はありません。 Microsoft で Office の COM、VSTO、VBA の拡張性プラットフォームが変更されることはほとんどなく、これらの変更についてはドキュメントで適切に説明されます。

>重要: Microsoft は、準備レポートに対してサポートされているアドインと、ISV 連絡先情報の一覧を保持しています。 一覧に含まれるアドインを取得するには、[/configmgr/desktop-analytics/ready-for-windows](/configmgr/desktop-analytics/ready-for-windows) を参照してください。

## <a name="use-process-monitor-to-help-debug-installation-or-loading-issues"></a>プロセス モニターを使用してインストールまたは読み込みに関する問題をデバッグする
インストールまたは読み込みの間にアドインで互換性に関する問題が発生する場合は、ファイルまたはレジストリへのアクセスの問題が関係している可能性があります。 [プロセス モニター](/sysinternals/downloads/procmon)または同様のデバッグ ツールを使用してログを記録し、動作している環境と比較して、問題を特定することができます。