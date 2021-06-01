---
title: Information Rights Management とマネージド コード拡張
description: 承認されていないユーザーが機密情報を表示または変更できないようにするための機能である Information Rights Management (IRM) について説明します。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Information Rights Management [Office development in Visual Studio]
- workbooks [Office development in Visual Studio], restricted permissions
- IRM [Office development in Visual Studio]
- documents [Office development in Visual Studio], restricted permissions
- rights management [Office development in Visual Studio]
- Office documents [Office development in Visual Studio, restricted permissions
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 8fc6a37a327c26ec46777575c3976c227e2d1de9
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99881491"
---
# <a name="information-rights-management-and-managed-code-extensions-overview"></a>Information Rights Management とマネージド コード拡張の概要
  Microsoft Office Word と Microsoft Office Excel には、承認されていないユーザーが機密情報を表示または変更できないようにするための機能である Information Rights Management (IRM) が用意されています。 Information Rights Management の動作のしくみの詳細については、特定の Office アプリケーションのヘルプを参照してください。

 [!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]

## <a name="run-code-behind-documents-with-restricted-permissions"></a>アクセス許可が制限されたドキュメントの背後でコードを実行する
 IRM を使用する文書またはブックがソリューションに含まれている場合、既定では、Word および Excel によりコードの実行は許可されません。 文書の作成者である場合、またはフル コントロール アクセス権を持っている場合は、ソリューションが動作するように既定値を変更できます。 詳細については、「[方法: アクセス許可が制限されたドキュメントの背後でのコードの実行を許可する](../vsto/how-to-permit-code-to-run-behind-documents-with-restricted-permissions.md)」を参照してください。

 <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument> を使用してドキュメントにキャッシュされているデータを取得または操作することは、IRM によって禁止されます。

## <a name="end-users-to-restrict-permissions-to-documents-that-use-managed-code-extensions"></a>エンド ユーザーが、マネージド コード拡張を使用するドキュメントへのアクセス許可を制限する
 ソリューション内のドキュメントまたはブックに対するフル コントロール アクセス権を持つユーザーは、IRM を使用してアクセス許可を制限できます。 たとえば、データベースのデータをワークシートに自動的に設定するソリューションを使用している会計部門のエンド ユーザーは、自分の部署のユーザーにのみ変更アクセス権を許可し、他のユーザーには読み取りアクセス権を許可することができます。 ユーザーが制限されたアクセス許可を追加すると、既定では、ワークシートの背後にあるコードは実行できず、ワークシートにデータは設定されません。

 この問題を解決するには、ドキュメントまたはブックに対するフル コントロール アクセス権を持つユーザーが、オブジェクト モデルにプログラムでアクセスできるように、既定のアクセス許可設定を変更する必要があります。 詳細については、「[方法: アクセス許可が制限されたドキュメントの背後でのコードの実行を許可する](../vsto/how-to-permit-code-to-run-behind-documents-with-restricted-permissions.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [ドキュメント レベルのソリューションにおけるドキュメントの保護](../vsto/document-protection-in-document-level-solutions.md)
- [Office ドキュメントのパスワード保護](../vsto/password-protection-on-office-documents.md)
- [Office ソリューションをセキュリティで保護する](../vsto/securing-office-solutions.md)
- [Office ソリューションを配置する](../vsto/deploying-an-office-solution.md)
- [Office ソリューションを設計して作成する](../vsto/designing-and-creating-office-solutions.md)
