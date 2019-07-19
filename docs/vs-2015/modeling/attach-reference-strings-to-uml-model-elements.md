---
title: UML モデル要素に参照文字列をアタッチ |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: reference
helpviewer_keywords:
- UML - extending, reference strings
ms.assetid: 15dbed99-efce-42fe-a768-714a5804e7d1
caps.latest.revision: 11
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: bd5a1ae4abc2e0b5c508b7b77160bbf8da3bb45e
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "68203225"
---
# <a name="attach-reference-strings-to-uml-model-elements"></a>UML モデル要素に参照文字列をアタッチする
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

モデル要素に任意の文字列をアタッチするコードを作成できます。 たとえば文字列は、URI の場合もあれば、キャッシュされた計算結果や、別のモデル内の要素への ModelBus 参照の場合もあります。 各文字列は IReference オブジェクトに含まれています。 任意の数の IReference オブジェクトを、各モデル要素にアタッチすることができます。  
  
 各 IReference オブジェクトには Name があります。 この Name を使って、参照値を解釈する方法を示すことができます。 たとえば、Name を ”URI” に設定して、値を URI として解釈するように示すことができます。 モデリング ツールによって使われる、定義済みの参照名がいくつかあります。  
  
## <a name="attaching-a-reference-to-an-ielement"></a>IElement への参照のアタッチ  
 次のメソッドを使用するのには、以下への参照を追加する必要があります。  
  
 Microsoft.VisualStudio.ArchitectureTools.Extensibility.dll  
  
 コード内に次のディレクティブを挿入する必要があります。  
  
 `using Microsoft.VisualStudio.ArchitectureTools.Extensibility.Uml;`  
  
|メソッド呼び出し|説明|  
|-----------------|-----------------|  
|`element.AddReference (nameString, valueString, duplicatesAllowed)`|指定された名前と値の文字列で `IReference` を作成し、`element` にリンクします。 `IReference` を返します。<br /><br /> `duplicatesAllowed` が False で、同じ名前の `IReference` が `element` に既にアタッチされている場合は、例外をスローします。|  
|`element.GetReferences(name)`|指定された `IReference` を持つ `element` にリンクされた、すべての `name` オブジェクトが返されます。|  
|`element.DeleteAllReferences(name)`|指定された名前を持つ要素にリンクされた、すべての `IReference` オブジェクトが返されます。|  
|`reference.Delete()`|この `IReference` を削除します。|  
|`ReferenceConstants.WorkItem`|作業項目参照に名前を付けるために使われる値。|  
  
## <a name="see-also"></a>関連項目  
 [作業項目リンク ハンドラーを定義します。](../modeling/define-a-work-item-link-handler.md)   
 [定義およびモデリング拡張機能のインストール](../modeling/define-and-install-a-modeling-extension.md)   
 [UML API を使用したプログラミング](../modeling/programming-with-the-uml-api.md)
