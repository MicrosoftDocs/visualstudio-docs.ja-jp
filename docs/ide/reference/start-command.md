---
title: Start コマンド
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- debug.start
helpviewer_keywords:
- Start command
- Debug.Start command
ms.assetid: dc4e4aa2-b0ab-4e00-92db-6dc3058ddc21
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 8f455306a87c82c5cd4fe55ccacdbba070b4467c
ms.sourcegitcommit: 5216c15e9f24d1d5db9ebe204ee0e7ad08705347
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/09/2019
ms.locfileid: "68926028"
---
# <a name="start-command"></a>Start コマンド
スタートアップ プロジェクトのデバッグを開始します。

## <a name="syntax"></a>構文

```cmd
Debug.Start [address]
```

## <a name="arguments"></a>引数
`address`

任意。 プログラムの実行を中断するアドレス。ソース コードでのブレークポイントに似ています。 この引数は、デバッグ モードでのみ有効です。

## <a name="remarks"></a>解説
**Start** コマンドを実行すると、指定したアドレスまで RunToCursor 操作が実行されます。

## <a name="example"></a>例
この例では、デバッガーを起動し、発生した例外はすべて無視されます。

```cmd
>Debug.Start
```

## <a name="see-also"></a>関連項目

- [Visual Studio のコマンド](../../ide/reference/visual-studio-commands.md)
- [コマンド ウィンドウ](../../ide/reference/command-window.md)
- [検索コマンド ボックス](../../ide/find-command-box.md)
- [Visual Studio Command Aliases](../../ide/reference/visual-studio-command-aliases.md)