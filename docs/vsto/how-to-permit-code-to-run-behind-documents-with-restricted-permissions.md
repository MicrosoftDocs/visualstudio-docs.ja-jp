---
title: '方法: 制限されたアクセス許可を持つドキュメントの背後で実行するコードを許可します。'
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Information Rights Management [Office development in Visual Studio]
- permissions [Office development in Visual Studio]
- IRM [Office development in Visual Studio]
- code [Office development in Visual Studio], running behind restricted documents
- documents [Office development in Visual Studio], restricted permissions
- Office documents [Office development in Visual Studio, restricted permissions
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: be5afe96af1baa615e5000a6c1a19b543f3c89c5
ms.sourcegitcommit: d0425b6b7d4b99e17ca6ac0671282bc718f80910
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/21/2019
ms.locfileid: "56637660"
---
# <a name="how-to-permit-code-to-run-behind-documents-with-restricted-permissions"></a>方法: 制限されたアクセス許可を持つドキュメントの背後で実行するコードを許可します。
  Microsoft Office の Information Rights Management (IRM) 機能を使用して、文書またはブックへのアクセス許可を制限することができます。 既定では、制限された Microsoft Office Word ドキュメントまたは Microsoft Office Excel ブックの背後にあるコードは実行できません。 既定値を変更するには、オブジェクト モデルにアクセスできる、マネージ コード拡張機能と、ソリューションが動作できるようにします。

 [!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]

 文書またはブックの作成者にするか、フル コントロール アクセス許可設定を変更できる必要があります。

## <a name="to-permit-code-to-run-behind-documents-with-restricted-permissions"></a>制限されたアクセス許可を持つドキュメントの背後で実行するためのコードを許可するには

1. Word または Excel でドキュメントまたはブックを開きます。

2. をクリックして、**ファイル** タブをポイントして、**準備**、 をポイント**アクセスの制限**、順にクリックします**制限されたアクセス**します。

   > [!NOTE]
   >  初めて使用する、Windows Rights Management クライアントのインストールを求められます。 クライアントをインストールした後は、手順を繰り返す必要があります。

3. **権限**ダイアログ ボックスで、**このドキュメントへのアクセスを制限する**、順にクリックします**オプションより**します。

4. **ユーザーの追加権限**を選択します**コンテンツをプログラムでアクセス**します。

   Word または Excel オブジェクト モデルにプログラムでアクセスが許可されます。

## <a name="see-also"></a>関連項目
- [Information rights management とマネージ コード拡張機能の概要](../vsto/information-rights-management-and-managed-code-extensions-overview.md)
- [ドキュメント レベルのソリューションでドキュメントの保護](../vsto/document-protection-in-document-level-solutions.md)
- [Office ドキュメントのパスワード保護](../vsto/password-protection-on-office-documents.md)
- [Office ソリューションの設計と作成](../vsto/designing-and-creating-office-solutions.md)
- [セキュリティで保護された Office ソリューション](../vsto/securing-office-solutions.md)
- [Office ソリューションのデプロイ](../vsto/deploying-an-office-solution.md)
