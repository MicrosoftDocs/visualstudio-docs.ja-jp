---
title: Create a Windows Form to search data | Microsoft Docs
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Windows Forms, searching data
- Windows Forms, displaying data
- parameters, displaying filtered data
- data [Visual Studio], parameterizing queries
- data [Visual Studio], searching
ms.assetid: 65ca79a9-7458-466c-af55-978cd24c549e
caps.latest.revision: 28
author: mikeblome
ms.author: mblome
manager: ghogen
translation.priority.ht:
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- ru-ru
- zh-cn
- zh-tw
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
ms.translationtype: HT
ms.sourcegitcommit: 21a413a3e2d17d77fd83d5109587a96f323a0511
ms.openlocfilehash: 6834e4d65b869c680e1a959c1667486e5b19ed34
ms.contentlocale: ja-jp
ms.lasthandoff: 08/30/2017

---
# <a name="create-a-windows-form-to-search-data"></a>Create a Windows Form to search data
A common application scenario is to display selected data on a form. For example, you might want to display the orders for a specific customer or the details of a specific order. In this scenario, a user enters information into a form, and then a query is executed with the user's input as a parameter; that is, the data is selected based on a parameterized query. The query returns only the data that satisfies the criteria entered by the user. This walkthrough shows how to create a query that returns customers in a specific city, and modify the user interface so that users can enter a city's name and press a button to execute the query.  
  
 Using parameterized queries helps make your application efficient by letting the database do the work it is best at — quickly filtering records. In contrast, if you request an entire database table, transfer it over the network, and then use application logic to find the records you want, your application can become slow and inefficient.  
  
 You can add parameterized queries to any TableAdapter (and controls to accept parameter values and execute the query), using the **Search Criteria Builder** dialog box. Open the dialog box by selecting the **Add Query** command on the **Data** menu (or on any TableAdapter smart tag).  
  
 Tasks illustrated in this walkthrough include:  
  
-   Creating a new Windows Forms Application project.  
  
-   Creating and configuring the data source in your application with the **Data Source Configuration** wizard.  
  
-   Setting the drop type of the items in the **Data Sources**window.  
  
-   Creating controls that display data by dragging items from the **Data Sources** window onto a form.  
  
-   Adding controls to display the data on the form.  
  
-   Completing the **Search Criteria Builder** dialog box.  
  
-   Entering parameters into the form and executing the parameterized query.  
  
## <a name="prerequisites"></a>Prerequisites  
 In order to complete this walkthrough, you need:  
  
-   Access to the Northwind sample database.  
  
## <a name="create-the-windows-application"></a>Create the Windows Application  
 The first step is to create a **Windows Application**. Assigning a name to the project is optional at this step, but you'll give it a name here because you'll save it later.  
  
#### <a name="to-create-the-new-windows-application-project"></a>To create the new Windows Application project  
  
1.  From the **File** menu, create a new project.  
  
2.  Name the project `WindowsSearchForm`.  
  
3.  Select **Windows Application** and click **OK**.  
  
     The **WindowsSearchForm** project is created and added to **Solution Explorer**.  
  
## <a name="create-the-data-source"></a>Create the data source  
 This step creates a data source from a database using the **Data Source Configuration** wizard. You must have access to the Northwind sample database to create the connection. For information on setting up the Northwind sample database, see [Install SQL Server sample databases](../data-tools/install-sql-server-sample-databases.md).  
  
#### <a name="to-create-the-data-source"></a>To create the data source  
  
1.  On the **Data** menu, click **Show Data Sources**.  
  
2.  In the **Data Sources** window, select **Add New Data Source** to start the **Data Source Configuration** wizard.  
  
3.  Select **Database** on the **Choose a Data Source Type** page, and then click **Next**.  
  
4.  On the **Choose your Data Connection** page do one of the following:  
  
    -   If a data connection to the Northwind sample database is available in the drop-down list, select it.  
  
    -   Select **New Connection** to launch the **Add/Modify Connection** dialog box.  
  
5.  If your database requires a password, select the option to include sensitive data, and then click **Next**.  
  
6.  On the **Save connection string to the Application Configuration file** page, click **Next**.  
  
7.  On the **Choose your Database Objects** page, expand the **Tables** node.  
  
8.  Select the **Customers** table, and then click **Finish**.  
  
     The **NorthwindDataSet** is added to your project, and the **Customers** table appears in the **Data Sources** window.  
  
## <a name="create-the-form"></a>Create the form  
 You can create the data-bound controls by dragging items from the **Data Sources** window onto your form.  
  
#### <a name="to-create-data-bound-controls-on-the-form"></a>To create data-bound controls on the form  
  
1.  Expand the **Customers** node in the **Data Sources** window.  
  
2.  Drag the **Customers** node from the **Data Sources** window to your form.  
  
     A <xref:System.Windows.Forms.DataGridView> and a tool strip (<xref:System.Windows.Forms.BindingNavigator>) for navigating records appear on the form. A [NorthwindDataSet](../data-tools/dataset-tools-in-visual-studio.md), CustomersTableAdapter, <xref:System.Windows.Forms.BindingSource>, and <xref:System.Windows.Forms.BindingNavigator> appear in the component tray.  
  
## <a name="add-parameterization-search-functionality-to-the-query"></a>Add parameterization (search functionality) to the query  
 You can add a WHERE clause to the original query using the **Search Criteria Builder** dialog box.  
  
#### <a name="to-create-a-parameterized-query-and-controls-to-enter-the-parameters"></a>To create a parameterized query and controls to enter the parameters  
  
1.  Select the <xref:System.Windows.Forms.DataGridView> control, and then choose **Add Query** on the **Data** menu.  
  
2.  Type `FillByCity` in the **New query name** area on the **Search Criteria Builder** dialog box.  
  
3.  Add `WHERE City = @City` to the query in the **Query Text** area.  
  
     The query should be similar to the following:  
  
     `SELECT CustomerID, CompanyName, ContactName, ContactTitle, Address, City, Region, PostalCode, Country, Phone, Fax`  
  
     `FROM Customers`  
  
     `WHERE City = @City`  
  
    > [!NOTE]
    >  Access and OLE DB data sources use the question mark ('?') to denote parameters, so the WHERE clause would look like this: `WHERE City = ?`.  
  
4.  Click **OK** to close the **Search Criteria Builder** dialog box.  
  
     A **FillByCityToolStrip** is added to the form.  
  
## <a name="testing-the-application"></a>Testing the application  
 Running the application opens your form ready to take the parameter as input.  
  
#### <a name="to-test-the-application"></a>To test the application  
  
1.  Press F5 to run the application.  
  
2.  Type **London** into the **City** text box, and then click **FillByCity**.  
  
     The data grid is populated with customers that meet the criteria. In this example, the data grid only displays customers that have a value of **London** in their **City** column.  
  
## <a name="next-steps"></a>Next Steps  
 Depending on your application requirements, there are several steps you may want to perform after creating a parameterized form. Some enhancements you could make to this walkthrough include:  
  
-   Adding controls that display related data. For more information, see [Relationships in Datasets](relationships-in-datasets.md).  
  
-   Editing the dataset to add or remove database objects. For more information, see [Create and configure datasets](../data-tools/create-and-configure-datasets-in-visual-studio.md).  
  
## <a name="see-also"></a>See Also  
 [Bind Windows Forms controls to data in Visual Studio](../data-tools/bind-windows-forms-controls-to-data-in-visual-studio.md)
