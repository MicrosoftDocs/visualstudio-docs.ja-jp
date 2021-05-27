---
title: Office ソリューションのイベント ログ
description: Windows のイベント ビューアーを使用し、Visual Studio Tools for Office ランタイムによってキャプチャされた例外メッセージを表示する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Office applications [Office development in Visual Studio], event viewer
- ClickOnce deployment [Office development in Visual Studio], event viewer
- deploying applications [Office development in Visual Studio], event viewer
- Office development in Visual Studio, event viewer
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: fb38c08e807c65845c323671b0c82151f5c8567c
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99910364"
---
# <a name="event-logging-for-office-solutions"></a>Office ソリューションのイベント ログ
  Windows のイベント ビューアーを使用すると、Office ソリューションのインストール時またはアンインストール時に [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] でキャプチャされる例外メッセージを表示できます。 イベント ロガーからのこれらのメッセージを使用して、インストールと配置の問題を解決できます。

 [!INCLUDE[appliesto_all](../vsto/includes/appliesto-all-md.md)]

## <a name="read-the-event-log"></a>イベント ログを読む
 **イベント ビューアー** を開き、目的のイベントを表示するためにフィルター処理します。

### <a name="to-read-the-event-log-in-windows-server-2003-and-windows-xp"></a>Windows Server 2003 と Windows XP でイベント ログを読むには

1. [コントロール パネル] の **[管理ツール]** を開きます。

2. **イベント ビューアー** を開始します。

3. イベント ログの一覧で **[アプリケーション]** を選択します。

4. **[表示]** メニューの **[フィルター]** をクリックします。

5. **[イベント ソース]** 一覧で **[VSTO 4.0]** を選択します。

6. インストール イベントの場合は、 **[イベント ID]** ボックスに **4096** と入力します。

7. **[OK]** をクリックして、フィルター処理されたビューを表示します。

### <a name="to-read-the-event-log-in-windows-7-windows-vista-and-windows-server-2008"></a>Windows 7、Windows Vista、Windows Server 2008 でイベント ログを読むには

1. [コントロール パネル] の **[管理ツール]** を開きます。

2. **イベント ビューアー** を開始します。

3. **[Windows ログ]** を展開します。

4. イベント ログの一覧で **[アプリケーション]** を選択します。

5. **[操作]** メニューの **[現在のログをフィルター]** をクリックします。

6. **[イベント ソース]** 一覧で **[VSTO 4.0]** を選択します。

7. インストール イベントの場合は、 **[イベント ID]** ボックスに **4096** と入力します。

8. **[OK]** をクリックして、フィルター処理されたビューを表示します。

   イベント ビューアーに次の情報が表示されます。

- ソリューションの配置マニフェストの場所。

- エラーまたは例外の原因を説明するメッセージ。

  これらの例外メッセージから、信頼されていない証明書、信頼されていないドキュメントの場所、無効な配置マニフェストといったインストール上の問題の原因を特定できます。

  Office ソリューションをアンインストールしても、例外メッセージはイベント ログに残ります。

  Office ソリューションの実行中、例外メッセージを表示するか、ログに記録する方法については、「[Office プロジェクトのデバッグ](../vsto/debugging-office-projects.md)」を参照してください。

### <a name="localization"></a>ローカリゼーション
 例外メッセージの言語は、Office ランタイム言語の Visual Studio Tools によって決まります。 たとえば、エンドユーザーのコンピューターに日本語の言語パックがインストールされている場合、例外メッセージは日本語でイベント ログに書き込まれます。

## <a name="disable-the-event-logger"></a>イベント ロガーを無効にする
 Office ソリューションをインストールまたはアンインストールするときには、既定ではイベント ロガーが有効になります。 イベント ロガーを無効にするには、VSTO_EVENTLOGDISABLED 環境変数を「1」に設定します。

### <a name="to-disable-the-event-log"></a>イベント ログを無効にするには

1. [コントロール パネル] の **[システム]** を開きます。

2. **[詳細設定]** タブの **[環境変数]** をクリックします。

3. **[システム変数]** ウィンドウの **[新規]** をクリックします。

4. **[新しいシステム変数]** ダイアログ ボックスで、 **[変数名]** ボックスに **VSTO_EVENTLOGDISABLED** と入力します。

5. **[変数値]** ボックスに **1** と入力します。

6. **[OK]** をクリックします。

## <a name="see-also"></a>関連項目
- [Office ソリューションを配置する](../vsto/deploying-an-office-solution.md)
- [Office ソリューションの配置のトラブルシューティング](../vsto/troubleshooting-office-solution-deployment.md)
