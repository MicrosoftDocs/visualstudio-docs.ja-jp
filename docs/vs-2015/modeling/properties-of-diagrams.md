---
title: 図のプロパティ |Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-tfs-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- vs.dsltools.dsldesigner.dsldiagram
helpviewer_keywords:
- Domain-Specific Language, diagram
ms.assetid: 00bba4b8-6aa6-4027-96cb-4f4c41a77d3c
caps.latest.revision: 27
author: gewarren
ms.author: gewarren
manager: douge
ms.openlocfilehash: 9db932bb5e19cdc10dde3cd8330c4a57208a0c2d
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/12/2018
ms.locfileid: "49280905"
---
# <a name="properties-of-diagrams"></a>図のプロパティ
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

生成されたデザイナーでのダイアグラムの表示方法を指定するプロパティを設定することができます。 たとえば、図でテキストの既定の色を指定できます。  
  
 詳細については、[ドメイン固有言語を定義する方法](../modeling/how-to-define-a-domain-specific-language.md)を参照してください。 これらのプロパティを使用する方法の詳細については、[をカスタマイズすると、ドメイン固有言語を拡張する](../modeling/customizing-and-extending-a-domain-specific-language.md)を参照してください。  
  
 次の表は、図のプロパティを一覧表示します。  
  
|プロパティ|説明|既定値|  
|--------------|-----------------|-------------|  
|[塗りつぶしの色]|ダイアグラムの塗りつぶしの色。|白|  
|テキストの色|ダイアグラムで表示されるテキストの色。|黒|  
|アクセス修飾子|(パブリックまたは内部) クラスのアクセス修飾子。|Public|  
|カスタム属性|生成されたコード クラスに属性を追加するために使用します。|\<なし >|  
|Double 型を生成します派生。|場合`True`、基底クラスと (オーバーライドによってカスタマイズをサポート) する部分クラスの両方が生成されます。 詳細については、[をオーバーライドすると、生成されたクラスを拡張する](../modeling/overriding-and-extending-the-generated-classes.md)を参照してください。|False|  
|カスタム コンス トラクターがあります。|場合`True`、カスタム コンス トラクターは、ソース コードで提供されます。 詳細については、次を参照してください[をオーバーライドすると、生成されたクラスを拡張する](../modeling/overriding-and-extending-the-generated-classes.md)..|False|  
|継承修飾子|ダイアグラムから生成されるソース コードのクラスの継承の種類について説明します (`none`、`abstract`または`sealed`)。|なし|  
|基本ダイアグラム|この図の基本クラス。|(なし)|  
|名前|このダイアグラムの名前。|現在の名前|  
|名前空間|この図に関連付けられた名前空間。|現在の名前空間|  
|表されるクラス|この図を表すルート ドメイン クラス。|該当する場合、現在のルート クラス|  
|メモ|この要素に関連付けられている非公式のメモ。|\<なし >|  
|プロパティとして公開塗りつぶしの色|場合`True`ユーザーは、生成されたデザイナーのダイアグラムの塗りつぶしの色を設定できます。 これを設定するダイアグラムの図形を右クリックし、をクリックして**追加 Explosed**します。|False|  
|テキストの色をプロパティとして公開します|場合`True`ユーザーは、生成されたデザイナーで、ダイアグラムのテキストの色を設定することができます。 これを設定するダイアグラムの図形を右クリックし、をクリックして**追加 Explosed**します。|False|  
|説明|生成されたデザイナーのドキュメントに使用される説明です。|\<なし >|  
|表示名|このダイアグラムの生成されたデザイナーに表示される名前です。|\<なし >|  
|ヘルプ キーワード|このダイアグラムの F1 ヘルプのインデックスを作成するために使用するキーワードです。|\<なし >|  
  
## <a name="see-also"></a>関連項目  
 [ドメイン固有言語ツールの用語集](http://msdn.microsoft.com/en-us/ca5e84cb-a315-465c-be24-76aa3df276aa)



