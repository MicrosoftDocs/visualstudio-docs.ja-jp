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
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 83fc6adeba0529be03a9a982713d0584a2a7bc45
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72661275"
---
# <a name="general-environment-options-dialog-box"></a>[全般] ([オプション] ダイアログ ボックス - [環境])
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

このページを使用して、統合開発環境 (IDE: Integrated Development Environment) のオプションのうち特に配色テーマ、ステータス バーの設定、およびファイル拡張子の関連付けを変更します。 **[オプション]** ダイアログ ボックスを表示するには、 **[ツール]** メニューを開いて、 **[オプション]** をクリックし、 **[環境]** フォルダーを開き、 **[全般]** ページをクリックします。 このページが一覧に表示されない場合は、 **[オプション]** ダイアログ ボックスの **[すべての設定を表示]** チェック ボックスをオンにします。

> [!NOTE]
> 実際に画面に表示されるダイアログ ボックスとメニュー コマンドは、アクティブな設定またはエディションによっては、ヘルプの説明と異なる場合があります。 設定を変更するには、**[ツール]** メニューを開き、**[設定のインポートとエクスポート]** を選択します。 詳細については、「[Visual Studio での開発設定のカスタマイズ](https://msdn.microsoft.com/22c4debb-4e31-47a8-8f19-16f328d7dcd3)」を参照してください。

## <a name="visual-experience"></a>視覚的効果
 **配色テーマ** IDE の **青**、 **明るい** 、または **濃い** 色のテーマを選択します。

 [Visual Studio Marketplace](https://marketplace.visualstudio.com) から **Visual Studio 2015 Color Theme Editor** をダウンロードしてインストールすることで、追加の定義済みテーマをインストールしたり、カスタム テーマを作成したりできます。 このツールをインストールすると、追加の配色テーマが [配色テーマ] ボックスの一覧に表示されます。

 Visual Studio 2015 では、メニューバーのメニューにタイトルの文字種が **既定で適用** されます。 このオプションのチェック ボックスをオフにすると、メニューが**すべて大文字**に設定されます。

 **クライアントのパフォーマンスに基づいて視覚的効果を自動的に調整** するVisual Studio が視覚効果に自動的に調整を設定するか、調整を明示的に設定するかを指定します。 この調整によって、色の表示がグラデーションからフラットに変わったり、メニューまたはポップアップ ウィンドウでのアニメーションの使用が制限されたりすることがあります。

 **リッチクライアントエクスペリエンスを有効にする** グラデーションやアニメーションなど、Visual Studio のビジュアルエクスペリエンスを完全に有効にします。 リモート デスクトップ接続や古いグラフィックス アダプターを使用している場合は、これらの機能のパフォーマンスが低下する可能性があるため、このオプションをオフにします。 このオプションをオンにできるのは、**[クライアントのパフォーマンスに基づいて視覚的効果を自動的に調整する]** をオフにした場合だけです。

 使用**可能な場合はハードウェアのグラフィックスアクセラレータを使用する**ソフトウェアアクセラレータではなく、使用可能な場合はハードウェアのグラフィックスアクセラレータを使用します。

## <a name="other"></a>その他
 **[ウィンドウ] メニューに表示される項目****[ウィンドウ]** メニューの [ウィンドウ] の一覧に表示されるウィンドウ数をカスタマイズします。 1 ～ 24 の範囲の数値を入力します。 既定値は 10 です。

 **最近使用した一覧に表示される項目****[ファイル]** メニューに表示される、最近使ったプロジェクトとファイルの数をカスタマイズします。 1 ～ 24 の範囲の数値を入力します。 既定値は 10 です。 このオプションを使用すると、最近使用したプロジェクトやファイルを簡単に表示できます。

 **ステータス バーの表示** ステータス バーが表示されます。 ステータス バーは IDE ウィンドウの一番下にあり、処理中の操作の進行状況が表示されます。

 **[閉じる] ボタンの影響はアクティブなツールのウィンドウのみ****[閉じる]** ボタンをクリックしたときに、ドッキング セット内のすべてのツール ウィンドウではなく、フォーカスのあるツール ウィンドウだけを閉じるように指定します。 既定では、このオプションが選択されています。

 **[自動的に隠す] ボタンの影響はアクティブなツールのウィンドウのみ****[自動的に隠す]** ボタンをクリックしたときに、ドッキング セット内のすべてのツール ウィンドウではなく、フォーカスのあるツール ウィンドウだけが非表示になるように指定します。 既定では、このチェック ボックスはオフになっています。

 **ファイルの関連付けの管理** [ **Windows のプログラムの関連付けの設定** ] ダイアログボックスを表示します。このダイアログボックスでは、通常、Visual Studio に関連付けられている項目のファイル拡張子と、各種類のファイルを開くための現在の既定のプログラムを表示できます。 関連付けられていないファイルの種類に対して Visual Studio を既定のアプリケーションにするには、ファイル拡張子を選択し、**[保存]** をクリックします。

 このオプションは、同じコンピューターに 2 つのバージョンの Visual Studio がインストールされていて、後で一方のバージョンをアンインストールする場合に役立ちます。 アンインストールすると、Visual Studio ファイルのアイコンがエクスプローラーに表示されなくなります。 さらに、これらのファイルを編集するための既定のアプリケーションが Visual Studio であるとは認識されなくなります。 このオプションは、このような関連付けを復元します。

## <a name="see-also"></a>参照
 [[環境] [オプション] ダイアログ ボックス](../../ide/reference/environment-options-dialog-box.md) [ウィンドウ レイアウトのカスタマイズ](../../ide/customizing-window-layouts-in-visual-studio.md)
