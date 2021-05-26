---
title: EditorConfig をサポートするために言語サービスを拡張する
description: EditorConfig ファイルをサポートするように言語サービスを更新するために行う変更について説明します。 言語固有のグローバル オプションをコンテキスト オプションに置き換えます。
ms.custom: SEO-VS-2020
ms.date: 11/22/2017
ms.topic: conceptual
helpviewer_keywords:
- editorconfig [extensibility]
- editorconfig, supporting in a language service
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: c3754c40ec1142684b5041341b22035eaec06ec8
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105056260"
---
# <a name="supporting-editorconfig-for-your-language-service"></a>言語サービスでの EditorConfig のサポート

[EditorConfig](https://editorconfig.org/) ファイルを使用すると、プロジェクトごとに、インデント サイズなどの一般的なテキスト エディター オプションを記述できます。 Visual Studio での EditorConfig ファイルのサポートの詳細については、[EditorConfig を使用した移植可能なエディター設定の作成](../ide/create-portable-custom-editor-options.md)に関するページをご覧ください。

ほとんどの場合、Visual Studio 言語サービスを実装するとき、EditorConfig ユニバーサル プロパティをサポートするための追加の作業は必要ありません。 ユーザーがファイルを開くと、コア エディターが .editorconfig ファイルを自動的に検出して読み込み、適切なテキスト バッファーとビュー オプションを設定します。 ただし、タブやスペースなどの編集の場合、一部の言語サービスでは、グローバル設定を使用するのではなく、コンテキストに基づいた適切なテキスト ビュー オプションを使用しようとします。 そのような場合は、EditorConfig ファイルをサポートするように言語サービスを更新する必要があります。

以下は、_言語固有_ のグローバル オプションを _コンテキスト_ オプションに置き換えることで、EditorConfig ファイルをサポートするように言語サービスを更新するために必要な変更です。

## <a name="indent-style"></a>インデント スタイル

言語固有のオプション | コンテキスト オプション
-------|--------
Microsoft.VisualStudio.TextManager.Interop.LANGPREFERENCES.fInsertTabs<br/>Microsoft.VisualStudio.Package.LanguagePreferences.InsertTabs|!textBufferOptions.GetOptionValue(DefaultOptions.ConvertTabsToSpacesOptionId)<br/>!textView.Options.GetOptionValue(DefaultOptions.ConvertTabsToSpacesOptionId)

## <a name="indent-size"></a>[インデント サイズ]

言語固有のオプション | コンテキスト オプション
-------|--------
Microsoft.VisualStudio.TextManager.Interop.LANGPREFERENCES.uIndentSize<br/>Microsoft.VisualStudio.Package.LanguagePreferences.InsertTabs.IndentSize|textBufferOptions.GetOptionValue(DefaultOptions.IndentSizeOptionId)<br/>textView.Options.GetOptionValue(DefaultOptions.IndentSizeOptionId)

## <a name="tab-size"></a>[タブ サイズ]

言語固有のオプション | コンテキスト オプション
-------|--------
Microsoft.VisualStudio.TextManager.Interop.LANGPREFERENCES.uTabSize<br/>Microsoft.VisualStudio.Package.LanguagePreferences.InsertTabs.TabSize|textBufferOptions.GetOptionValue(DefaultOptions.TabSizeOptionId)<br/>textView.Options.GetOptionValue(DefaultOptions.TabSizeOptionId)

## <a name="see-also"></a>関連項目

- [EditorConfig を使用して移植可能なエディター設定を作成する](../ide/create-portable-custom-editor-options.md)
- [エディターと言語サービスの拡張](../extensibility/extending-the-editor-and-language-services.md)
