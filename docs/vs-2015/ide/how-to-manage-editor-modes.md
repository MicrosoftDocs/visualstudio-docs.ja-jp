﻿---
title: '方法: エディターのモードの管理 |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
helpviewer_keywords:
- word wrap
- views, virtual space
- line numbers, displaying
- virtual space mode
- line numbers
- Code Editor, view and display options
- full screen mode
- Code Editor, modes
- views, splitting
- views, word wrapping
- fonts and size
- views, creating new windows
- views, line numbers
- views, changing mode
- views, outlining
ms.assetid: 1fb48027-d870-439f-8b72-4a0321390748
caps.latest.revision: 24
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 7db5f2869c1118a04f1aa734e5067ece4b268833
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63430532"
---
# <a name="how-to-manage-editor-modes"></a>方法: エディターのモードを管理します。
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio のコード エディターは、さまざまな表示モードで表示できます。  
  
> [!NOTE]
> 実際に画面に表示されるダイアログ ボックスとメニュー コマンドは、アクティブな設定またはエディションによっては、ヘルプの説明と異なる場合があります。 設定を変更するには、 **[ツール]** メニューの **[設定のインポートとエクスポート]** をクリックします。 詳細については、「 [Visual Studio での開発設定のカスタマイズ](http://msdn.microsoft.com/22c4debb-4e31-47a8-8f19-16f328d7dcd3)」を参照してください。  
  
## <a name="enabling-full-screen-mode"></a>全画面表示モードを有効にする  
 **全画面表示**モードを有効にすると、すべてのツール ウィンドウを非表示にして、ドキュメント ウィンドウだけを表示することができます。  
  
#### <a name="to-enable-full-screen-mode"></a>全画面表示モードを有効にするには  
  
- **全画面表示**モードを開始または終了するには、Alt + Shift + Enter キーを押します。  
  
     または  
  
- **[コマンド]** ウィンドウで `View.Fullscreen` コマンドを実行します。  
  
## <a name="enabling-virtual-space-mode"></a>仮想空白モードを有効にする  
 **仮想空白**モードでは、各コード行の末尾に空白が挿入されます。 コードの横に一貫してコメントを入れる場合は、このチェック ボックスをオンにします。  
  
#### <a name="to-enable-virtual-space-mode"></a>仮想空白モードを有効にするには  
  
1. **[ツール]** メニューの **[オプション]** を選択します。  
  
2. **[テキスト エディター]** フォルダーを展開し、**[すべての言語]** を選択してこのオプションをグローバルに設定するか、または特定の言語フォルダーを選択します  (たとえば、Visual Basic でのみ行番号を表示するには、[テキスト エディター] で [Basic] を選択します)。  
  
3. **[全般]** オプションを選択し、**[設定]** で **[仮想空白文字を使用]** を選択します。  
  
    > [!NOTE]
    > **列の選択**モードで**仮想空白文字**が有効になります。 **仮想空白**モードを有効にしないと、挿入ポイントは行の末尾から次の行の先頭文字に直接移動します。  
  
## <a name="see-also"></a>関連項目
 [エディターのカスタマイズ](../ide/customizing-the-editor.md)   
 [方法: 整列し、固定 Windows](../misc/how-to-arrange-and-dock-windows.md)   
 [[フォントおよび色] ([オプション] ダイアログ ボックス - [環境])](../ide/reference/fonts-and-colors-environment-options-dialog-box.md)
