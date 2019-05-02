﻿---
title: '方法: 目次のトピックが見つかります |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
f1_keywords:
- hv_contents
helpviewer_keywords:
- Help Viewer 2.0, table of contents filtering
- Help Viewer 2.0, Contents tab
- Contents tab [Help Viewer 2.0]
- table of contents filtering [Help Viewer 2.0]
ms.assetid: 8b98464d-2b05-4710-ad68-5647e78c6b7b
caps.latest.revision: 14
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 8ab015fdfd459dbb13e81deed0fe0cc89f71cd1f
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63416688"
---
# <a name="how-to-find-topics-in-the-table-of-contents"></a>方法: 目次でトピックを検索する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

**[目次]** タブでは、目次 (TOC) を使用して情報を検索できます。 目次は、インストールしたブックに関するトピックをすべて含む、拡張可能なリストです。 TOC 内の移動方法に関するユーザー補助情報については、「[ショートカット キー (ヘルプ ビューアー)](../ide/shortcut-keys-help-viewer.md)」を参照してください。  
  
> [!IMPORTANT]
> TOC で使用できるトピックの範囲は、選択したフィルターによって異なります。  
  
## <a name="filter-the-toc"></a>TOC のフィルター処理  
 TOC をフィルター処理して、**[目次]** タブに表示されるトピックの範囲を絞り込むことができます。指定した用語のルートがタイトルに含まれている場合にのみ、一覧にタイトルが表示されます。 たとえば、フィルターとして「troubleshooting」を指定すると、「troubleshoot」または「troubleshooting」を含むタイトルのみが表示されます。 タイトルに用語が含まれないノードは、省略記号 (...) と共に単一のノードに折りたたまれます。  
  
#### <a name="to-filter-the-toc"></a>TOC をフィルター処理するには  
  
1. **[目次]** タブをクリックします。  
  
2. **[フィルターの内容]** テキスト ボックスに、用語を入力します。  
  
> [!NOTE]
> フィルターの実行に時間がかかる場合は、高度な検索演算子 `title:` を使用すると、結果がすばやく表示される場合があります。  
  
## <a name="synchronize-a-topic-with-the-toc"></a>TOC とのトピックの同期  
 インデックスまたはフルテキストの検索機能を使用してトピックを開いている場合は、トピック ウィンドウと TOC を同期させることによって、TOC のどこにこのトピックがあるかを特定できます。  
  
#### <a name="to-synchronize-the-toc-with-the-topic-window"></a>TOC をトピック ウィンドウと同期させるには  
  
1. トピックを表示します。  
  
2. ツール バーの **[目次のトピックを表示]** ボタンをクリックするか、Ctrl+S キーを押します。  
  
     **[目次]** タブが開き、TOC 内のトピックの場所が表示されます。  
  
## <a name="see-also"></a>関連項目
 [情報の検索](../ide/locate-information.md)   
 [Microsoft Help Viewer](../ide/microsoft-help-viewer.md)
