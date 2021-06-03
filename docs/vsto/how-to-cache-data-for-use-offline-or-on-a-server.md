---
title: '方法: オフラインで使用するデータまたはサーバー上で使用するデータをキャッシュする'
description: データ項目をドキュメントへのキャッシュ対象としてマークして、オフラインで使用できるようにします。 これにより、ドキュメント内のデータを他のコードで操作できるようになります。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- data caching [Office development in Visual Studio], server use
- Office applications [Office development in Visual Studio], data
- datasets [Office development in Visual Studio], caching
- offline data [Office development in Visual Studio]
- data [Office development in Visual Studio], caching
- data caching [Office development in Visual Studio], offline use
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 07d7a33d90fd9d05c041ddc27f92a5b6a59bb75e
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2021
ms.locfileid: "107825993"
---
# <a name="how-to-cache-data-for-use-offline-or-on-a-server"></a>方法: オフラインで使用するデータまたはサーバー上で使用するデータをキャッシュする
  データ項目をドキュメントへのキャッシュ対象としてマークすると、オフラインで使用できるようになります。 これにより、ドキュメントがサーバーに格納されている場合に、ドキュメント内のデータを他のコードで操作することも可能になります。

 [!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]

 データ項目をコード内で宣言するときに、または <xref:System.Data.DataSet> を使用している場合は **[プロパティ]** ウィンドウでプロパティを設定することにより、データ項目をキャッシュ対象としてマークできます。 <xref:System.Data.DataSet> または <xref:System.Data.DataTable> ではないデータ項目をキャッシュする場合は、ドキュメントにキャッシュするための条件を満たしていることを確認してください。 詳細については、「[キャッシュ データ](../vsto/caching-data.md)」を参照してください。

> [!NOTE]
> **Cached** および **WithEvents** とマークされている Visual Basic を使用して作成されたデータセット ( **[データ ソース]** ウィンドウまたは **[ツールボックス]** からドラッグされた、**CacheInDocument** プロパティが **True** に設定されているデータセットも含む) には、キャッシュ内で名前の先頭にアンダースコアが付きます。 たとえば、データセットを作成して **Customers** という名前を付けた場合、キャッシュ内の <xref:Microsoft.VisualStudio.Tools.Applications.CachedDataItem> の名前は **_Customers** になります。 <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument> を使用してこのキャッシュされた項目にアクセスする場合は、**Customers** の代わりに **_Customers** を指定する必要があります。

### <a name="to-cache-data-in-the-document-using-code"></a>コードを使用してドキュメントにデータをキャッシュするには

1. データ項目のパブリック フィールドまたはパブリック プロパティを、プロジェクト内のホスト項目クラス (Word プロジェクトの `ThisDocumen`t クラスや、Excel プロジェクトの `ThisWorkbook` クラスなど) のメンバーとして宣言します。

2. このメンバーに <xref:Microsoft.VisualStudio.Tools.Applications.Runtime.CachedAttribute> 属性を適用して、ドキュメントのデータ キャッシュに格納するデータ項目としてマークします。 次の例では、この属性を <xref:System.Data.DataSet> のフィールド宣言に適用します。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreDataExcelCS/Sheet1.cs" id="Snippet11":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreDataExcelVB/Sheet1.vb" id="Snippet11":::

3. データ項目のインスタンスを作成して必要に応じてデータベースから読み込むコードを追加します。

     データ項目は、最初に作成されたときにのみ読み込まれます。その後、キャッシュはドキュメントと共に保持されます。更新するには、他のコードを記述する必要があります。

### <a name="to-cache-a-dataset-in-the-document-by-using-the-properties-window"></a>プロパティ ウィンドウを使用してドキュメントにデータセットをキャッシュするには

1. Visual Studio デザイナーのツールを使用して、データセットをプロジェクトに追加します。たとえば、 **[データ ソース]** ウィンドウを使用してプロジェクトにデータ ソースを追加します。

2. データセットのインスタンスをまだ作成していない場合は作成し、デザイナーでインスタンスを選択します。

3. **[プロパティ]** ウィンドウで、**CacheInDocument** プロパティを **True** に設定します。

     詳細については、「[Office プロジェクトのプロパティ](../vsto/properties-in-office-projects.md)」を参照してください。

4. **[プロパティ]** ウィンドウで、**Modifiers** プロパティを **Public** に設定します (既定では **Internal** です)。

## <a name="see-also"></a>関連項目
- [キャッシュ データ](../vsto/caching-data.md)
- [方法: データ ソースをプログラムによって Office ドキュメント内にキャッシュする](../vsto/how-to-programmatically-cache-a-data-source-in-an-office-document.md)
- [方法: パスワードで保護されたドキュメントにデータをキャッシュする](../vsto/how-to-cache-data-in-a-password-protected-document.md)
- [サーバー上のドキュメント内のデータにアクセスする](../vsto/accessing-data-in-documents-on-the-server.md)
- [データを保存する](../data-tools/save-data-back-to-the-database.md)
