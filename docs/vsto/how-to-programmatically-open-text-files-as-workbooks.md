---
title: '方法: プログラムによってテキスト ファイルをブックとして開く'
description: Visual Studio を使用して、プログラムによってテキスト ファイルを Microsoft Excel ブックとして開く方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- workbooks, opening text files as
- text [Office development in Visual Studio], text files
- text files, opening as workbooks
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 14a73d7a06c3d79c15df5b823b38efc9ddceb846
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2021
ms.locfileid: "107824173"
---
# <a name="how-to-programmatically-open-text-files-as-workbooks"></a>方法: プログラムによってテキスト ファイルをブックとして開く
  テキスト ファイルをブックとして開くことができます。 開くテキスト ファイルの名前を渡す必要があります。 ファイル内の解析を開始する行番号やデータの列の形式など、いくつかの省略可能なパラメーターを指定できます。

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

## <a name="example"></a>例
 :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs" id="Snippet80":::
 :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb" id="Snippet80":::

## <a name="compile-the-code"></a>コードのコンパイル
 この例には、次のコンポーネントが必要です。

- 少なくとも 3 行のテキストを含む、`Test.txt` という名前のコンマ区切りのテキスト ファイル。

- ドライブ C に格納するテキスト ファイル `Test.txt`。

## <a name="see-also"></a>関連項目
- [ブックを操作する](../vsto/working-with-workbooks.md)
- [方法: プログラムによってブックを開く](../vsto/how-to-programmatically-open-workbooks.md)
- [方法: プログラムによって新しいブックを作成する](../vsto/how-to-programmatically-create-new-workbooks.md)
- [方法: プログラムによってブックを保存する](../vsto/how-to-programmatically-save-workbooks.md)
- [方法: プログラムによってブックを閉じる](../vsto/how-to-programmatically-close-workbooks.md)
- [Office ソリューションの省略可能なパラメーター](../vsto/optional-parameters-in-office-solutions.md)
