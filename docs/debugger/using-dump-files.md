---
title: デバッガーでダンプ ファイルを使用する | Microsoft Docs
description: ダンプ ファイルは、実行中のアプリと読み込まれたモジュールのスナップショットです。 アプリへのデバッグ アクセスがない場合は、ダンプ ファイルを作成することを検討してください。
ms.custom: SEO-VS-2020
ms.date: 11/05/2018
ms.topic: conceptual
f1_keywords:
- vs.debug.crashdump
dev_langs:
- CSharp
- VB
- FSharp
- C++
- JScript
helpviewer_keywords:
- dumps, about dumps
- crash dumps
- dump files
- dumps
ms.assetid: b71be6dc-57e0-4730-99d2-b540a0863e49
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 1496c50d6a4022083a5cd093a0682ef36c70bbaa
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/19/2021
ms.locfileid: "112389229"
---
# <a name="dump-files-in-the-visual-studio-debugger"></a>Visual Studio デバッガーでのダンプ ファイル

<a name="BKMK_What_is_a_dump_file_"></a>"*ダンプ ファイル*" は、実行されていたプロセスと、ある時点でアプリに対して読み込まれたモジュールを示すスナップショットです。 ヒープ情報を含むダンプには、その時点でのアプリのメモリのスナップショットも含まれます。

Visual Studio でヒープ付きダンプ ファイルを開くのは、デバッグ セッションのブレークポイントで実行を中断するようなものです。 実行を続行することはできませんが、ダンプ時におけるアプリのスタック、スレッド、変数値を調べることができます。

ダンプは、ほとんどの場合、開発者がアクセス権を持たないコンピューターで生じた問題をデバッグするために使用されます。 クラッシュや応答しないプログラムを自分のマシン上で再現できないときは、顧客のマシンからのダンプ ファイルを使用できます。 また、テスト担当者は、詳細なテストに使用するクラッシュまたは応答しないプログラムのデータを保存するためにダンプを作成します。

Visual Studio デバッガーでは、マネージドまたはネイティブ コードのダンプ ファイルを保存できます。 Visual Studio によって作成されたダンプ ファイルも、"*ミニダンプ形式*" でファイルを保存する他のアプリによって作成されたダンプ ファイルもデバッグすることができます。

## <a name="requirements-and-limitations"></a><a name="BKMK_Requirements_and_limitations"></a> 要件と制限事項

- 64 ビットのコンピューターからのダンプ ファイルをデバッグするには、Visual Studio を 64 ビットのコンピューター上で実行する必要があります。

::: moniker range=">= vs-2019"
- Visual Studio では、Linux OS からのマネージド アプリのダンプ ファイルをデバッグできます。 
::: moniker-end

- Visual Studio では、ARM デバイスからのネイティブ アプリのダンプ ファイルをデバッグできます。 また、ARM デバイスからのマネージド アプリのダンプもデバッグできますが、これはネイティブ デバッガーでのみ可能です。

- [カーネルモード](/windows-hardware/drivers/debugger/kernel-mode-dump-files)のダンプ ファイルをデバッグする場合、または Visual Studio で [SOS.dll](/dotnet/framework/tools/sos-dll-sos-debugging-extension) デバッグ拡張機能を使用する場合は、[Windows Driver Kit (WDK)](/windows-hardware/drivers/download-the-wdk) の Windows 用のデバッグ ツールをダウンロードします。

- Visual Studio では、[フル ユーザーモード ダンプ](/windows/desktop/wer/collecting-user-mode-dumps)という以前の形式で保存されたダンプ ファイルをデバッグすることはできません。 フル ユーザーモード ダンプはヒープ付きダンプとは異なります。

- 最適化されたコードのダンプ ファイルをデバッグすると、混乱が生じることがあります。 たとえば、コンパイラによる関数のインライン展開により、予期しない呼び出し履歴になっていたり、その他の最適化により、変数の有効期間が変更されていたりします。

## <a name="dump-files-with-or-without-heaps"></a><a name="BKMK_Dump_files__with_or_without_heaps"></a> ヒープ情報あり/なしのダンプ ファイル

ダンプ ファイルには、ヒープ情報が含まれている場合もあれば、そうでない場合もあります。

- **ヒープ付きダンプ ファイル** には、ダンプ時におけるアプリのメモリのスナップショット (変数の値を含む) が格納されます。 また、Visual Studio では、読み込まれたネイティブ モジュールのバイナリがヒープ付きのダンプ ファイルに保存されるため、デバッグが大幅に簡単になります。 Visual Studio では、アプリ バイナリを見つけられない場合でも、ヒープ付きのダンプ ファイルからシンボルを読み込むことができます。

- **ヒープなしのダンプ ファイル** は、ヒープ付きのダンプよりもはるかに小さくなりますが、シンボル情報を検索する場合、デバッガーではアプリ バイナリを読み込む必要があります。 読み込まれたバイナリは、ダンプ作成中に実行されていたものと正確に一致する必要があります。 ヒープなしのダンプ ファイルには、スタック変数の値のみが保存されます。

## <a name="create-a-dump-file"></a><a name="BKMK_Create_a_dump_file"></a> ダンプ ファイルを作成する

Visual Studio でのプロセスのデバッグ中、デバッガーが例外またはブレークポイントで停止したときに、ダンプを保存できます。

