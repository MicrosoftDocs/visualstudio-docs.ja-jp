---
title: '方法: [逆アセンブル] ウィンドウを使用して |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.debug.disassembly
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
- assembly language, debugging inline assembly code
- breakpoints, Disassembly window
- Disassembly window
- machine code
ms.assetid: eaf84dd0-c82d-481b-af51-690b74e7794c
caps.latest.revision: 34
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 624be251be9b560f5996a16f3012825d04834758
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63431509"
---
# <a name="how-to-use-the-disassembly-window"></a>方法: 逆アセンブル ウィンドウを使用します。
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

この機能は、アドレス レベルのデバッグが有効になっている場合にのみ使用可能な**オプション**ダイアログ ボックスで、**デバッグ**ノード。 スクリプトまたは SQL のデバッグには使用できません。  
  
 **[逆アセンブル]** ウィンドウには、コンパイラによって作成された命令に対応するアセンブリ コードが表示されます。 マネージド コードをデバッグする場合、これらのアセンブリ命令は、Visual Studio コンパイラが生成した Microsoft Intermediate Language (MSIL) ではなく、Just-In-Time (JIT) コンパイラが作成したネイティブ コードに対応しています。  
  
 **[逆アセンブル]** ウィンドウでは、アセンブリ命令だけでなく、必要に応じて以下の情報も表示できます。  
  
- 各命令が配置されているメモリ アドレス。 ネイティブ アプリケーションの場合は、実際のメモリ アドレスです。 Visual Basic、C#、またはマネージド コードの場合は、関数の先頭からのオフセットです。  
  
- アセンブリ コードの派生元のソース コード。  
  
- コード バイト。これは、実際のマシン語命令または MSIL 命令のバイト表現です。  
  
- メモリ アドレスのシンボル名。  
  
- ソース コードに対応する行番号。  
  
  アセンブリ言語命令は、命令名の省略形であるニーモニックと、変数、レジスタ、および定数を表す記号で構成されます。 各マシン語命令は 1 つのアセンブリ言語ニーモニックで表現され、通常はその後に 1 つ以上の変数、レジスタ、または定数が続きます。  
  
  アセンブリ言語を読み取ることができない状況において [逆アセンブル] ウィンドウを最大限に活用するには、アセンブリ言語プログラミングに関して詳しく説明している文献を参照してください。 [逆アセンブル] ウィンドウに関するこの簡単な紹介では、アセンブリ言語のプログラミングについては説明しません。  
  
  アセンブリ コードは、プロセッサのレジスタ (マネージド コードの場合は共通言語ランタイムのレジスタ) に大きく依存するため、[逆アセンブル] ウィンドウと一緒に [レジスタ] ウィンドウを使用すると、レジスタの内容をチェックできるので便利です。  
  
  ほとんどの場合、アセンブリ言語ではなく生の数値の形式でマシン語コード命令を表示する必要はありません。 ただし、必要に応じて、[メモリ] ウィンドウを使用するか、[逆アセンブル] ウィンドウのショートカット メニューの [コード バイトの表示] を選択すると表示できます。  
  
> [!NOTE]
> 実際に画面に表示されるダイアログ ボックスとメニュー コマンドは、アクティブな設定またはエディションによっては、ヘルプの説明と異なる場合があります。 設定を変更するには、 **[ツール]** メニューの **[設定のインポートとエクスポート]** をクリックします。 詳細については、「 [Visual Studio での開発設定のカスタマイズ](http://msdn.microsoft.com/22c4debb-4e31-47a8-8f19-16f328d7dcd3)」を参照してください。  
  
### <a name="to-display-the-disassembly-window"></a>[逆アセンブル] ウィンドウを表示するには  
  
- **デバッグ** メニューの 選択**Windows**、 をクリック**逆アセンブル**します。  
  
     デバッガーは動作中であるか、中断モードである必要があります。  
  
### <a name="to-turn-optional-information-on-or-off"></a>オプション情報の表示と非表示を切り替えるには  
  
- 右クリックし、**逆アセンブル**ウィンドウで、設定や、ショートカット メニューで目的のオプションをオフにします。  
  
     左マージンの黄色の矢印は、現在の実行ポイントの位置を示します。 ネイティブ コードの場合、これは CPU のプログラム カウンターに対応します。 この位置は、プログラム内で次に実行される命令を示します。  
  
     詳細については、次を参照してください。[上下インメモリ](../debugger/how-to-page-up-or-down-in-memory.md)します。  
  
## <a name="see-also"></a>関連項目  
 [デバッガーでのデータ表示](../debugger/viewing-data-in-the-debugger.md)   
 [方法: [レジスタ] ウィンドウを使用する](../debugger/how-to-use-the-registers-window.md)
