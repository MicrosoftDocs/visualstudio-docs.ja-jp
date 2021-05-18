---
title: '[String ビジュアライザー] ダイアログ ボックス | Microsoft Docs'
description: Visual Studio でのデバッグ中に、組み込みの文字列ビジュアライザー ダイアログ ボックスを使用して文字列を表示します。
ms.date: 10/10/2018
ms.custom: contperf-fy21q4
ms.topic: reference
f1_keywords:
- vs.debug.stringviewer
dev_langs:
- CSharp
- VB
- FSharp
- C++
- JavaScript
helpviewer_keywords:
- string visualizer
- visualizers, string
ms.assetid: 080fd8f1-72b0-461f-8451-3c84d5dc51df
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 85092f6a339fdaaa3ddaa56112cc351d8b8e9bdc
ms.sourcegitcommit: dd2fc6e03a789c044f8438096b8f112e4dba5557
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/06/2021
ms.locfileid: "108640845"
---
# <a name="string-visualizer-dialog-box"></a>[String ビジュアライザー] ダイアログ ボックス

Visual Studio でのデバッグ中に、組み込みの文字列ビジュアライザーを使用して文字列を表示できます。 文字列ビジュアライザーには、データ ヒントまたはデバッガー ウィンドウに対して長すぎる文字列が表示されます。 また、形式に誤りがある文字列を識別するのにも役立ちます。

組み込みの文字列ビジュアライザーには、[テキスト](#text-string-data)、[XML](#xml-string-data)、[HTML](#html-string-data)、[JSON](#json-string-data) の各オプションが含まれています。 [DataSet、DataTable、DataView](../debugger/dataset-visualizer-dialog-box.md) オブジェクトなど、他のいくつかの種類の組み込みビジュアライザーを、 **[自動変数]** またはその他のデバッガー ウィンドウから開くこともできます。

> [!NOTE]
> ビジュアライザーで XAML または WPF の UI 要素を検査する必要がある場合は、「[デバッグ中に XAML のプロパティを調べる](../xaml-tools/inspect-xaml-properties-while-debugging.md)」または「[方法: WPF ツリー ビジュアライザーを使用する](../debugger/how-to-use-the-wpf-tree-visualizer.md)」を参照してください。

文字列ビジュアライザーを開くには、デバッグ中に一時停止する必要があります。 プレーンテキスト、XML、HTML、または JSON 文字列値を持つ変数の上にマウス ポインターを移動し、虫眼鏡アイコン ![ビジュアライザー アイコン](../debugger/media/dbg-tips-visualizer-icon.png "ビジュアライザー アイコン") を選択します。

## <a name="uielement-list"></a>UIElement の一覧

**[式]** フィールドには、マウス ポインターを置いている変数または式が表示されます。

**[値]** フィールドには、文字列値が表示されます。 **[値]** が空白の場合は、選択したビジュアライザーで文字列を認識できないことを意味します。 たとえば、**XML ビジュアライザー** では、XML タグのないテキスト文字列または JSON 文字列に対して、空白の **[値]** が表示されます。 選択したビジュアライザーから認識できない文字列を表示するには、代わりに **[テキスト ビジュアライザー]** を選択します。 **テキスト ビジュアライザー** にはプレーンテキストが表示されます。

### <a name="text-string-data"></a>テキスト文字列データ

**テキスト ビジュアライザー** にはプレーンテキストが表示されます。 C++ 文字列にカスタム書式設定が必要な場合は、[Natvis の視覚化](../debugger/create-custom-views-of-native-objects.md)を作成します。

![テキスト文字列ビジュアライザー](../debugger/media/dbg-string-visualizer-text.png "テキスト文字列ビジュアライザー")

### <a name="json-string-data"></a>JSON 文字列データ

整形式の JSON 文字列は、次の図に示すように JSON ビジュアライザーに表示されます。 形式に誤りがある JSON には、エラー アイコンが表示されることがあります (または、認識できない場合は空白になります)。 JSON エラーを特定するには、文字列をコピーし、[JSLint](https://www.jslint.com/) などの JSON リンティング ツールに貼り付けます。

![JSON 文字列ビジュアライザー](../debugger/media/dbg-tips-string-visualizer-json.png "JSON 文字列ビジュアライザー")

### <a name="xml-string-data"></a>XML 文字列データ

整形式の XML 文字列は、次の図に示すように XML ビジュアライザーに表示されます。 形式に誤りがある XML は、XML タグなしで表示されるか、認識されない場合は空白になります。

![XML 文字列ビジュアライザー](../debugger/media/dbg-string-visualizers-xml.png "XML 文字列ビジュアライザー")

### <a name="html-string-data"></a>HTML 文字列データ

次の図に示すように、整形式の HTML 文字列は、ブラウザーに表示されているかのように表示されます。 形式に誤りがある HTML は、プレーンテキストとして表示される場合があります。

![HTML 文字列ビジュアライザー](../debugger/media/dbg-string-visualizers-html.png "HTML 文字列ビジュアライザー")

## <a name="see-also"></a>関連項目

- [カスタム ビジュアライザーを作成する (C#、Visual Basic)](../debugger/create-custom-visualizers-of-data.md)
- [Visual Studio for Mac でのデータの可視化](/visualstudio/mac/data-visualizations)