[Just-In-Time デバッグ](../debugger/just-in-time-debugging-in-visual-studio.md)を有効にすると、Visual Studio の外部でクラッシュしたプロセスに Visual Studio デバッガーをアタッチして、デバッガーからのダンプ ファイルを保存できます。 [実行中のプロセスへのアタッチ](../debugger/attach-to-running-processes-with-the-visual-studio-debugger.md)に関するページを参照してください。

**ダンプ ファイルを保存するには:**

1. デバッグ中にエラーまたはブレークポイントで停止したときに、 **[デバッグ]** ** > [名前を付けてダンプを保存]** の順に選択します。

1. **[名前を付けてダンプを保存]** ダイアログ ボックスの **[保存の種類]** で、 **[ミニ ダンプ]** または **[ヒープ付きミニダンプ]** (既定値) を選択します。

1. パスを参照し、ダンプ ファイルの名前を選択してから、 **[保存]** を選択します。

>[!NOTE]
>Windows ミニダンプ形式をサポートする任意のプログラムでダンプ ファイルを作成できます。 たとえば、[Windows Sysinternals](/sysinternals/) の **Procdump** コマンド ライン ユーティリティでは、トリガーまたは必要に応じてプロセスのクラッシュ ダンプ ファイルを作成できます。 その他のツールを使用したダンプ ファイルの作成については、「[要件と制限](../debugger/using-dump-files.md#BKMK_Requirements_and_limitations)」を参照してください。

## <a name="open-a-dump-file"></a><a name="BKMK_Open_a_dump_file"></a> ダンプ ファイルを開く

1. Visual Studio で、 **[ファイル]**  >  **[開く]**  >  **[ファイル]** の順に選択します。

1. **[ファイルを開く]** ダイアログ ボックスで、ダンプ ファイルを探して選択します。 通常は拡張子 *.dmp* が付いています。 **[OK]** を選択します。

   **[ミニダンプ ファイルの概要]** ウィンドウには、ダンプ ファイルについての概要およびモジュール情報、実行できる操作が表示されます。

   ![ミニダンプ概要ページ](../debugger/media/dbg_dump_summarypage.png "ミニダンプ概要ページ")

1. **[アクション]** で次の操作を行います。
   - シンボルの読み込み場所を設定するには、 **[シンボル パスの設定]** を選択します。
   - デバッグを開始するには、 **[Debug with Managed Only]\(マネージドのみでデバッグ\)** 、 **[ネイティブのみでデバッグ]** 、 **[混合でデバッグ]** 、または **[Debug with Managed Memory]\(マネージド メモリでデバッグ\)** を選択します。

## <a name="find-exe-pdb-and-source-files"></a><a name="BKMK_Find_binaries__symbol___pdb__files__and_source_files"></a>.exe、.pdb、およびソース ファイルを検索する

完全なデバッグ機能をダンプ ファイルで使用する場合、Visual Studio では次のものが必要です。

- ダンプが作成された *.exe* ファイルと、ダンプ プロセスで使用されたその他のバイナリ (DLL など)。
- *.exe* およびその他のバイナリのシンボル ( *.pdb*) ファイル。
- ダンプ作成時のファイルのバージョンとビルドに正確に一致する *.exe* および *.pdb* ファイル。
- 関連モジュールのソース ファイル。 ソース ファイルを見つけることができない場合は、モジュールの逆アセンブルを使用できます。

ダンプにヒープ データが含まれる場合、Visual Studio では、一部のモジュールにバイナリ ファイルが欠落している状況にも対処できますが、有効な呼び出し履歴を生成できる十分なモジュールのバイナリが用意されている必要があります。

### <a name="search-paths-for-exe-files"></a>.exe ファイルの検索パス

Visual Studio では、ダンプ ファイルに含まれていない *.exe* ファイルが次の場所で自動的に検索されます。

1. ダンプ ファイルが含まれたフォルダー。
2. ダンプ ファイルで指定されているモジュール パス。これは、ダンプを収集したコンピューター上のモジュール パスです。
3. **[ツール]** (または **[デバッグ]** ) > **[オプション]**  >  **[デバッグ]**  >  **[シンボル]** で指定されたシンボル パス。 また、 **[ダンプ ファイルの概要]** ウィンドウの **[アクション]** ペインから **[シンボル]** ページを開くこともできます。 このページで、検索する複数の場所を追加できます。

### <a name="use-the-no-binary-no-symbols-or-no-source-found-pages"></a>[バイナリが見つかりません]、[シンボルが見つかりません]、[ソースが見つかりません] の各ページを使用する

Visual Studio でダンプ内のモジュールをデバッグするために必要なファイルが見つからない場合は、 **[バイナリが見つかりません]** 、 **[シンボルが見つかりません]** 、または **[ソースが見つかりません]** ページが表示されます。 これらのページでは、問題の原因に関する詳細な情報が表示され、ファイルの検索に役立つアクション リンクも表示されます。 [シンボル (.pdb) ファイルとソース ファイルの指定](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md)に関する記事をご覧ください。

## <a name="see-also"></a>関連項目

- [.NET 診断アナライザーを使用してマネージド メモリ ダンプをデバッグする方法](../debugger/how-to-debug-managed-memory-dump.md)
- [Just-In-Time デバッグ](../debugger/just-in-time-debugging-in-visual-studio.md)
- [シンボル (.pdb) とソース ファイルの指定](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md)
- [IntelliTrace](../debugger/intellitrace.md)