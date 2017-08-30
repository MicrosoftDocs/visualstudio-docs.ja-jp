---
title: Save data in a transaction | Microsoft Docs
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- System.Transactions namespace
- data [Visual Studio], saving in a transaction
- transactions, saving data
- Transactions namespace
- saving data
ms.assetid: 80260118-08bc-4b37-bfe5-9422ee7a1e4e
caps.latest.revision: 15
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
ms.openlocfilehash: 83cfcdc179e88ed40266983266f320f18266a12b
ms.contentlocale: ja-jp
ms.lasthandoff: 08/30/2017

---
# <a name="save-data-in-a-transaction"></a>Save data in a transaction
This walkthrough demonstrates how to save data in a transaction by using the <xref:System.Transactions> namespace. This example uses the `Customers` and `Orders` tables from the Northwind sample database.  
  
## <a name="prerequisites"></a>Prerequisites  
 This walkthrough requires access to the Northwind sample database. For information about setting up the Northwind sample database, see [How to: Install Sample Databases](../data-tools/installing-database-systems-tools-and-samples.md).  
  
## <a name="create-a-windows-application"></a>Create a Windows application  
 The first step is to create a **Windows Application**.  
  
#### <a name="to-create-the-new-windows-project"></a>To create the new Windows project  
  
1.  In Visual Studio, on the **File** menu, create a new **Project**.  
  
2.  Name the project **SavingDataInATransactionWalkthrough**.  
  
3.  Select **Windows Application**, and then select **OK**. For more information, see [Client Applications](/dotnet/framework/develop-client-apps).  
  
     The **SavingDataInATransactionWalkthrough** project is created and added to **Solution Explorer**.  
  
## <a name="create-a-database-data-source"></a>Create a database data source  
 This step uses the [Data Source Configuration Wizard](../data-tools/media/data-source-configuration-wizard.png) to create a data source based on the `Customers` and `Orders` tables in the Northwind sample database.  
  
#### <a name="to-create-the-data-source"></a>To create the data source  
  
1.  On the **Data** menu, select**Show Data Sources**.  
  
2.  In the **Data Sources** window, select **Add New Data Source** to start the **Data Source Configuration Wizard**.  
  
3.  On the **Choose a Data Source Type**screen, select **Database**, and then select **Next**.  
  
4.  On the **Choose your Data Connection** screen do one of the following:  
  
    -   If a data connection to the Northwind sample database is available in the drop-down list, select it.  
  
         -or-  
  
    -   Select **New Connection** to launch the **Add/Modify Connection** dialog box and create a connection to the Northwind database.  
  
5.  If your database requires a password, select the option to include sensitive data, and then select **Next**.  
  
6.  On the **Save connection string to the Application Configuration file** screen, select **Next**.  
  
7.  On the **Choose your Database Objects** screen, expand the **Tables** node.  
  
8.  Select the `Customers` and `Orders` tables, and then select **Finish**.  
  
     The **NorthwindDataSet** is added to your project and the `Customers` and `Orders` tables appear in the **Data Sources** window.  
  
## <a name="addcontrols-to-the-form"></a>Addcontrols to the form  
 You can create the data-bound controls by dragging items from the **Data Sources** window onto your form.  
  
#### <a name="to-create-data-bound-controls-on-the-windows-form"></a>To create data bound controls on the Windows form  
  
-   In the **Data Sources** window, expand the **Customers** node.  
  
-   Drag the main **Customers** node from the **Data Sources** window onto **Form1**.  
  
     A <xref:System.Windows.Forms.DataGridView> control and a tool strip (<xref:System.Windows.Forms.BindingNavigator>) for navigating records appear on the form. A [NorthwindDataSet](../data-tools/dataset-tools-in-visual-studio.md), `CustomersTableAdapter`, <xref:System.Windows.Forms.BindingSource>, and <xref:System.Windows.Forms.BindingNavigator> appear in the component tray.  
  
-   Drag the related **Orders** node (not the main **Orders** node, but the related child-table node below the **Fax** column) onto the form below the **CustomersDataGridView**.  
  
     A <xref:System.Windows.Forms.DataGridView> appears on the form. An `OrdersTableAdapter` and <xref:System.Windows.Forms.BindingSource> appear in the component tray.  
  
