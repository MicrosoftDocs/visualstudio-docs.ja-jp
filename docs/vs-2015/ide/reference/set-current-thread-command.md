---
title: SetCurrentThread コマンド | Microsoft ドキュメント
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- debug.setcurrentthread
helpviewer_keywords:
- Set Current Thread command
- Debug.SetCurrentThread command
ms.assetid: 9917ed1d-6c30-4d94-b2f0-69acce74f1b2
caps.latest.revision: 20
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 67bf0d37e6f734fa4b3229488bc3eee2732c3063
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72665443"
---
# <a name="set-current-thread-command"></a>SetCurrentThread コマンド
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

指定したスレッドを現在のスレッドとして設定します。

## <a name="syntax"></a>構文

```
Debug.SetCurrentThread index
```

## <a name="arguments"></a>引数
 `index` 必須。 スレッドをそのインデックスで選択します。

## <a name="example"></a>例

```
>Debug.SetCurrentThread 1
```

## <a name="see-also"></a>参照
 [Visual Studio コマンド](../../ide/reference/visual-studio-commands.md)の [コマンドウィンドウ](../../ide/reference/command-window.md)の [検索/コマンドボックス](../../ide/find-command-box.md) [visual studio コマンドのエイリアス](../../ide/reference/visual-studio-command-aliases.md)
