---
title: 'Walkthrough: Creating a DataTable in the Dataset Designer | Microsoft Docs'
ms.custom: 
ms.date: 10/19/2016
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- DataTable objects, creating
- Dataset Designer, creating data tables
- tables [Visual Studio], creating
- data [Visual Studio], Dataset Designer
ms.assetid: abf0a2b5-e4e5-422e-97ef-55a0e35a82df
caps.latest.revision: 10
author: gewarren
ms.author: gewarren
manager: ghogen
robots: noindex,nofollow
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
ms.translationtype: HT
ms.sourcegitcommit: cca2a707627c36221a654cf8a06730383492f371
ms.openlocfilehash: f238249749a46879a50e315d03556756afe5983f
ms.contentlocale: ja-jp
ms.lasthandoff: 09/13/2017

---
# <a name="walkthrough-creating-a-datatable-in-the-dataset-designer"></a>Walkthrough: Creating a DataTable in the Dataset Designer
This walkthrough explains how to create a <xref:System.Data.DataTable> (without a TableAdapter) using the **Dataset Designer**. For information on creating data tables that include TableAdapters, see [Create and configure TableAdapters](../data-tools/create-and-configure-tableadapters.md).  
  
 Tasks illustrated in this walkthrough include:  
  
-   Creating a new Windows Forms Application project  
  
-   Adding a new dataset to the application  
  
-   Adding a new data table to the dataset  
  
-   Adding columns to the data table  
  
-   Setting the primary key for the table  
  
## <a name="creating-a-new-windows-forms-application"></a>Creating a New Windows Forms Application  
  
#### <a name="to-create-a-new-windows-forms-application-project"></a>To create a new Windows Forms Application project  
  
1. In Visual Studio, on the **File** menu, select **New**, **Project...**.  
  
2. Expand either **Visual C#** or **Visual Basic** in the left-hand pane, then select **Windows Classic Desktop**.  

3. In the middle pane, select the **Windows Forms App** project type.  

4. Name the project **DataTableWalkthrough**, and then choose **OK**. 
  
     The **DataTableWalkthrough** project is created, and added to **Solution Explorer**.  
  
## <a name="adding-a-new-dataset-to-the-application"></a>Adding a New Dataset to the Application  
  
#### <a name="to-add-a-new-dataset-item-to-the-project"></a>To add a new dataset item to the project  
  
1.  On the **Project** menu, click **Add New Item**.  
  
     The Add New Item Dialog Box appears.  
  
2.  In the **Templates** box, select **DataSet**.  
  
3.  Click **Add**.  
  
     Visual Studio will add a file called **DataSet1.xsd** to the project and open it in the **Dataset Designer**.  
  
## <a name="adding-a-new-datatable-to-the-dataset"></a>Adding a New DataTable to the Dataset  
  
#### <a name="to-add-a-new-data-table-to-the-dataset"></a>To add a new data table to the dataset  
  
1.  Drag a **DataTable** from the **DataSet** tab of the **Toolbox** onto the **Dataset Designer**.  
  
     A table named **DataTable1** is added to the dataset.  
   
2.  Click the title bar of **DataTable1** and rename it `Music`.  
  
## <a name="adding-columns-to-the-data-table"></a>Adding Columns to the Data Table  
  
#### <a name="to-add-columns-to-the-data-table"></a>To add columns to the data table  
  
1.  Right-click the **Music** table. Point to **Add**, and then click **Column**.  
  
2.  Name the column `SongID`.  
  
3.  In the **Properties** window, set the <xref:System.Data.DataColumn.DataType%2A> property to <xref:System.Int16?displayProperty=fullName>.  
  
4.  Repeat this process and add the following columns:  
  
     `SongTitle`: <xref:System.String?displayProperty=fullName>  
  
     `Artist`: <xref:System.String?displayProperty=fullName>  
  
     `Genre`: <xref:System.String?displayProperty=fullName>  
  
## <a name="setting-the-primary-key-for-the-table"></a>Setting the Primary Key for the Table  
All data tables should have a primary key. A primary key uniquely identifies a specific record in a data table.  
  
#### <a name="to-set-the-primary-key-of-the-data-table"></a>To set the primary key of the data table  
  
-   Right-click the **SongID** column, and then click **Set Primary Key**.  
  
     A key icon appears next to the **SongID** column.  
  
## <a name="saving-your-project"></a>Saving Your Project  
  
#### <a name="to-save-the-datatablewalkthrough-project"></a>To save the DataTableWalkthrough project  
  
-   On the **File** menu, click **Save All**.  
  
## <a name="see-also"></a>See Also  
    
 [Bind controls to data in Visual Studio](../data-tools/bind-controls-to-data-in-visual-studio.md)   
 [Validating Data](validate-data-in-datasets.md)   
 [Saving Data](../data-tools/saving-data.md)   

