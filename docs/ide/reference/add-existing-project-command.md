---
title: AddExistingProject コマンド
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- file.addexistingproject
helpviewer_keywords:
- Add Existing Project command
- File.AddExistingProject
ms.assetid: 71cf3e31-c76b-405b-ad6a-1b1bc654bd40
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: b5a511e19394b397096a5a5ba2e339166454138e
ms.sourcegitcommit: 5216c15e9f24d1d5db9ebe204ee0e7ad08705347
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/09/2019
ms.locfileid: "68926280"
---
# <a name="add-existing-project-command"></a>AddExistingProject コマンド
既存のプロジェクトを現在のソリューションに追加します。

## <a name="syntax"></a>構文

```cmd
File.AddExistingProject filename
```

## <a name="arguments"></a>引数
`filename`\
任意。 ソリューションに追加するプロジェクトの完全なパスとプロジェクト名 (拡張子付き)。

`filename` 引数にスペースが含まれる場合は、引用符で囲む必要があります。

ファイル名が指定されていない場合、ファイルを開くダイアログ ボックスが表示され、ユーザーがプロジェクトを選択できます。

## <a name="remarks"></a>解説
オート コンプリートでは、入力された正しいパスとファイル名の検索を試みます。

## <a name="example"></a>例
この例では、[!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)] プロジェクトの TestProject1 を現在のソリューションに追加します。

```cmd
>File.AddExistingProject "c:\visual studio projects\TestProject1.vbproj"
```

## <a name="see-also"></a>関連項目

- [Visual Studio のコマンド](../../ide/reference/visual-studio-commands.md)
- [コマンド ウィンドウ](../../ide/reference/command-window.md)
- [検索コマンド ボックス](../../ide/find-command-box.md)
- [Visual Studio Command Aliases](../../ide/reference/visual-studio-command-aliases.md)