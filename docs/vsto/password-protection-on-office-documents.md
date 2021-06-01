---
title: Office ドキュメントのパスワード保護
description: Microsoft Word 文書や Excel ブックにパスワードを設定し、承認されていないユーザーが開くことができないようにする方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- permissions [Office development in Visual Studio]
- workbooks [Office development in Visual Studio], restricted permissions
- passwords [Office development in Visual Studio], document protections
- documents [Office development in Visual Studio], restricted permissions
- Office documents [Office development in Visual Studio, restricted permissions
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 2cc320baf310af0ec2b4cdd84fabff951b2a9cb2
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99885288"
---
# <a name="password-protection-on-office-documents"></a>Office ドキュメントのパスワード保護
  Microsoft Office Word 文書や Microsoft Office Excel ブックにパスワードを設定し、パスワードを知らないユーザーが開けないようにすることができます。 このオプションは、**開くときのパスワード** と呼ばれます。

 [!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]

 **開くときのパスワード** が有効になっている既存の文書やブックを使用して、ドキュメント レベルのプロジェクトを作成できます。 **開くときのパスワード** が有効になっている Word や Excel のドキュメントは、Visual Studio での動作が異なります。

 **開くときのパスワード** を有効にする方法については、Word または Excel のヘルプをご覧ください。

## <a name="behavior-of-excel-and-word"></a>Excel と Word の動作
 Excel ブックで **開くときのパスワード** が有効になっている場合、Visual Studio で開くたびに、パスワードを入力するように求められます。 ソリューションをビルドするときは、ビルドの間にドキュメントが開かれるため、再びパスワードの入力を求められます。

 **開くときのパスワード** が有効になっている Word 文書を Visual Studio で初めて開くと、パスワードの入力を求めるメッセージが表示されます。 パスワードを正しく入力すると、**開くときのパスワード** が文書から削除され、ドキュメントを開くときにパスワードは不要になります。 ソリューション内のドキュメントを開く前にパスワードが要求されるようにするには、最終的なビルドの後、ソリューションを配置する前に、**開くときのパスワード** を有効にする必要があります。

## <a name="see-also"></a>こちらもご覧ください
- [ドキュメント レベルのソリューションにおけるドキュメントの保護](../vsto/document-protection-in-document-level-solutions.md)
- [Information Rights Management とマネージド コード拡張の概要](../vsto/information-rights-management-and-managed-code-extensions-overview.md)
- [方法: アクセス許可が制限されたドキュメントの背後でのコードの実行を許可する](../vsto/how-to-permit-code-to-run-behind-documents-with-restricted-permissions.md)
- [Office ソリューションを設計して作成する](../vsto/designing-and-creating-office-solutions.md)
