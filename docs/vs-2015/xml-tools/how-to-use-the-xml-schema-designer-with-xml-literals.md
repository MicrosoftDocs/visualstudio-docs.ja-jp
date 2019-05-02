---
title: '方法: XML リテラルと XML スキーマ デザイナーを使用して |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-xml-tools
ms.topic: conceptual
ms.assetid: d11803e7-f81a-41a2-a145-ba494a45cc93
caps.latest.revision: 9
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 05c32bfc6c3220739c433ef519b696953bc8b1b4
ms.sourcegitcommit: 1fc6ee928733e61a1f42782f832ead9f7946d00c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2019
ms.locfileid: "60074948"
---
# <a name="how-to-use-the-xml-schema-designer-with-xml-literals"></a>方法: XML リテラルに XML スキーマ デザイナーを使用する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

このトピックでは、Visual Basic プロジェクトの XML リテラルに関連付けられたスキーマを表示する方法について説明します。  
  
### <a name="to-create-a-new-visual-basic-console-application-project"></a>新しい Visual Basic コンソール アプリケーションのプロジェクトを作成するには  
  
1. Visual Studio 2010 を起動します。  
  
2. **ファイル**メニューの **新規**、し、**プロジェクト**します。 **[新しいプロジェクト]** ダイアログ ボックスが表示されます。 **プロジェクトの種類**を選択します**他の言語、** 選び**Visual Basic**します。 **テンプレート**、コンソール アプリケーションを選択します。 入力`XMLLiterals`で、**名前**フィールドとプロジェクトの場所、**場所**フィールド。 **[OK]** をクリックします。  
  
     新しいプロジェクトが作成されます。 XMLLiterals プロジェクトには、Module1.vb という 1 つの Visual Basic ソース ファイルが含まれています。  
  
### <a name="to-add-an-existing-xsd-file-to-the-project"></a>既存の XSD ファイルをプロジェクトに追加するには  
  
1. 開いている新しいテキスト ファイルを Notepad.Copy から XML スキーマのサンプル コード[購買発注書スキーマ](../xml-tools/sample-xsd-file-simple-schema.md)ファイルに貼り付けます。  
  
2. PurchaseOrderSchema.xsd という名前でファイルをどこかに保存します。  
  
3. ソリューション エクスプ ローラーでプロジェクトの名前を右クリックして**追加**、し、**既存の項目**. **既存項目の追加** ダイアログ ボックスが表示されます。 PurchaseOrderSchema.xsd ファイルを参照し、選択しをクリックして**追加**します。  
  
     XMLLiterals プロジェクトには、2 つのファイルが含まれています。Module1.vb および PurchaseOrderSchema.xsd します。  
  
### <a name="to-add-visual-basic-code-with-an-xml-literal-based-on-the-xsd-file-included-in-the-project"></a>プロジェクトに含まれる XSD ファイルに基づいて XML リテラルの Visual Basic コードを追加するには  
  
1. Module1.vb ファイルのコードを次のコードに置き換えます。  
  
    ```  
    Imports <xmlns:ns="http://tempuri.org/PurchaseOrderSchema.xsd">  
  
    Module Module1  
        Sub Main()  
  
            Dim XMLLiteral = <ns:PurchaseOrder OrderDate="1900-01-01">  
                                 <ns:ShipTo country="US">  
                                     <ns:name>name1</ns:name>  
                                     <ns:street>street1</ns:street>  
                                     <ns:city>city1</ns:city>  
                                     <ns:state>state1</ns:state>  
                                     <ns:zip>1</ns:zip>  
                                 </ns:ShipTo>  
                                 <ns:BillTo country="US">  
                                     <ns:name>name1</ns:name>  
                                     <ns:street>street1</ns:street>  
                                     <ns:city>city1</ns:city>  
                                     <ns:state>state1</ns:state>  
                                     <ns:zip>1</ns:zip>  
                                 </ns:BillTo>  
                             </ns:PurchaseOrder>  
  
        End Sub  
    End Module  
    ```  
  
2. XML リテラルまたは XML 名前空間インポートでの任意の XML ノードを右クリックして**スキーマ エクスプ ローラーで表示する**します。  
  
     XML スキーマ エクスプローラーが、XML スキーマ セットに関連付けられた XML リテラルを持つ Visual Basic ファイルと並んで表示されます。
