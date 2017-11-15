---
title: "方法: 型の間の関連付けを作成する (クラス デザイナー) | Microsoft Docs"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology: vs-ide-general
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: vs.classdesigner.associationline
helpviewer_keywords:
- types [Visual Studio], associations
- association lines, defining (Class Designer)
- defining association lines (Class Designer)
- associations, types
- association lines
ms.assetid: adccb9c8-2f8a-4086-9fa9-f70f99fb6e00
caps.latest.revision: "20"
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: 69c1a3ddb60008f14dd76aeef224c040c7faace3
ms.sourcegitcommit: f40311056ea0b4677efcca74a285dbb0ce0e7974
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/31/2017
---
# <a name="how-to-create-associations-between-types-class-designer"></a>方法: 型の間の関連付けを作成する (クラス デザイナー)
クラス デザイナーの関連行は、ダイアグラムのクラスの関係を示します。 関連行は、プロジェクト内の別のクラスのプロパティまたはフィールドの型であるクラスを表します。 関連行は、一般に、プロジェクト内のクラス間の最も重要な関係を示すために使用されます。  
  
 すべてのフィールドとプロパティを関連付けとして表示できますが、ダイアグラムで強調する対象に応じて、重要なメンバーだけを関連付けとして表示する方が有意義です。 重要度の低いメンバーを通常のメンバーとして表示するか、それらのメンバーを完全に非表示にできます。  
  
> [!NOTE]
>  クラス デザイナーでは、一方向の関連付けだけがサポートされます。  
  
### <a name="to-define-an-association-line-in-the-class-diagram"></a>クラス ダイアグラムに関連行を定義するには  
  
1.  クラス デザイナーのツールボックスで、**[関連]** を選択します。  
  
2.  関連付けでリンクする 2 つの図形間に線を描画します。  
  
     新しいプロパティが最初のクラスに作成されます。 このプロパティは、図形のコンパートメント内のプロパティとしてではなく、既定の名前を持つ関連行として表示されます。 その型は、関連行が指す図形です。  
  
### <a name="to-change-the-name-of-an-association"></a>関連付けの名前を変更するには  
  
-   ダイアグラム領域で、関連行のラベルをクリックし、編集します。  
  
 \- または  
  
1.  関連付けとして表示されるプロパティを含む図形をクリックします。  
  
     図形がフォーカスを取得し、図形のメンバーが [クラスの詳細] ウィンドウと [プロパティ] ウィンドウに表示されます。  
  
2.  [クラスの詳細] ウィンドウまたは [プロパティ] ウィンドウで、そのプロパティの名前フィールドを編集し、Enter キーを押します。  
  
     **[クラスの詳細]** ウィンドウ、関連行、[プロパティ] ウィンドウ、およびコード上の名前が更新されます。  
  
## <a name="see-also"></a>関連項目  
 [方法: メンバー表記と関連付け表記の間で変更する (クラス デザイナー)](../ide/how-to-change-between-member-notation-and-association-notation-class-designer.md)