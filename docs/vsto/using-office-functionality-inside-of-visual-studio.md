---
title: Visual Studio 内での Office 機能の使用
description: ドキュメントレベルのプロジェクトからのドキュメントと関連付けられているアプリケーションが、Visual Studio 内でどのようにホストされて、ドキュメントを直接デザインして操作できるかを説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- security [Office development in Visual Studio], document protection
- Office applications [Office development in Visual Studio]
- Office functionality inside Visual Studio
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 258ea4529a558c91eb115b82b35def4ca4ab6561
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99838244"
---
# <a name="use-office-functionality-inside-of-visual-studio"></a>Visual Studio 内での Office 機能の使用
  ドキュメントレベルのプロジェクトを作成するとき、ドキュメントと関連付けられているアプリケーションは Visual Studio 内でホストされるため、ドキュメントを直接デザインして操作できます。 Visual Studio で開いた場合、Microsoft Office アプリケーションは通常、想定どおりに動作します。 ただし、アプリケーションの機能の中には、異なるものやアクセスできないものがあります。

 [!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]

## <a name="document-protection"></a>ドキュメント保護
 Microsoft Office Word および Microsoft Office Excel では、プロジェクトで使用できるドキュメント保護機能が用意されています。 ただし、ドキュメントが Visual Studio で開かれている間にドキュメント保護が有効になっていると、デザインを変更できない場合があります。 詳細については、「[ドキュメント レベルのソリューションにおけるドキュメントの保護](../vsto/document-protection-in-document-level-solutions.md)」を参照してください。

## <a name="information-rights-management"></a>Information Rights Management
 Information Rights Management (IRM) を、Microsoft Office Word と Microsoft Office Excel で使用できます。 IRM を使用すると、承認されていないユーザーが機密情報を表示したり、変更したりできないようにすることができます。 ただし、IRM では、コードが実行されないようにすることもできます。 詳細については、「[Information Rights Management とマネージド コード拡張機能の概要](../vsto/information-rights-management-and-managed-code-extensions-overview.md)」を参照してください。

## <a name="password-protection"></a>パスワード保護
 Microsoft Office Word 文書や Microsoft Office Excel ブックを、パスワードを知らない人が開けないように設定できます。 パスワード保護は Word と Excel では異なる方法で処理されるため、開発プロセスに影響を与える可能性があります。 詳細については、「[Office ドキュメントのパスワード保護](../vsto/password-protection-on-office-documents.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [ドキュメント レベルのソリューションにおけるドキュメントの保護](../vsto/document-protection-in-document-level-solutions.md)
- [Information Rights Management とマネージド コード拡張機能の概要](../vsto/information-rights-management-and-managed-code-extensions-overview.md)
- [Office ドキュメントのパスワード保護](../vsto/password-protection-on-office-documents.md)
- [方法: コードを実行せずに Office ソリューションを開く](../vsto/how-to-open-office-solutions-without-running-code.md)
