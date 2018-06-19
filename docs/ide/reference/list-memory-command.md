---
title: ListMemory コマンド
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- debug.listmemory
helpviewer_keywords:
- Debug.ListMemory command
- ListMemory command
- list memory command
ms.assetid: a84de361-a6a6-4f6d-96aa-a0d4a424371e
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 9f3ce3aee4a7a498600da4eb0c99210c9c20d00f
ms.sourcegitcommit: fe5a72bc4c291500f0bf4d6e0778107eb8c905f5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/07/2018
ms.locfileid: "33703420"
---
# <a name="list-memory-command"></a>ListMemory コマンド
指定範囲のメモリの内容を表示します。

## <a name="syntax"></a>構文

```cmd
Debug.ListMemory [/ANSI|Unicode] [/Count:number] [/Format:formattype]
[/Hex|Signed|Unsigned] [expression]
```

## <a name="arguments"></a>引数
 `expression`

 任意。 メモリの表示を開始するメモリ アドレス。

## <a name="switches"></a>スイッチ
 /ANSI&#124;Unicode

 任意。 メモリを、メモリ バイトに対応する ANSI 文字または Unicode 文字として表示します。

 /Count:`number`

 任意。 表示するメモリを `expression` からのバイト数で指定します。

 /Format:`formattype`

 任意。 **[メモリ]** ウィンドウにメモリ情報を表示する場合の形式の種類は、OneByte、TwoBytes、FourBytes、EightBytes、Float (32 ビット)、または Double (64 ビット) を指定できます。 OneByte を使用する場合、`/Unicode` は使用できません。

 /Hex&#124;Signed&#124;Unsigned

 任意。 数字の表示形式を、符号付き、符号なし、または 16 進数のいずれかに指定します。

## <a name="remarks"></a>コメント
 すべてのスイッチを指定して完全な **Debug.ListMemory** コマンドを記述する代わりに、特定のスイッチが指定された値に事前に設定された定義済みのエイリアスを使用してコマンドを起動することもできます。 以下に例を示します。

```cmd
>Debug.ListMemory /Format:float /Count:30 /Unicode
```

 上のコードを入力する代わりに、次のように記述できます。

```cmd
>df /Count:30 /Unicode
```

 **Debug.ListMemory** コマンドで使用できるエイリアスの一覧を以下に示します。

|Alias|コマンドおよびスイッチ|
|-----------|--------------------------|
|**d**|Debug.ListMemory|
|**da**|Debug.ListMemory /Ansi|
|**db**|Debug.ListMemory /Format:OneByte|
|**dc**|Debug.ListMemory /Format:FourBytes /Ansi|
|**dd**|Debug.ListMemory /Format:FourBytes|
|**df**|Debug.ListMemory /Format:Float|
|**dq**|Debug.ListMemory /Format:EightBytes|
|**du**|Debug.ListMemory /Unicode|

## <a name="example"></a>例

```cmd
>Debug.ListMemory /Format:float /Count:30 /Unicode
```

## <a name="see-also"></a>参照

- [ListCallStack コマンド](../../ide/reference/list-call-stack-command.md)
- [ListThreads コマンド](../../ide/reference/list-threads-command.md)
- [Visual Studio のコマンド](../../ide/reference/visual-studio-commands.md)
- [コマンド ウィンドウ](../../ide/reference/command-window.md)
- [検索コマンド ボックス](../../ide/find-command-box.md)
- [Visual Studio コマンドのエイリアス](../../ide/reference/visual-studio-command-aliases.md)