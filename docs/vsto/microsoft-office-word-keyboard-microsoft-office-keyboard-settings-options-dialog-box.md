---
title: Office Word キーボード ([オプション] ダイアログ ボックス - [設定])
description: '[ダイナミック キーボード スキーム] を選択してドキュメントにフォーカスがあるときに、Microsoft Word でショートカット キー コマンドを受け取れるようにする方法について説明します。'
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: conceptual
f1_keywords:
- VS.ToolsOptionsPages.Microsoft_Office_Tools.Microsoft_Office_Word.Keyboard
- VS.ToolsOptionsPages.Microsoft_Office_Keyboard_Settings.Microsoft_Office_Word_Keyboard
- VST.WordOptions.KeyboardMappingScheme
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- keyboard shortcuts, Office development in Visual Studio
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 0138fcd73ddf07202a9111ec2b3d17dcc0fb7a0e
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99879424"
---
# <a name="microsoft-office-word-keyboard-settings-options-dialog-box"></a>[Microsoft Office Word キーボード] ([オプション] ダイアログ ボックス - [設定])
  Microsoft Office Word と Visual Studio の両方で、ショートカット キーが処理されます。 同じショートカット キーの組み合わせによって表されるコマンドが、Word と Visual Studio で異なる場合があります。 Visual Studio のドキュメント レベルのプロジェクトで Word が 開かれている場合、ショートカット キーのコマンドを受け取るアプリケーションは一度に 1 つだけです。 既定では、Visual Studio がすべてのショートカット キー コマンドを受け取りますが、**ダイナミック キーボード スキーム** を選択することによってドキュメントにフォーカスがあるときは、Word でそれらを受け取れるようにすることができます。

 現在ショートカット キーを処理しているアプリケーションのコマンドに割り当てられていないショートカット キーを使用すると、そのショートカット キーは他のアプリケーションに渡されます。

 選択したオプションは、変更するまで、Word プロジェクトに対して有効なままになります。 この選択は、Microsoft Office Excel プロジェクトには影響しません。Excel に対する変更は、Microsoft Office Excel のキーボード オプションを使用して行う必要があります。

## <a name="uielement-list"></a>UIElement の一覧
 **[Visual Studio キーボード スキーム]** Word 文書にフォーカスがある場合でも、Visual Studio がすべてのショートカット キー コマンドを受け取ります。 たとえば、文書にフォーカスがある状態でファンクション キー **F5** を押すと、Visual Studio によってソリューションのデバッグが開始されます。

 **[ダイナミック キーボード スキーム]** Visual Studio は、フォーカスがあるときにのみショートカット キー コマンドを受け取ります。 Word 文書にフォーカスがあるときは、Word がすべてのショートカット キー コマンドを受け取ります。 たとえば、Word 文書にフォーカスがあるときにファンクション キー **F5** を押すと、Word の **[検索と置換]** ダイアログ ボックスが開き、 **[ジャンプ]** タブが選択されます。 Visual Studio にフォーカスがあるときに **F5** キーを押すと、ソリューションのデバッグが開始されます。

## <a name="see-also"></a>関連項目
- [[Microsoft Office Excel キーボード] ([オプション] ダイアログ ボックス - [Microsoft Office Keyboard 設定])](../vsto/microsoft-office-excel-keyboard-microsoft-office-keyboard-settings-options-dialog-box.md)
