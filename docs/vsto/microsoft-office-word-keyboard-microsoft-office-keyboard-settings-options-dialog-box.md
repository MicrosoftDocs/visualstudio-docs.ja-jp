---
title: Microsoft Office Word キーボード、Microsoft Office Keyboard 設定、オプション ダイアログ ボックス
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
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 6506fec976822ea4a4e675c9961395c952a7a35f
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "62970306"
---
# <a name="microsoft-office-word-keyboard-microsoft-office-keyboard-settings-options-dialog-box"></a>Microsoft Office Word キーボード、Microsoft Office Keyboard 設定、オプション ダイアログ ボックス
  Microsoft Office Word と Visual Studio 両方のショートカット キーを処理します。 同じショートカット キーの組み合わせは、Word と Visual Studio のさまざまなコマンドのスタンバイことができます。 Word が Visual Studio でのドキュメント レベルのプロジェクトで開いているときは、一度に 1 つだけのアプリケーションは、ショートカット キーのコマンドを受け取ります。 既定では、Visual Studio がショートカット キー、すべてのコマンドを受け取りますが、Word ドキュメントにフォーカスがある場合は、選択して、受信を行うことができます**ダイナミック キーボード スキーム**します。

 ショートカット キーを現在処理しているアプリケーションでのコマンドに割り当てられていないショートカット キーを使用する場合は、他のアプリケーションへショートカット キーが渡されます。

 選択したオプションは、変更するまで Word プロジェクトで有効になります。 選択範囲では Microsoft Office Excel プロジェクトには影響しませんMicrosoft Office Excel キーボード オプションを使用して Excel の変更を行う必要があります。

## <a name="uielement-list"></a>UIElement の一覧
 **Visual Studio のキーボード スキーム**Word 文書にフォーカスがある場合でも、Visual Studio がショートカット キー、すべてのコマンドを受信します。 たとえば、ファンクション キーを押して**F5** Visual Studio の起動時、ソリューションのデバッグ ドキュメントにフォーカスがあります。

 **ダイナミック キーボード スキーム**フォーカスがある場合にのみ、Visual Studio がショートカット キーのコマンドを受信します。 Word 文書にフォーカスがある場合は、Word はすべてのショートカット キーのコマンドを受信します。 関数キーを押す場合など**f5 キーを押して**Word が開き、Word 文書にフォーカスがある、**検索し、置換** ダイアログ ボックスで、**ジャンプ**タブを選択します。 キーを押す場合**F5** Visual Studio にフォーカスがある Visual Studio は、ソリューションのデバッグを開始します。

## <a name="see-also"></a>関連項目
- [Microsoft Office Excel Keyboard、Microsoft Office Keyboard 設定、オプション ダイアログ ボックス](../vsto/microsoft-office-excel-keyboard-microsoft-office-keyboard-settings-options-dialog-box.md)
