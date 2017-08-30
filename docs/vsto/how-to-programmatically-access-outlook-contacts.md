---
title: 'How to: Programmatically Access Outlook Contacts | Microsoft Docs'
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
- contacts [Office development in Visual Studio], searching
ms.assetid: ea2297ea-6802-40e4-af1a-1e511a71ec75
caps.latest.revision: 23
author: kempb
ms.author: kempb
manager: ghogen
ms.translationtype: HT
ms.sourcegitcommit: eb5c9550fd29b0e98bf63a7240737da4f13f3249
ms.openlocfilehash: 876bd379d6990e1793c178333bc2c5cd7423ad4f
ms.contentlocale: ja-jp
ms.lasthandoff: 08/30/2017

---
# <a name="how-to-programmatically-access-outlook-contacts"></a>How to: Programmatically Access Outlook Contacts
  This example finds all contacts whose last names contain a specified search string.  
  
 [!INCLUDE[appliesto_olkallapp](../vsto/includes/appliesto-olkallapp-md.md)]  
  
## <a name="example"></a>Example  
 [!code-csharp[Trin_OL_AccessContacts#1](../vsto/codesnippet/CSharp/Trin_OL_AccessContacts.trin_ol_accesscontacts/thisaddin.cs#1)] [!code-csharp[Trin_OL_AccessContacts#1](../vsto/codesnippet/CSharp/Trin_OL_AccessContacts.trin_ol_accesscontacts/thisaddin.cs#1)] [!code-vb[Trin_OL_AccessContacts#1](../vsto/codesnippet/VisualBasic/Trin_OL_AccessContacts/thisaddin.vb#1)]  
  
## <a name="compiling-the-code"></a>Compiling the Code  
 This example requires:  
  
-   Contacts whose last names contain the string "**Na"** (for example, Tzipi Butnaru) in the **Contacts** folder.  
  
## <a name="see-also"></a>See Also  
 [Working with Contact Items](../vsto/working-with-contact-items.md)   
 [How to: Programmatically Add an Entry to Outlook Contacts](../vsto/how-to-programmatically-add-an-entry-to-outlook-contacts.md)   
 [How to: Programmatically Search for a Specific Contact](../vsto/how-to-programmatically-search-for-a-specific-contact.md)   
 [How to: Programmatically Search for an E-Mail Address in Contacts](../vsto/how-to-programmatically-search-for-an-e-mail-address-in-contacts.md)   
 [How to: Programmatically Delete Outlook Contacts](../vsto/how-to-programmatically-delete-outlook-contacts.md)  
  
  
