---
title: SetCurrentStackFrame コマンド
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- debug.setcurrentstackframe
helpviewer_keywords:
- Set Current Stack Frame command
- Debug.SetCurrentStackFrame command
ms.assetid: 3dcf52c0-6781-4598-bac2-0094dce67c20
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 24880f997d604d3db11ae19a6220c2789da7648f
ms.sourcegitcommit: 5216c15e9f24d1d5db9ebe204ee0e7ad08705347
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/09/2019
ms.locfileid: "68926076"
---
# <a name="set-current-stack-frame-command"></a>SetCurrentStackFrame コマンド
特定のスタック フレームを設定できます。

## <a name="syntax"></a>構文

```cmd
Debug.SetCurrentStackFrame index
```

## <a name="arguments"></a>引数
`index`

必須です。 インデックスでスタック フレームを選びます。

## <a name="example"></a>例

```cmd
>Debug.SetCurrentStackFrame 1
```

## <a name="see-also"></a>関連項目

- [Visual Studio のコマンド](../../ide/reference/visual-studio-commands.md)
- [コマンド ウィンドウ](../../ide/reference/command-window.md)
- [検索コマンド ボックス](../../ide/find-command-box.md)
- [Visual Studio Command Aliases](../../ide/reference/visual-studio-command-aliases.md)