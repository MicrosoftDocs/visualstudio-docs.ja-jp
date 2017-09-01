---
title: 'Walkthrough: Creating a Master Detail Relation Using a Cached Dataset | Microsoft Docs'
ms.custom: 
ms.date: 02/02/2017
ms.prod: visual-studio-dev14
ms.reviewer: 
ms.suite: 
ms.technology:
- office-development
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- master-detail tables [Office development in Visual Studio], walkthroughs
- data caching [Office development in Visual Studio], Master/Detail Relation
ms.assetid: 419f4e07-c67f-4fc9-973a-bc794f349ac3
caps.latest.revision: 41
author: kempb
ms.author: kempb
manager: ghogen
ms.translationtype: HT
ms.sourcegitcommit: eb5c9550fd29b0e98bf63a7240737da4f13f3249
ms.openlocfilehash: fb02770a5cb607cc13a5db2be2cc7128a699d569
ms.contentlocale: ja-jp
ms.lasthandoff: 08/30/2017

---
# <a name="walkthrough-creating-a-master-detail-relation-using-a-cached-dataset"></a>Walkthrough: Creating a Master Detail Relation Using a Cached Dataset
  This walkthrough demonstrates creating a master/detail relation on a worksheet, and caching the data so that the solution can be used offline.  
  
 [!INCLUDE[appliesto_xlalldoc](../vsto/includes/appliesto-xlalldoc-md.md)]  
  
 During this walkthrough, you will learn how to:  
  
-   Add controls to a worksheet.  
  
-   Set up a dataset to be cached in a worksheet.  
  
-   Add code to enable scrolling through the records.  
  
-   Test your project.  
  
> [!NOTE]  
>  Your computer might show different names or locations for some of the Visual Studio user interface elements in the following instructions. The Visual Studio edition that you have and the settings that you use determine these elements. For more information, see [Personalize the Visual Studio IDE](../ide/personalizing-the-visual-studio-ide.md).  
  
## <a name="prerequisites"></a>Prerequisites  
 You need the following components to complete this walkthrough:  
  
-   [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]  
  
-   [!INCLUDE[Excel_15_short](../vsto/includes/excel-15-short-md.md)] or [!INCLUDE[Excel_14_short](../vsto/includes/excel-14-short-md.md)].  
  
-   Access to the Northwind SQL Server sample database. The database can be on your development computer or on a server.  
  
-   Permissions to read from and write to the SQL Server database.  
  
## <a name="creating-a-new-project"></a>Creating a New Project  
 In this step, you will create an Excel Workbook project.  
  
#### <a name="to-create-a-new-project"></a>To create a new project  
  
1.  Create an Excel Workbook project with the name **My Master-Detail**, using either Visual Basic or C#. Make sure that **Create a new document** is selected. For more information, see [How to: Create Office Projects in Visual Studio](../vsto/how-to-create-office-projects-in-visual-studio.md).  
  
 Visual Studio opens the new Excel workbook in the designer and adds the **My Master-Detail** project to **Solution Explorer**.  
  
## <a name="creating-the-data-source"></a>Creating the Data Source  
 Use the **Data Sources** window to add a typed dataset to your project.  
  
#### <a name="to-create-the-data-source"></a>To create the data source  
  
1.  If the **Data Sources** window is not visible, display it by, on the menu bar, choosing **View**, **Other Windows**, **Data Sources**.  
  
2.  Choose **Add New Data Source** to start the **Data Source Configuration Wizard**.  
  
3.  Select **Database** and then click **Next**.  
  
4.  Select a data connection to the Northwind sample SQL Server database, or add a new connection by using the **New Connection** button.  
  
5.  After selecting or creating a connection, click **Next**.  
  
6.  Clear the option to save the connection if it is selected, and then click **Next**.  
  
7.  Expand the **Tables** node in the **Database objects** window.  
  
8.  Select the **Orders** table and the **Order Details** table.  
  
9. Click **Finish**.  
  
 The wizard adds the two tables to the **Data Sources** window. It also adds a typed dataset to your project that is visible in **Solution Explorer**.  
  
## <a name="adding-controls-to-the-worksheet"></a>Adding Controls to the Worksheet  
 In this step, you will add a named range, a list object, and two buttons to the first worksheet. First, add the named range and the list object from the **Data Sources** window so that they are automatically bound to the data source. Next, add the buttons from the **Toolbox**.  
  
#### <a name="to-add-a-named-range-and-a-list-object"></a>To add a named range and a list object  
  
1.  Verify that the **My Master-Detail.xlsx** workbook is open in the Visual Studio designer, with **Sheet1** displayed.  
  
2.  Open the **Data Sources** window and expand the **Orders** node.  
  
3.  Select the **OrderID** column, and then click the drop-down arrow that appears.  
  
4.  Click **NamedRange** in the drop-down list, and then drag the **OrderID** column to cell **A2**.  
  
     A <xref:Microsoft.Office.Tools.Excel.NamedRange> control named `OrderIDNamedRange` is created in cell **A2**. At the same time, a <xref:System.Windows.Forms.BindingSource> named `OrdersBindingSource`, a table adapter, and a <xref:System.Data.DataSet> instance are added to the project. The control is bound to the <xref:System.Windows.Forms.BindingSource>, which in turn is bound to the <xref:System.Data.DataSet> instance.  
  
5.  Scroll down past the columns that are under the **Orders** table. At the bottom of the list is the **Order Details** table; it is here because it is a child of the **Orders** table. Select this **Order Details** table, not the one that is at the same level as the **Orders** table, and then click the drop-down arrow that appears.  
  
