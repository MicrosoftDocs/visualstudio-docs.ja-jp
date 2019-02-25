---
title: '[全般]([オプション] ダイアログ ボックス - [環境]) | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- VS.Message.0x800a002e
- VS.ToolsOptionsPages.Environment.General
- VS.Environment.General
helpviewer_keywords:
- MRU lists
- windows, customizing
- MDI, environment options
- speed, environment animation
- File menu
- menus, customizing
- Windows menu customizing
- status bars, displaying
- Visual Studio Start page, setting
- IDE, startup options
- editors, autocompletion
- Options dialog box, General Environment
- General Environment Options dialog box
ms.assetid: 90fc2e6f-572f-4384-96d8-5678299ce58e
caps.latest.revision: 38
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 836c5be9df565d6171949845e36febc22024b20a
ms.sourcegitcommit: 8b538eea125241e9d6d8b7297b72a66faa9a4a47
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 01/23/2019
ms.locfileid: "54752291"
---
# <a name="general-environment-options-dialog-box"></a>[全般] ([オプション] ダイアログ ボックス - [環境])
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

  
このページを使用して、統合開発環境 (IDE: Integrated Development Environment) のオプションのうち特に配色テーマ、ステータス バーの設定、およびファイル拡張子の関連付けを変更します。 **[オプション]** ダイアログ ボックスを表示するには、**[ツール]** メニューを開いて、**[オプション]** をクリックし、**[環境]** フォルダーを開き、**[全般]** ページをクリックします。 このページが一覧に表示されない場合は、**[オプション]** ダイアログ ボックスの **[すべての設定を表示]** チェック ボックスをオンにします。  
  
> [!NOTE]
>  実際に画面に表示されるダイアログ ボックスとメニュー コマンドは、アクティブな設定またはエディションによっては、ヘルプの説明と異なる場合があります。 設定を変更するには、**[ツール]** メニューを開き、**[設定のインポートとエクスポート]** を選択します。 詳細については、「 [Visual Studio での開発設定のカスタマイズ](http://msdn.microsoft.com/22c4debb-4e31-47a8-8f19-16f328d7dcd3)」を参照してください。  
  
## <a name="visual-experience"></a>視覚的効果  
 **[配色テーマ]**  
 IDE の配色テーマで **[青]**、**[淡色]** または **[濃色]** を選択します。  
  
 [Visual Studio ギャラリー](https://visualstudiogallery.msdn.microsoft.com/site/search?f%5B0%5D.Type=RootCategory&f%5B0%5D.Value=tools)から **Visual Studio 2015 配色テーマ エディター**をダウンロードしてインストールすることで、追加の定義済みテーマをインストールし、カスタム テーマを作成することもできます。 このツールをインストールすると、追加の配色テーマが [配色テーマ] ボックスの一覧に表示されます。  
  
 タイトルの文字スタイルをメニュー バーに適用  
 Visual Studio 2015 で、既定では、メニューは**タイトルの文字スタイル**になります。 このオプションのチェック ボックスをオフにすると、メニューが**すべて大文字**に設定されます。  
  
 **クライアントのパフォーマンスに基づいて視覚的効果を自動的に調整する**  
 Visual Studio で視覚的効果を自動的に調整するか、ユーザーが明示的に調整するかを指定します。 この調整によって、色の表示がグラデーションからフラットに変わったり、メニューまたはポップアップ ウィンドウでのアニメーションの使用が制限されたりすることがあります。  
  
 **リッチ クライアント エクスペリエンスを有効にする**  
 グラデーションやアニメーションなど、Visual Studio の視覚的効果のすべてを有効にします。 リモート デスクトップ接続や古いグラフィックス アダプターを使用している場合は、これらの機能のパフォーマンスが低下する可能性があるため、このオプションをオフにします。 このオプションをオンにできるのは、**[クライアントのパフォーマンスに基づいて視覚的効果を自動的に調整する]** をオフにした場合だけです。  
  
 **可能ならハードウェアのグラフィックス アクセラレータを使用する**  
 可能な場合は、ソフトウェア アクセラレータではなく、ハードウェアのグラフィックス アクセラレータを使用します。  
  
## <a name="other"></a>その他  
 **項目をウィンドウ メニューに表示**  
 **[ウィンドウ]** メニューの [ウィンドウ] の一覧に表示されるウィンドウ数をカスタマイズします。 1 ～ 24 の値を入力します。 既定値は 10 です。  
  
 **項目を最近使用した一覧に表示**  
 **[ファイル]** メニューに表示される、最近使ったプロジェクトとファイルの数をカスタマイズします。 1 ～ 24 の値を入力します。 既定値は 10 です。 このオプションを使用すると、最近使用したプロジェクトやファイルを簡単に表示できます。  
  
 **ステータス バーの表示**  
 ステータス バーが表示されます。 ステータス バーは IDE ウィンドウの一番下にあり、処理中の操作の進行状況が表示されます。  
  
 **[閉じる] ボタンを、アクティブなツール ウィンドウに対してのみ実行する**  
 **[閉じる]** をクリックしたときに、ドッキング セット内のすべてのツール ウィンドウではなく、フォーカスのあるツール ウィンドウだけを閉じるように指定します。 既定では、このチェック ボックスはオンになっています。  
  
 **[自動的に隠す] ボタンを、アクティブなツール ウィンドウに対してのみ実行する**  
 **[自動的に隠す]** をクリックしたときに、ドッキング セット内のすべてのツール ウィンドウではなく、フォーカスのあるツール ウィンドウだけを自動的に非表示にするように指定します。 既定では、このチェック ボックスはオフになっています。  
  
 **ファイルの関連付けの管理**  
 **[Windows のプログラムの関連付けを設定する]** ダイアログ ボックスを表示します。そこには、一般に Visual Studio に関連付けられている項目のファイル拡張子とそれぞれの種類のファイルを開く現在の既定のプログラムが表示されます。 関連付けられていないファイルの種類に対して Visual Studio を既定のアプリケーションにするには、ファイル拡張子を選択し、**[保存]** をクリックします。  
  
 このオプションは、同じコンピューターに 2 つのバージョンの Visual Studio がインストールされていて、後で一方のバージョンをアンインストールする場合に役立ちます。 アンインストールすると、Visual Studio ファイルのアイコンがエクスプローラーに表示されなくなります。 さらに、これらのファイルを編集するための既定のアプリケーションが Visual Studio であるとは認識されなくなります。 このオプションは、このような関連付けを復元します。  
  
## <a name="see-also"></a>関連項目
 [[環境] ([オプション] ダイアログ ボックス)](../../ide/reference/environment-options-dialog-box.md)   
 [ウィンドウ レイアウトをカスタマイズする](../../ide/customizing-window-layouts-in-visual-studio.md)
