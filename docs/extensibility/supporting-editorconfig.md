---
title: EditorConfig をサポートするために言語サービスを拡張します。
ms.date: 11/22/2017
ms.topic: conceptual
helpviewer_keywords:
- editorconfig [extensibility]
- editorconfig, supporting in a language service
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: be9502569fd57da630da949ba14bbfc5e9045a22
ms.sourcegitcommit: 117ece52507e86c957a5fd4f28d48a0057e1f581
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/28/2019
ms.locfileid: "66261812"
---
# <a name="supporting-editorconfig-for-your-language-service"></a>EditorConfig 言語サービスのサポート

[EditorConfig](http://editorconfig.org/)ファイルを使用すると、プロジェクトごとに、インデント サイズなどの一般的なテキスト エディター オプションについて説明します。 EditorConfig ファイルの Visual Studio のサポートについての詳細については、次を参照してください。 [EditorConfig を使用して移植可能なエディターの設定を作成する](../ide/create-portable-custom-editor-options.md)します。

ほとんどの場合、Visual Studio 言語サービスを実装するとき、EditorConfig ユニバーサル プロパティをサポートするための追加の作業は必要ありません。 ユーザーがファイルを開くと、コア エディターが .editorconfig ファイルを自動的に検出して読み込み、適切なテキスト バッファーとビュー オプションを設定します。 ただし、タブやスペースなどの編集、一部の言語サービスはグローバル設定を使用するのではなく、適切なコンテキストに基づいてテキストの表示 オプションを使用して選択します。 そのような場合は、EditorConfig ファイルをサポートするように言語サービスを更新する必要があります。

グローバルに置き換えることで、EditorConfig ファイルをサポートするために言語サービスを更新するために必要な変更は、次_言語固有_オプションは、_コンテキスト_オプション。

## <a name="indent-style"></a>インデント スタイル

言語固有のオプション | コンテキストのオプション
-------|--------
Microsoft.VisualStudio.TextManager.Interop.LANGPREFERENCES.fInsertTabs<br/>Microsoft.VisualStudio.Package.LanguagePreferences.InsertTabs|!textBufferOptions.GetOptionValue(DefaultOptions.ConvertTabsToSpacesOptionId)<br/>!textView.Options.GetOptionValue(DefaultOptions.ConvertTabsToSpacesOptionId)

## <a name="indent-size"></a>[インデント サイズ]

言語固有のオプション | コンテキストのオプション
-------|--------
Microsoft.VisualStudio.TextManager.Interop.LANGPREFERENCES.uIndentSize<br/>Microsoft.VisualStudio.Package.LanguagePreferences.InsertTabs.IndentSize|textBufferOptions.GetOptionValue(DefaultOptions.IndentSizeOptionId)<br/>textView.Options.GetOptionValue(DefaultOptions.IndentSizeOptionId)

## <a name="tab-size"></a>[タブ サイズ]

言語固有のオプション | コンテキストのオプション
-------|--------
Microsoft.VisualStudio.TextManager.Interop.LANGPREFERENCES.uTabSize<br/>Microsoft.VisualStudio.Package.LanguagePreferences.InsertTabs.TabSize|textBufferOptions.GetOptionValue(DefaultOptions.TabSizeOptionId)<br/>textView.Options.GetOptionValue(DefaultOptions.TabSizeOptionId)

## <a name="see-also"></a>関連項目

- [EditorConfig を使用して移植可能なエディターの設定を作成します。](../ide/create-portable-custom-editor-options.md)
- [エディターと言語サービスを拡張します。](../extensibility/extending-the-editor-and-language-services.md)