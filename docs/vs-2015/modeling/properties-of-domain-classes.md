---
title: ドメイン クラスのプロパティ |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: reference
helpviewer_keywords:
- Domain-Specific Language, domain class
ms.assetid: a3993995-19e7-4761-a972-b1de89131a1b
caps.latest.revision: 23
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 1a5f2b2fa8c2ff39b0a7ec3e982145567602ab10
ms.sourcegitcommit: 8b538eea125241e9d6d8b7297b72a66faa9a4a47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/23/2019
ms.locfileid: "58973119"
---
# <a name="properties-of-domain-classes"></a>ドメイン クラスのプロパティ
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

ドメイン クラスでは、次の表に、プロパティがあります。 ドメイン クラスについては、次を参照してください。[理解のモデル、クラスとリレーションシップ](../modeling/understanding-models-classes-and-relationships.md)します。 これらのプロパティを使用する方法の詳細については、次を参照してください。[をカスタマイズすると、ドメイン固有言語を拡張する](../modeling/customizing-and-extending-a-domain-specific-language.md)します。  
  
|プロパティ|説明|既定値|  
|--------------|-----------------|-------------|  
|アクセス修飾子|ドメイン クラスのアクセスのレベル (`public` または `internal`)。|`public`|  
|カスタム属性|このドメイン クラスから生成されるソース コードのクラスに属性を追加するために使用します。|\<none>|  
|Double 型を生成します派生。|場合`True`、基底クラスと (オーバーライドによってカスタマイズをサポート) する部分クラスの両方が生成されます。 詳細については、次を参照してください。[をオーバーライドすると、生成されたクラスを拡張する](../modeling/overriding-and-extending-the-generated-classes.md)します。|`False`|  
|カスタム コンストラクターがあります。|場合`True`、カスタム コンストラクターは、ソース コードで提供されます。 詳細については、次を参照してください。[をオーバーライドすると、生成されたクラスを拡張する](../modeling/overriding-and-extending-the-generated-classes.md)します。|`False`|  
|継承修飾子|ドメイン クラスから生成されるソース コードのクラスの継承の種類について説明します (`none`、`abstract`または`sealed`)。|`none`|  
|基本クラス|このドメイン クラスが派生の場合、基底クラスの名前。|\<none>|  
|名前|このドメイン クラスの名前。|現在の名前|  
|名前空間|このドメイン クラスの名前空間。|現在の名前空間|  
|メモ|このドメイン クラスに関連付けられている非公式のメモ。|\<none>|  
|説明|生成されたデザイナーの UI を文書化するために使用する説明。|\<none>|  
|表示名|このドメイン クラスの生成されたデザイナーに表示される名前です。|\<none>|  
|ヘルプ キーワード|このドメイン クラスの F1 ヘルプのインデックスを作成するために使用する省略可能なキーワード。|\<none>|  
  
## <a name="see-also"></a>関連項目  
 [ドメイン固有言語ツールの用語集](http://msdn.microsoft.com/ca5e84cb-a315-465c-be24-76aa3df276aa)
