---
title: ページファイル タブの プロセス プロパティ ダイアログ ボックス |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- Process properties for Windows NT
ms.assetid: daf41a06-8a55-48f6-95f5-49a8416bd308
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 25dc3b0aca1b58c18ae4038540c14fc4dbfe4036
ms.sourcegitcommit: b0d8e61745f67bd1f7ecf7fe080a0fe73ac6a181
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 02/22/2019
ms.locfileid: "56720849"
---
# <a name="page-file-tab-process-properties-dialog-box"></a>[ページ ファイル] タブ ([プロセス プロパティ] ダイアログ ボックス)
使用して、**ページファイル**タブ プロセスのページング ファイルを確認します。 表示する、[プロセス プロパティ ダイアログ ボックス](../debugger/process-properties-dialog-box.md)、フォーカスを移動、[プロセス ビュー](../debugger/processes-view.md)ウィンドウ。 ツリーで、プロセスの任意のノードを選択し、**プロパティ**から、**ビュー**メニュー。

 次の設定は [使用可能な**ページファイル**] タブ。

|入力|説明|
|-----------|-----------------|
|**ページ ファイル サイズ**|ページング ファイル内でこのプロセスを使用しているページの現在数。 ページング ファイルには、ページのプロセスによって使用されますが、その他のファイルに含まれていないデータが格納されます。 ページング ファイルはすべてのプロセスによって使用され、ページング ファイル内の領域が不足している他のプロセスが実行中にエラーが発生します。|
|**ピーク ページ ファイルのサイズ**|ページング ファイル内でこのプロセスが使用されるページの最大数。|
|**ページ フォールト**|このプロセスで実行するスレッドによるページ フォールトの数。 ページ フォールトでは、スレッドがその作業をメイン メモリに設定されていない仮想メモリ ページを参照するときに発生します。 したがって、ページは取得されませんディスクからスタンバイ リスト上にある場合ため、メイン メモリ上に既にをもう 1 つ使用されているかどうか、またはのページを共有して処理します。|