---
title: 書式設定すると、XML、テキスト エディターのオプション ダイアログ ボックス |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-xml-tools
ms.topic: conceptual
ms.assetid: bb539b3a-027c-4b2f-906e-403e0e22ba8d
caps.latest.revision: 9
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 588bf415a801a9244cd9a046e0c503c0b238db58
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63417417"
---
# <a name="formatting-xml-text-editor-options-dialog-box"></a>[書式設定] ([オプション] ダイアログ ボックス - [テキスト エディター] - [XML])
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

このダイアログ ボックスでは、XML エディターの書式設定を指定することができます。 アクセスできる、**オプション** ダイアログ ボックスから、**ツール**メニュー。  
  
> [!NOTE]
> 選択すると、これらの設定は使用可能な**テキスト エディター**フォルダー、 **XML**フォルダーをクリックし、**書式設定**オプションを**のオプション**  ダイアログ ボックス。  
  
## <a name="attributes"></a>属性  
 **手動による属性の書式設定を保持する**  
 属性の書式は再設定されません。 既定値です。  
  
> [!NOTE]
> 属性が複数行にわたっている場合、エディターは親要素のインデントに対応するように属性の各行にインデントを設定します。  
  
 **独自の行の属性を整列します。**  
 最初の属性のインデントに対応するように、2 番目およびそれ以降の行頭を揃えて配置します。 XML テキストで属性がどのように並べられるかについて例を次に示します。  
  
```  
<item id = "123-A"  
      name = "hammer"  
      price = "9.95">  
</item>  
```  
  
## <a name="auto-reformat"></a>自動による書式の再設定  
 **クリップボードから貼り付け時に**  
 クリップボードから貼り付ける XML テキストの書式を再設定します。  
  
 **終了タグの完成時**  
 終了タグが完了したときに要素の書式を再設定します。  
  
## <a name="mixed-content"></a>混合コンテンツ  
 **既定では混合コンテンツを保持します。**  
 エディターで混合コンテンツの書式を再設定するかどうかを指定します。 既定では、コンテンツが `xml:space="preserve"` スコープで見つかった場合を除き、エディターは混合コンテンツの書式を再設定しようとします。  
  
 要素にテキストとマークアップが混在して含まれている場合、そのコンテンツは混合コンテンツと見なされます。 混合コンテンツを持つ要素の例を次に示します。  
  
```  
<dir>c:\data\AlphaProject\  
  <file readOnly="false">test1.txt</file>  
  <file readOnly="false">test2.txt</file>  
</dir>  
```  
  
## <a name="see-also"></a>関連項目  
 [XML ドキュメントのプロパティと [プロパティ] ウィンドウ](../xml-tools/xml-document-properties-properties-window.md)   
 [XML エディターのコンポーネント](../xml-tools/xml-editor-components.md)
