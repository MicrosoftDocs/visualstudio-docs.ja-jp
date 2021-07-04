---
title: DLL と実行可能ファイルの表示
description: Visual Studio のデバッグ セッション中に、[モジュール] ウィンドウでアプリによって使用される DLL と実行可能ファイル (.exe ファイル) を表示します。
ms.custom: SEO-VS-2020
titleSuffix: Visual Studio Modules window
ms.date: 11/04/2018
ms.topic: how-to
f1_keywords:
- vs.debug.modules
dev_langs:
- CSharp
- VB
- FSharp
- C++
- JScript
helpviewer_keywords:
- debugger, Modules window
- Modules window
- executable files, displaying while debugging
- debugging [Visual Studio], displaying modules
- DLLs, displaying while debugging
- modules, displaying
ms.assetid: d840fdca-b035-4452-b652-72580c831896
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: f82b8a5051cf1c338c4b1aab6e78209fb2bc08b0
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/19/2021
ms.locfileid: "112385410"
---
# <a name="view-dlls-and-executables-in-the-modules-window-c-c-visual-basic-f"></a>[モジュール] ウィンドウでの DLL と実行可能ファイルの表示 (C#、C++、Visual Basic、F#)

Visual Studio のデバッグ中、アプリで使用される DLL と実行可能ファイル ( *.exe* ファイル) に関する情報が **[モジュール]** ウィンドウに表示されます。

> [!NOTE]
> [モジュール] ウィンドウは、SQL またはスクリプトのデバッグには使用できません。

## <a name="use-the-modules-window"></a>[モジュール] ウィンドウを使用する

[モジュール] ウィンドウを開くには、デバッグ中に **[デバッグ]**  >  **[ウィンドウ]**  >  **[モジュール]** の順に選択します (または、**Ctrl + Alt + U** キーを押します)。

既定では、 **[モジュール]** ウィンドウには、モジュールが読み込み順に表示されます。 任意のウィンドウ列で並べ替えるには、列の上部にあるヘッダーを選択します。

## <a name="load-symbols"></a>シンボルの読み込み

**[モジュール]** ウィンドウの **[シンボルの状態]** 列では、デバッグ シンボルが読み込まれたモジュールを確認できます。 状態が **[シンボルの読み込みをスキップしました]** 、 **[PDB ファイルを開けないか、ファイルが見つかりません]** 、または **[含める/除外する設定により、読み込みは無効になっています]** の場合は、シンボルを手動で読み込むことができます。 シンボルの読み込みについては、[シンボル (.pdb) ファイルとソース ファイルの指定](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md)に関するページを参照してください。

**シンボルを手動で読み込むには:**

1. **[モジュール]** ウィンドウで、シンボルが読み込まれていないモジュールを右クリックします。

   - シンボルが読み込まれなかった理由の詳細については、 **[シンボルの読み込み情報]** を選択してください。

   - シンボルを手動で読み込むには、 **[シンボルの読み込み]** を選択します。

1. シンボルが読み込まれない場合は、 **[シンボルの設定]** を選択して、 **[オプション]** ダイアログを開き、シンボルの読み込み場所を指定または変更します。

   パブリックの Microsoft シンボル サーバーまたはその他のサーバーからシンボルをダウンロードするか、コンピューター上のフォルダーからシンボルを読み込むことができます。 詳細については、[シンボルの場所と読み込み動作の指定](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md#BKMK_Specify_symbol_locations_and_loading_behavior)に関するページを参照してください。

**シンボル読み込み動作の設定を変更するには:**

1. **[モジュール]** ウィンドウで、任意のモジュールを右クリックします。

1. **[シンボルの設定]** を選択します。

1. **[すべてのシンボルを読み込む]** を選択するか、含めるモジュール、または除外するモジュールを選択します。

1. **[OK]** を選択します。 変更は、次のデバッグ セッションで有効になります。

**特定のモジュールのシンボル読み込み動作を変更するには:**

1. **[モジュール]** ウィンドウで、モジュールを右クリックします。

1. 右クリック メニューで、 **[常に自動的に読み込む]** を選択または選択解除します。 変更は、次のデバッグ セッションで有効になります。

## <a name="see-also"></a>関連項目
- [実行の中断](/previous-versions/visualstudio/visual-studio-2010/7z9se2d8(v=vs.100))
- [デバッガーでのデータ表示](../debugger/viewing-data-in-the-debugger.md)
- [シンボル (.pdb) とソース ファイルの指定](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md)