6.  Click **ListObject** in the drop-down list, and then drag the **OrderDetails** table to cell **A6**.  
  
7.  A <xref:Microsoft.Office.Tools.Excel.ListObject> control named **Order_DetailsListObject** is created in cell **A6**, and bound to the <xref:System.Windows.Forms.BindingSource>.  
  
#### <a name="to-add-two-buttons"></a>To add two buttons  
  
1.  From the **Common Controls** tab of the **Toolbox**, add a <xref:System.Windows.Forms.Button> control to cell **A3** of the worksheet.  
  
     This button is named `Button1`.  
  
2.  Add another <xref:System.Windows.Forms.Button> control to cell **B3** of the worksheet.  
  
     This button is named `Button2`.  
  
 Next, mark the dataset to be cached in the document.  
  
## <a name="caching-the-dataset"></a>Caching the Dataset  
 Mark the dataset to be cached in the document by making the dataset public and setting the **CacheInDocument** property.  
  
#### <a name="to-cache-the-dataset"></a>To cache the dataset  
  
1.  Select **NorthwindDataSet** in the component tray.  
  
2.  In the **Properties** window, change the **Modifiers** property to **Public**.  
  
     Datasets must be public before caching is enabled.  
  
3.  Change the **CacheInDocument** property to **True**.  
  
 The next step is to add text to the buttons, and in C# add code to hook up the event handlers.  
  
## <a name="initializing-the-controls"></a>Initializing the Controls  
 Set the button text and add event handlers during the <xref:Microsoft.Office.Tools.Excel.Workbook.Startup> event.  
  
#### <a name="to-initialize-the-data-and-the-controls"></a>To initialize the data and the controls  
  
1.  In **Solution Explorer**, right-click **Sheet1.vb** or **Sheet1.cs**, and then click **View Code** on the shortcut menu.  
  
2.  Add the following code to the `Sheet1_Startup` method to set the text for the buttons.  
  
     [!code-vb[Trin_VstcoreDataExcel#15](../vsto/codesnippet/VisualBasic/Trin_VstcoreDataExcelVB/Sheet2.vb#15)]  [!code-csharp[Trin_VstcoreDataExcel#15](../vsto/codesnippet/CSharp/Trin_VstcoreDataExcelCS/Sheet2.cs#15)]  
  
3.  For C# only, add event handlers for the button click events to the `Sheet1_Startup` method.  
  
     [!code-csharp[Trin_VstcoreDataExcel#16](../vsto/codesnippet/CSharp/Trin_VstcoreDataExcelCS/Sheet2.cs#16)]  
  
## <a name="adding-code-to-enable-scrolling-through-the-records"></a>Adding Code to Enable Scrolling Through the Records  
 Add code to the <xref:System.Windows.Forms.Control.Click> event handler of each button to move through the records.  
  
#### <a name="to-scroll-through-the-records"></a>To scroll through the records  
  
1.  Add an event handler for the <xref:System.Windows.Forms.Control.Click> event of `Button1`, and add the following code to move backwards through the records:  
  
     [!code-vb[Trin_VstcoreDataExcel#17](../vsto/codesnippet/VisualBasic/Trin_VstcoreDataExcelVB/Sheet2.vb#17)]  [!code-csharp[Trin_VstcoreDataExcel#17](../vsto/codesnippet/CSharp/Trin_VstcoreDataExcelCS/Sheet2.cs#17)]  
  
2.  Add an event handler for the <xref:System.Windows.Forms.Control.Click> event of `Button2`, and add the following code to advance through the records:  
  
     [!code-vb[Trin_VstcoreDataExcel#18](../vsto/codesnippet/VisualBasic/Trin_VstcoreDataExcelVB/Sheet2.vb#18)]  [!code-csharp[Trin_VstcoreDataExcel#18](../vsto/codesnippet/CSharp/Trin_VstcoreDataExcelCS/Sheet2.cs#18)]  
  
## <a name="testing-the-application"></a>Testing the Application  
 Now you can test your workbook to make sure that the data appears as expected, and that you can use the solution offline.  
  
#### <a name="to-test-the-data-caching"></a>To test the data caching  
  
1.  Press **F5**.  
  
2.  Verify that the named range and the list object are filled with data from the data source.  
  
3.  Scroll through some of the records by clicking the buttons.  
  
4.  Save the workbook, and then close the workbook and Visual Studio.  
  
5.  Disable the connection to the database. Unplug the network cable from your computer if the database is located on a server, or stop the SQL Server service if the database is on your development computer.  
  
6.  Open Excel, and then open **My Master-Detail.xlsx** from the \bin directory (\My Master-Detail\bin in Visual Basic or \My Master-Detail\bin\debug in C#).  
  
7.  Scroll through some of the records to see that the worksheet operates normally when disconnected.  
  
8.  Reconnect to the database. Connect your computer to the network again if the database is located on a server, or start the SQL Server service if the database is on your development computer.  
  
## <a name="next-steps"></a>Next Steps  
 This walkthrough shows the basics of creating a master/detail data relationship on a worksheet and caching a dataset. Here are some tasks that might come next:  
  
-   Deploy the solution. For more information, see [Deploying an Office Solution](../vsto/deploying-an-office-solution.md)  
  
## <a name="see-also"></a>See Also  
 [Binding Data to Controls in Office Solutions](../vsto/binding-data-to-controls-in-office-solutions.md)   
 [Data in Office Solutions](../vsto/data-in-office-solutions.md)   
 [Caching Data](../vsto/caching-data.md)   
 [Host Items and Host Controls Overview](../vsto/host-items-and-host-controls-overview.md)  
  
  