## <a name="add-a-reference-to-the-systemtransactions-assembly"></a>Add a reference to the System.Transactions assembly  
 Transactions use the <xref:System.Transactions> namespace. A project reference to the system.transactions assembly is not added by default, so you need to manually add it.  
  
#### <a name="to-add-a-reference-to-the-systemtransactions-dll-file"></a>To add a reference to the System.Transactions DLL file  
  
1.  On the **Project** menu, select **Add Reference**.  
  
2.  Select **System.Transactions** (on the **.NET** tab), and then select **OK**.  
  
     A reference to **System.Transactions** is added to the project.  
  
## <a name="modifythe-code-in-the-bindingnavigators-saveitem-button"></a>Modifythe code in the BindingNavigator's SaveItem button  
 For the first table dropped onto your form, code is added by default to the `click` event of the save button on the <xref:System.Windows.Forms.BindingNavigator>. You need to manually add code to update any additional tables. For this walkthrough, we refactor the existing save code out of the save button's click event handler.We also create a few more methods to provide specific update functionality based on whether the row needs to be added or deleted.  
  
#### <a name="to-modify-the-auto-generated-save-code"></a>To modify the auto-generated save code  
  
1.  Select the **Save** button on the **CustomersBindingNavigator** (the button with the floppy disk icon).  
  
2.  Replace the `CustomersBindingNavigatorSaveItem_Click` method with the following code:  
  
     [!code-vb[VbRaddataSaving#4](../data-tools/codesnippet/VisualBasic/save-data-in-a-transaction_1.vb)]  [!code-cs[VbRaddataSaving#4](../data-tools/codesnippet/CSharp/save-data-in-a-transaction_1.cs)]  
  
 The order for reconciling changes to related data is as follows:  
  
-   Delete child records. (In this case, delete records from the `Orders` table.)  
  
-   Delete parent records. (In this case, delete records from the `Customers` table.)  
  
-   Insert parent records.(In this case, insert records in the `Customers` table.)  
  
-   Insert child records. (In this case, insert records in the `Orders` table.)  
  
#### <a name="to-delete-existing-orders"></a>To delete existing orders  
  
-   Add the following `DeleteOrders` method to **Form1**:  
  
     [!code-vb[VbRaddataSaving#5](../data-tools/codesnippet/VisualBasic/save-data-in-a-transaction_2.vb)]  [!code-cs[VbRaddataSaving#5](../data-tools/codesnippet/CSharp/save-data-in-a-transaction_2.cs)]  
  
#### <a name="to-delete-existing-customers"></a>To delete existing customers  
  
-   Add the following `DeleteCustomers` method to **Form1**:  
  
     [!code-vb[VbRaddataSaving#6](../data-tools/codesnippet/VisualBasic/save-data-in-a-transaction_3.vb)]  [!code-cs[VbRaddataSaving#6](../data-tools/codesnippet/CSharp/save-data-in-a-transaction_3.cs)]  
  
#### <a name="to-add-new-customers"></a>To add new customers  
  
-   Add the following `AddNewCustomers` method to **Form1**:  
  
     [!code-vb[VbRaddataSaving#7](../data-tools/codesnippet/VisualBasic/save-data-in-a-transaction_4.vb)]  [!code-cs[VbRaddataSaving#7](../data-tools/codesnippet/CSharp/save-data-in-a-transaction_4.cs)]  
  
#### <a name="to-add-new-orders"></a>To add new orders  
  
-   Add the following `AddNewOrders` method to **Form1**:  
  
     [!code-vb[VbRaddataSaving#8](../data-tools/codesnippet/VisualBasic/save-data-in-a-transaction_5.vb)]  [!code-cs[VbRaddataSaving#8](../data-tools/codesnippet/CSharp/save-data-in-a-transaction_5.cs)]  
  
## <a name="run-the-application"></a>Run the application  
  
#### <a name="to-run-the-application"></a>To run the application  
  
-   Select **F5** to run the application.  
  
## <a name="see-also"></a>See Also  
 [Save data back to the database](../data-tools/save-data-back-to-the-database.md)
