---
title: データセットを XML として保存する
description: データセットを XML として保存します。 GetXml や WriteXml など、データセットの使用可能な XML メソッドを呼び出すことによって、データセット内の XML データにアクセスします。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- XML [Visual Basic], datasets
- data [Visual Studio], saving as XML
- datasets [Visual Basic], saving as XML
- saving data
ms.assetid: 68b8327c-ae05-49ff-b9ba-99183e70b52c
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
- data-storage
ms.openlocfilehash: 42974852a3051fd3473b6b23d880eeb38b966b95
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/02/2021
ms.locfileid: "106216203"
---
# <a name="save-a-dataset-as-xml"></a>データセットを XML として保存する

データセットの使用可能な XML メソッドを呼び出すことによって、データセット内の XML データにアクセスします。 XML 形式でデータを保存するには、<xref:System.Data.DataSet> の <xref:System.Data.DataSet.GetXml%2A> メソッドまたは <xref:System.Data.DataSet.WriteXml%2A> メソッドのいずれかを呼び出します。

<xref:System.Data.DataSet.GetXml%2A> メソッドを呼び出すと、XML として書式設定された、データセット内のすべてのデータ テーブルのデータを含む文字列が返されます。

<xref:System.Data.DataSet.WriteXml%2A> メソッドを呼び出すと、指定したファイルに XML 形式のデータが送信されます。

## <a name="to-save-the-data-in-a-dataset-as-xml-to-a-variable"></a>データセットのデータを XML として変数に保存するには

- <xref:System.Data.DataSet.GetXml%2A> メソッドが <xref:System.String> を返します。 <xref:System.String> 型の変数を宣言し、<xref:System.Data.DataSet.GetXml%2A> メソッドの結果を代入します。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataSaving/VB/Class1.vb" id="Snippet12":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataSaving/CS/Class1.cs" id="Snippet12":::

## <a name="to-save-the-data-in-a-dataset-as-xml-to-a-file"></a>データセットのデータを XML としてファイルに保存するには

- <xref:System.Data.DataSet.WriteXml%2A> メソッドには複数のオーバーロードがあります。 変数を宣言し、ファイルを保存する有効なパスを代入します。 次のコードでは、データをファイルに保存する方法を示します。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataSaving/VB/Class1.vb" id="Snippet13":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataSaving/CS/Class1.cs" id="Snippet13":::

## <a name="see-also"></a>関連項目

- [データをデータベースに保存する](../data-tools/save-data-back-to-the-database.md)
