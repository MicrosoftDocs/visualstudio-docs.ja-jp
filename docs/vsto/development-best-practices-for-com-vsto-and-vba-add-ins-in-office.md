---
title: 開発のベストプラクティス:Office の COM、VSTO、& VBA アドイン
ms.date: 07/25/2017
ms.topic: conceptual
dev_langs:
- ''
helpviewer_keywords:
- ''
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 35b39aef2865f0438e6165bd6bf2c5418e8fbcb0
ms.sourcegitcommit: e98db44f3a33529b0ba188d24390efd09e548191
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/25/2019
ms.locfileid: "71254642"
---
# <a name="development-best-practices-for-com-vsto-and-vba-add-ins-in-office"></a>Office での COM、VSTO、および VBA アドインの開発に関するベストプラクティス
  Office 用の COM、VSTO、または VBA アドインを開発している場合は、この記事で説明されている開発のベストプラクティスに従ってください。   これは次のことを保証するのに役立ちます。

- さまざまなバージョンや Office の展開でのアドインの互換性。
- ユーザーと IT 管理者のためのアドイン配置の複雑さが軽減されます。
- アドインの意図しないインストールまたは実行時のエラーは発生しません。

>メモ:[デスクトップブリッジ](/windows/uwp/porting/desktop-to-uwp-root)を使用して、Windows ストア用の COM、VSTO、または VBA アドインを準備することはできません。 COM、VSTO、および VBA アドインを Windows ストアまたは Office ストアに配布することはできません。

## <a name="do-not-check-for-office-during-installation"></a>インストール中に Office を確認しない
 アドインのインストールプロセス中に Office がインストールされているかどうかをアドインで検出することはお勧めしません。 Office がインストールされていない場合は、アドインをインストールできます。これにより、Office のインストール後にユーザーがアクセスできるようになります。

## <a name="use-embedded-interop-types-nopia"></a>埋め込み相互運用機能型を使用する (NoPIA)
ソリューションで .NET 4.0 以降を使用している場合は、Office プライマリ相互運用機能アセンブリ (PIA) の再頒布可能パッケージに依存するのではなく、埋め込まれた相互運用機能型 (NoPIA) を使用します。 型の埋め込みを使用すると、ソリューションのインストールサイズが削減され、将来の互換性が確保されます。 Office 2010 は、PIA 再頒布可能パッケージに同梱されていた Office の最後のバージョンです。 詳細については、「[チュートリアル:Microsoft Office アセンブリ](https://msdn.microsoft.com/library/ee317478.aspx) 、[型の等価性、および埋め込まれた相互運用機能型](/windows/uwp/porting/desktop-to-uwp-root)からの型情報の埋め込み。

ソリューションで以前のバージョンの .NET を使用している場合は、.NET 4.0 以降を使用するようにソリューションを更新することをお勧めします。 .NET 4.0 以降を使用すると、新しいバージョンの Windows で実行時の前提条件を減らすことができます。

## <a name="avoid-depending-on-specific-office-versions"></a>特定の Office バージョンに依存しない
新しいバージョンの Office でのみ使用できる機能をソリューションで使用する場合は、実行時に機能が (可能であれば機能レベルで) 存在することを確認します (たとえば、例外処理を使用するか、バージョンを確認します)。 オブジェクトモデルでサポートされている Api ( [Application. Version プロパティ](<xref:Microsoft.Office.Interop.Excel._Application.Version%2A>)など) を使用して、特定のバージョンではなく、最小バージョンを検証します。 Office バイナリメタデータ、インストールパス、またはレジストリキーは、インストール、環境、およびバージョン間で変わる可能性があるため、使用しないことをお勧めします。

## <a name="enable-both-32-bit-and-64-bit-office-usage"></a>32ビットと64ビットの両方の Office の使用を有効にする
ソリューションが特定のビットにしか使用できないライブラリに依存している場合を除き、既定のビルドターゲットは32ビット (x86) と64ビット (x64) の両方をサポートする必要があります。 Office の64ビットバージョンは、特にビッグデータ環境で導入されています。 32ビットと64ビットの両方をサポートすることにより、ユーザーは、Office の32ビットバージョンと64ビットバージョンを簡単に移行できます。

VBA コードを記述する場合は、64ビットセーフな declare ステートメントを使用し、必要に応じて変数を変換します。 また、各ビットのコードを提供することで、32ビットまたは64ビットの両方のバージョンの Office を実行しているユーザー間でドキュメントを共有できることを確認します。 詳細については、「 [64 ビット Visual Basic アプリケーションの概要](/office/vba/Language/Concepts/Getting-Started/64-bit-visual-basic-for-applications-overview)」を参照してください。

## <a name="support-restricted-environments"></a>制限された環境のサポート
ソリューションには、ユーザーアカウントの昇格または管理者特権は必要ありません。 また、ソリューションは設定または変更に依存しないようにする必要があります。

- 現在の作業ディレクトリ。
- DLL の読み込みディレクトリ。
- PATH 変数です。

## <a name="change-the-save-location-of-shared-data-and-settings"></a>共有データと設定の保存場所を変更する
アドインと、Office の外部にあるプロセスでソリューションが構成されている場合は、ユーザーのアプリケーションデータフォルダーまたはレジストリを使用して、アドインと外部プロセスとの間でデータや設定を交換しないでください。 代わりに、ユーザーの一時フォルダー、ドキュメントフォルダー、またはソリューションのインストールディレクトリを使用することを検討してください。

## <a name="increment-the-version-number-with-each-update"></a>各更新プログラムを使用してバージョン番号を増分する
ソリューション内のバイナリのバージョン番号を設定し、更新ごとにインクリメントします。 これにより、ユーザーはバージョン間の変更を識別し、互換性を評価することが容易になります。

## <a name="provide-support-statements-for-the-latest-versions-of-office"></a>Office の最新バージョンのサポートに関する声明を提供する
お客様は、Office で実行される COM、VSTO、および VBA アドインに対してサポートステートメントを提供するよう Isv に依頼しています。 明示的なサポートステートメントを一覧表示しておくと、Office 365 ProPlus readiness ツールを使用したお客様のサポートの理解に役立ちます。

Office クライアントアプリケーション (Word、Excel など) のサポートステートメントを提供するには、まず、アドインが現在の Office リリースで実行されていることを確認し、今後のリリースでアドインが破損した場合に、更新プログラムの提供を確定します。 Microsoft が新しいビルドをリリースしたとき、または Office に更新プログラムをリリースしたときに、アドインをテストする必要はありません。 Microsoft では、Office の COM、VSTO、および VBA の拡張プラットフォームを変更することはほとんどありません。これらの変更については、ドキュメントをご覧ください。

>重要 : Microsoft では、準備レポートと ISV 連絡先情報のサポートされているアドインの一覧を保持しています。 アドインを表示するには、「」 [https://aka.ms/readyforwindows](https://aka.ms/readyforwindows)を参照してください。

## <a name="use-process-monitor-to-help-debug-installation-or-loading-issues"></a>プロセスモニターを使用してインストールまたは読み込みに関する問題をデバッグする
インストールまたは読み込み中にアドインに互換性の問題がある場合は、ファイルまたはレジストリへのアクセスに関する問題に関連している可能性があります。 [プロセスモニター](/sysinternals/downloads/procmon)または同様のデバッグツールを使用して、動作中の環境に対する動作をログに記録して比較し、問題を特定することができます。
