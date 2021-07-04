---
title: デバッガーで逆アセンブリ コードを表示する | Microsoft Docs
description: Visual Studio の [逆アセンブリ] ウィンドウを使用して、コンパイラによって作成された命令に対応するアセンブリ コードを表示します。
ms.custom: SEO-VS-2020
ms.date: 10/30/2018
ms.topic: how-to
f1_keywords:
- vs.debug.disassembly
dev_langs:
- CSharp
- VB
- FSharp
- C++
- JScript
helpviewer_keywords:
- assembly language, debugging inline assembly code
- breakpoints, Disassembly window
- Disassembly window
- machine code
ms.assetid: eaf84dd0-c82d-481b-af51-690b74e7794c
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: c8cc67b2f8136ea426eb56c25fb3c345198701f1
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/19/2021
ms.locfileid: "112387464"
---
# <a name="view-disassembly-code-in-the-visual-studio-debugger-c-c-visual-basic-f"></a>Visual Studio デバッガーで逆アセンブリ コードを表示する (C#、C++、Visual Basic、F#)

**[逆アセンブル]** ウィンドウには、コンパイラによって作成された命令に対応するアセンブリ コードが表示されます。 マネージド コードをデバッグする場合、これらのアセンブリ命令は、Visual Studio コンパイラによって作成された Microsoft Intermediate Language (MSIL) ではなく、Just-In-Time (JIT) コンパイラが作成したネイティブ コードに対応します。

> [!NOTE]
> **逆アセンブリ** ウィンドウを最大限に活用するには、[アセンブリ言語プログラミング](https://wikipedia.org/wiki/Assembly_language)の基本について理解しているか、または学習する必要があります。

この機能は、アドレスレベルのデバッグが有効になっている場合のみ使用できます。 スクリプトまたは SQL のデバッグには使用できません。

**[逆アセンブル]** ウィンドウでは、アセンブリ命令だけでなく、必要に応じて以下の情報も表示できます。

- 各命令が配置されているメモリ アドレス。 ネイティブ アプリケーションの場合は、実際のメモリ アドレスです。 Visual Basic または C# の場合、これは、関数の先頭からのオフセットです。

- アセンブリ コードの派生元のソース コード。

- コード バイト、つまり、実際のマシン語命令または MSIL 命令のバイト表現。

- メモリ アドレスのシンボル名。

- ソース コードに対応する行番号。

アセンブリ言語命令は、命令名の省略形である "*ニーモニック*" と、変数、レジスタ、定数を表す "*記号*" で構成されます。 各マシン語命令は 1 つのアセンブリ言語ニーモニックで表現され、任意でその後に 1 つ以上の記号が続きます。

アセンブリ コードは、プロセッサ レジスタ、またはマネージド コードの場合は、共通言語ランタイム レジスタに大きく依存します。 **逆アセンブリ** ウィンドウと **レジスタ** ウィンドウを組み合わせて使用することができ、これによりレジスタの内容を調べることができます。

マシンコード命令をアセンブリ言語ではなく未加工の数値形式で表示するには、**メモリ** ウィンドウを使用するか、**逆アセンブリ** ウィンドウのショートカット メニューから **[コード バイト]** を選択します。

## <a name="use-the-disassembly-window"></a>[逆アセンブル] ウィンドウを使用する

**逆アセンブリ** ウィンドウを有効にするには、 **[ツール]** 、 **[オプション]** 、 **[デバッグ]** の順に選択し、 **[アドレスレベルのデバッグを有効にする]** を選択します。

デバッグ中に **逆アセンブリ** ウィンドウを開くには、 **[ウィンドウ]**  >  **[逆アセンブリ]** を選択するか、または **Alt**+**8** キーを押します。

> [!NOTE]
> 実際に画面に表示されるダイアログ ボックスとメニュー コマンドは、アクティブな設定またはエディションによっては、ヘルプの説明と異なる場合があります。 設定を変更するには、 **[ツール]** メニューの **[設定のインポートとエクスポート]** をクリックします。 詳細については、「[リセット設定](../ide/environment-settings.md#reset-settings)」を参照してください。

オプションの情報の表示と非表示を切り替えるには、**逆アセンブリ** ウィンドウで右クリックし、ショートカット メニューで必要なオプションを設定またはクリアします。

左余白の黄色の矢印は、現在の実行ポイントを示します。 ネイティブ コードの場合、実行ポイントは CPU のプログラム カウンターに対応します。 この位置は、プログラム内で次に実行される命令を示します。

## <a name="see-also"></a>関連項目

* [ページ単位の上下移動 (メモリ内での)](../debugger/how-to-page-up-or-down-in-memory.md)
* [デバッガーでのデータ表示](../debugger/viewing-data-in-the-debugger.md)
* [方法: [レジスタ] ウィンドウを使用する](../debugger/how-to-use-the-registers-window.md)