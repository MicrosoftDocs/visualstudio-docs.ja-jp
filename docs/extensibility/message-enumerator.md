---
title: メッセージ列挙子 | Microsoft Docs
description: この列挙子のメンバーは、IDE が SccOpenProject を呼び出すときに提供するコールバック関数である TEXTOUTPROC 関数のために使用されます。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- message enumerator
- source control plug-ins, message enumeration
ms.assetid: 4a4faa0d-d352-40ea-a21d-c09ea286a8e1
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 77c49f79ccdcfc4aa0325b89dfb38f3f8d4da721
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2021
ms.locfileid: "112902593"
---
# <a name="message-enumerator"></a>メッセージ列挙子
次のフラグは、IDE が [SccOpenProject](../extensibility/sccopenproject-function.md) を呼び出すときに提供するコールバック関数である `TEXTOUTPROC` 関数のために使用されます (コールバック関数の詳細については、[LPTEXTOUTPROC](../extensibility/lptextoutproc.md) を参照)。

 IDE は、プロセスをキャンセルするよう依頼される場合、いずれかのキャンセル メッセージを受け取る可能性があります。 この場合、ソース管理プラグインでは `SCC_MSG_STARTCANCEL` を使用して、IDE に **[キャンセル]** ボタンを表示するよう依頼します。 この後、一連の通常のメッセージが送信される可能性があります。 これらのうちのいずれかが `SCC_MSG_RTN_CANCEL` を返した場合、プラグインは操作を終了して戻ります。 プラグインではまた、`SCC_MSG_DOCANCEL` を定期的にポーリングして、ユーザーが操作をキャンセルしたかどうかも判定します。 すべての操作が完了するか、またはユーザーがキャンセルした場合、プラグインでは `SCC_MSG_STOPCANCEL` を送信します。 `SCC_MSG_INFO`、SCC_MSG_WARNING、SCC_MSG_ERROR の各種類は、メッセージのスクロール リストに表示されるメッセージのために使用されます。 `SCC_MSG_STATUS` は、テキストがステータス バーまたは一時的な表示領域に表示されることを示す特殊な種類です。 その一覧に永続的に残るわけではありません。

## <a name="syntax"></a>構文

```
enum { 
   SCC_MSG_RTN_CANCEL = -1, 
   SCC_MSG_RTN_OK = 0, 
   SCC_MSG_INFO = 1 
   SCC_MSG_WARNING, 
   SCC_MSG_ERROR, 
   SCC_MSG_STATUS, 
   SCC_MSG_DOCANCEL, 
   SCC_MSG_STARTCANCEL, 
   SCC_MSG_STOPCANCEL 
};
```

## <a name="members"></a>メンバー
 SCC_MSG_RTN_CANCEL コールバックから戻ってキャンセルを示します。

 SCC_MSG_RTN_OK コールバックから戻って続行します。

 SCC_MSG_INFO 情報メッセージを示します。

 SCC_MSG_WARNING 警告メッセージを示します。

 SCC_MSG_ERROR エラー メッセージを示します。

 SCC_MSG_STATUS ステータス バー用のメッセージを示します。

 SCC_MSG_DOCANCEL テキストはなく、IDE では `SCC_MSG_RTN_OK` または `SCC_MSG_RTN_CANCEL` を返します。

 SCC_MSG_STARTCANCEL キャンセル ループを開始します。

 SCC_MSG_STOPCANCEL キャンセル ループを停止します。

## <a name="see-also"></a>関連項目
- [ソース管理プラグイン](../extensibility/source-control-plug-ins.md)
- [LPTEXTOUTPROC](../extensibility/lptextoutproc.md)
