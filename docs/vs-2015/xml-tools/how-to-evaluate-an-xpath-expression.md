---
title: '方法: XPath 式を評価する |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-xml-tools
ms.topic: conceptual
ms.assetid: 159ba4ef-75e4-4ac8-80dc-e064e0bec345
caps.latest.revision: 5
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: ecec9004506a9bd05d3d773e44bb264af363f96f
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72670861"
---
# <a name="how-to-evaluate-an-xpath-expression"></a>方法 : XPath 式を評価する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

XPath 式は、 **[クイックウォッチ]** ダイアログボックスで評価できます。 XPath 式は、W3C XPath 1.0 勧告に沿って有効である必要があります。 現在の XSLT コンテキスト ( **[ローカル]** ウィンドウの [`self::node()`] ノード) は、XPath 式の評価コンテキストを提供します。

 XPath 式を評価する際にどの機能がサポートされるかについて次の一覧に示します。

- 組み込みの XPath 関数はサポートされます。

- 組み込みの XSLT 関数はサポートされません。

- ユーザー定義関数はサポートされません。

> [!NOTE]
> 次の手順では、「[チュートリアル: XSLT スタイルシートのデバッグ](../xml-tools/walkthrough-debug-an-xslt-style-sheet.md)」のトピックで説明されている、前の例の xml ファイルと books.xml ファイルを使用します。

### <a name="to-evaluate-an-xpath-expression"></a>XPath 式を評価するには

1. `xsl:if` 開始タグにブレークポイントを挿入します。

2. XML エディターのツールバーにある **[XSL のデバッグ]** ボタンをクリックします。

     デバッガーが起動され、`xsl:if` タグで実行が中断されます。

3. 右クリックして **[クイックウォッチ]** を選択します。

     **[クイックウォッチ]** ダイアログボックスが表示されます。

4. **[クイックウォッチ]** ダイアログボックスの **[式]** フィールドに `./price/text()` を入力し、再 **[評価]** をクリックします。

     **[値]** ボックスに、現在の book ノードの価格が表示されます。

5. XPath 式を `./price/text() < $bookAverage` に変更し、[再**評価**] をクリックします。

     **[値]** ボックスに、XPath 式が `true` として評価されたことが表示されます。

## <a name="see-also"></a>参照
 [XSLT のデバッグ](../xml-tools/debugging-xslt.md)
