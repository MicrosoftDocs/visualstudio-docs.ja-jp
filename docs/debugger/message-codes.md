---
title: コードのメッセージ |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- message codes
ms.assetid: 9f91f4e2-c1f1-4349-9f11-2fbbf59654be
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 1c09245056bf7e947985bfa55dc9cc4a3a96b8cf
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "62846274"
---
# <a name="message-codes"></a>メッセージ コード
表示される各メッセージ行[メッセージ ビュー](../debugger/messages-view.md) 'P' を含むの 'の' または 'R' コード。 これらのコードでは、次の意味があります。

|コード|説明|
|----------|-------------|
|P|メッセージがキューにポストされた、 **PostMessage**関数。 情報のメッセージの最終的な廃棄に関連はありません。|
|S|メッセージが送信された、 **SendMessage**関数。 これは、送信者は、受信側の処理し、メッセージを返すまでは制御を回復しないことを意味します。 受信側は、センダーに送り返す戻り値を返すため、ことができます。|
|s|メッセージが送信されましたが、セキュリティでは、戻り値にアクセスができなくなります。|
|R|それぞれの ' の行が 'R' (戻り値) の対応する行をメッセージの戻り値の一覧を表示します。 場合によってメッセージ呼び出しは入れ子に、その 1 つのメッセージ ハンドラーは、別のメッセージを送信することを意味します。|