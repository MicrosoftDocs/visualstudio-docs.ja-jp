---
title: '方法: ActiveX コントロールのデバッグ |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vc.controls.debug
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- testing [Visual Studio], test containers
- ActiveX control container debugging [Visual Studio]
- debugging ActiveX controls
- data-bound controls, ActiveX
- test container
- containers, specifying for debug sessions
- ActiveX controls, debugging
- testing [Visual Studio], ActiveX controls
ms.assetid: bbc02cf7-a7e6-44fe-99af-87a43e1d7251
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 385f5c9e03aaeb84cf33c6d76a499b0d1e35d5c3
ms.sourcegitcommit: 2193323efc608118e0ce6f6b2ff532f158245d56
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 01/25/2019
ms.locfileid: "54931987"
---
# <a name="how-to-debug-an-activex-control"></a>方法: ActiveX コントロールをデバッグする

> [!NOTE]
> 実際に画面に表示されるダイアログ ボックスとメニュー コマンドは、アクティブな設定またはエディションによっては、ヘルプの説明と異なる場合があります。 設定を変更するには、[ツール] メニューの [設定のインポートとエクスポート] をクリックします。 詳細については、「[リセット設定](../ide/environment-settings.md#reset-settings)」を参照してください。

ActiveX コントロールをデバッグするには、そのコントロールが実行されるコンテナー (実行可能ファイル) を指定する必要があります。

## <a name="to-specify-a-container-for-the-debug-session"></a>デバッグ セッションのコンテナーを指定するには

1.  ソリューション エクスプローラーでプロジェクトを選択します。

2.  **ビュー** ] メニューの [選択**プロパティ ページ**します。

3.  **[プロジェクト プロパティ ページ]** ダイアログ ボックスで、**[構成プロパティ]** フォルダーを開き、**[デバッグ]** を選択します。

4.  **[デバッグ]** カテゴリの **[コマンド]** プロパティを探します。

5.  コンテナーのパス名を指定します。 たとえば、「C:\Program Files\Internet Explorer\IEXPLORE.EXE」のように指定します。

6.  Internet Explorer をコンテナーとして指定し、アクティブ デスクトップを使用している場合は、**[コマンド引数]** ボックスに「`/new`」と入力します。

7.  **[OK]** をクリックします。

     **[プロジェクト プロパティ ページ]** ダイアログ ボックスでコンテナーを指定しなかった場合でも、デバッグを開始するときにコンテナーを指定できます。 実行コマンドを選択してデバッグを開始するときに、[[デバッグ セッションで実行可能] ダイアログ ボックス](../debugger/executable-for-debugging-session-dialog-box.md)が表示されます。 ダイアログ ボックスにコンテナーのパス名を指定します。

## <a name="see-also"></a>関連項目

- [ActiveX コントロール](/cpp/mfc/activex-controls)
- [テスト コンテナーでのプロパティとイベントのテスト](/cpp/mfc/testing-properties-and-events-with-test-container)
- [COM および ActiveX のデバッグ](../debugger/com-and-activex-debugging.md)
- [Visual Studio でのデバッグ](../debugger/index.md)
- [デバッガーでのはじめに](../debugger/debugger-feature-tour.md)