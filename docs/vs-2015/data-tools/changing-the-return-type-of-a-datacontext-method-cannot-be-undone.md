---
title: 元に戻すする DataContext メソッドの戻り値の型を変更することはできません |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-data-tools
ms.topic: conceptual
ms.assetid: 76b161fc-5075-4192-8d94-f15b02e199e9
caps.latest.revision: 6
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: fb8389d3be96f190941e06ef4a822eaf081f281b
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/15/2019
ms.locfileid: "65705555"
---
# <a name="changing-the-return-type-of-a-datacontext-method-cannot-be-undone"></a>DataContext メソッドの戻り値の型を変更すると、元に戻せなくなります
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

DataContext メソッドの戻り値の型を変更すると、元に戻せなくなります。 自動生成された型に戻すには、項目をサーバー エクスプローラー/データベース エクスプローラーから O/R デザイナーにもう一度ドラッグする必要があります。 戻り値の型を変更してもよろしいですか?  
  
 <xref:System.Data.Linq.DataContext> メソッドの戻り値の型は、[!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)]で項目をドロップする場所によって異なります。 既存のエンティティ クラスに項目を直接ドロップすると、そのエンティティ クラスを戻り値の型とする <xref:System.Data.Linq.DataContext> メソッドが作成されます。 [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)]の空の領域に項目をドロップすると、自動生成された型を返す <xref:System.Data.Linq.DataContext> メソッドが作成されます。 <xref:System.Data.Linq.DataContext> メソッドをメソッド ペインに追加した後に、その戻り値の型を変更できます。 <xref:System.Data.Linq.DataContext> メソッドの戻り値の型を確認または変更するには、**[プロパティ]** ウィンドウでそのメソッドを選択し、**[Return Type]** プロパティをクリックします。  
  
### <a name="to-change-the-return-type-of-a-datacontext"></a>DataContext の戻り値の型を変更するには  
  
- **[はい]** をクリックします。  
  
### <a name="to-exit-the-message-box-and-leave-the-return-type-unchanged"></a>メッセージ ボックスを終了し、現在の戻り値の型を維持するには  
  
- **[いいえ]** をクリックします。  
  
### <a name="to-revert-to-the-original-return-type-after-changing-the-return-type"></a>戻り値の型を変更した後で、元の戻り値の型に戻すには  
  
1. <xref:System.Data.Linq.DataContext> で [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)] メソッドを選択し、削除します。  
  
2. **サーバー エクスプローラー/データベース エクスプローラー**で項目を探し、[!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)] にドラッグします。  
  
     元の既定の戻り値の型で <xref:System.Data.Linq.DataContext> メソッドが作成されます。  
  
## <a name="see-also"></a>関連項目  
 [LINQ to Visual Studio での SQL ツール](../data-tools/linq-to-sql-tools-in-visual-studio2.md)   
 [DataContext メソッド (O/R デザイナー)](../data-tools/datacontext-methods-o-r-designer.md)   
 [方法: ストアド プロシージャおよび関数 (O/R デザイナー) にマップされる DataContext メソッドを作成します。](../data-tools/how-to-create-datacontext-methods-mapped-to-stored-procedures-and-functions-o-r-designer.md)   
 [LINQ to SQL](https://msdn.microsoft.com/library/73d13345-eece-471a-af40-4cc7a2f11655)
