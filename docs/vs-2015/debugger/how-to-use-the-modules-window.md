---
title: '方法: Use the Modules Window |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.debug.modules
dev_langs:
- FSharp
- VB
- CSharp
- C++
- JScript
- VB
- CSharp
- C++
helpviewer_keywords:
- debugger, Modules window
- Modules window
- executable files, displaying while debugging
- debugging [Visual Studio], displaying modules
- DLLs, displaying while debugging
- modules, displaying
ms.assetid: d840fdca-b035-4452-b652-72580c831896
caps.latest.revision: 41
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 2f332ef1a52ae49e51025614745fc1b5c4a44e07
ms.sourcegitcommit: 1fc6ee928733e61a1f42782f832ead9f7946d00c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2019
ms.locfileid: "60078292"
---
# <a name="how-to-use-the-modules-window"></a>方法: [モジュール] ウィンドウを使用します。
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

注意]
>  この機能は、SQL またはスクリプトのデバッグでは使用できません。  
  
 **モジュール**ウィンドウには、プログラムによって使用され、それぞれの関連情報が表示される Dll と EXE が一覧表示されます。  
  
### <a name="to-display-the-modules-window-in-break-mode-or-in-run-mode"></a>[モジュール] ウィンドウを表示するには (中断モードまたは実行モードの場合)  
  
- **デバッグ** メニューの 選択**Windows**、 をクリックし、**モジュール**します。  
  
     既定では、**[モジュール]** ウィンドウには、モジュールが読み込み順に表示されます。 ただし、基準列を指定して並べ替えるように選択できます。  
  
### <a name="to-sort-by-any-column"></a>基準列を指定して並べ替えるには  
  
- 列の上部にあるボタンをクリックします。  
  
     シンボルの読み込みまたはシンボル パスを指定することができます、**モジュール**ウィンドウ ショートカット メニューを使用します。  
  
## <a name="loading-symbols"></a>シンボルの読み込み  
 **モジュール**ウィンドウで、モジュールでは、デバッグ シンボルが読み込まれるを参照してください。 この情報が表示されます、**シンボルの状態**列。 済み状態の場合**Skipped loadingCannot が見つからないか、PDB ファイルを開く**、または**包含/除外の設定で無効にする読み込み**、Microsoft パブリック シンボルからシンボルをダウンロードするデバッガーに指示することができますサーバーまたはコンピューターにシンボルのディレクトリからシンボルを読み込みます。 詳細については、次を参照してください[指定シンボル (.pdb) とソース ファイル。](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md)  
  
#### <a name="to-load-symbols-manually"></a>シンボルを手動で読み込むには  
  
1. **モジュール**ウィンドウで、モジュールのシンボルが読み込まれていないを右クリックします。  
  
2. をポイント**シンボルの読み込み元**し**Microsoft シンボル サーバー**または**シンボル パス**します。  
  
#### <a name="to-change-symbol-load-settings"></a>シンボル読み込みの設定を変更するには  
  
1. **[モジュール]** ウィンドウで、任意のモジュールを右クリックします。  
  
2. クリックして**シンボルの設定**します。  
  
     シンボルの読み込み設定を変更することができますようになりました[シンボルの場所を指定し、読み込み動作](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md#BKMK_Specify_symbol_locations_and_loading_behavior)します。 変更内容は、デバッグ セッションを再起動しないと有効になりません。  
  
#### <a name="to-change-symbol-load-behavior-for-a-specific-module"></a>特定のモジュールのシンボル読み込み動作を変更するには  
  
1. **[モジュール]** ウィンドウで、モジュールを右クリックします。  
  
2. をポイント**自動シンボル読み込みの設定** をクリックし、**常に手動で読み込む**または**既定**します。 変更内容は、デバッグ セッションを再起動しないと有効になりません。  
  
## <a name="see-also"></a>関連項目  
 [実行の中断](http://msdn.microsoft.com/30fc4643-f337-4651-b1ff-f2de2c098d40)   
 [デバッガーでのデータ表示](../debugger/viewing-data-in-the-debugger.md)   
 [シンボルとソース コードの管理](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md)
