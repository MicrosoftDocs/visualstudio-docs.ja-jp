---
title: アクセス許可が制限されたドキュメントの背後でのコードの実行を許可する
description: Visual Studio の Office 開発ツールを使用して、アクセス許可が制限されたドキュメントの背後でコードを実行できるようにする方法について説明します。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: how-to
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
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 1a65e99712658567996598d2190447ff09cf9b05
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99888889"
---
# <a name="how-to-permit-code-to-run-behind-documents-with-restricted-permissions"></a>方法: アクセス許可が制限されたドキュメントの背後でのコードの実行を許可する
  Microsoft Office の Information Rights Management (IRM) 機能を使用して、ドキュメントまたはブックへのアクセス許可を制限できます。 既定では、制限された Microsoft Office Word 文書または Microsoft Office Excel ブックの背後にあるコードは実行できません。 既定値を変更して、マネージド コード拡張機能からオブジェクト モデルにアクセスできるようにすると、ソリューションが正常に機能します。

 [!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]

 アクセス許可の設定を変更できるようにするには、ドキュメントまたはブックの作成者であるか、フル コントロール アクセス権を持っている必要があります。

## <a name="to-permit-code-to-run-behind-documents-with-restricted-permissions"></a>アクセス許可が制限されたドキュメントの背後でのコードの実行を許可するには

1. Word または Excel で文書またはブックを開きます。

2. **[ファイル]** タブをクリックし、 **[準備]** 、 **[アクセスの制限]** の順にポイントしてから、 **[アクセス制限あり]** をクリックします。

   > [!NOTE]
   > 初回使用時には、Windows Rights Management クライアントをインストールするように求められます。 クライアントをインストールした後、場合によってはこれらの手順を繰り返す必要があります。

3. **[アクセス許可]** ダイアログ ボックスで、 **[このドキュメントへのアクセスを制限する]** を選択してから、 **[その他のオプション]** をクリックします。

4. **[ユーザーの追加権限]** で、 **[プログラムを使ってコンテンツにアクセスする]** を選択します。

   Word または Excel で、プログラムによるオブジェクト モデルへのアクセスが許可されます。

## <a name="see-also"></a>関連項目
- [Information Rights Management とマネージド コード拡張機能の概要](../vsto/information-rights-management-and-managed-code-extensions-overview.md)
- [ドキュメント レベルのソリューションにおけるドキュメントの保護](../vsto/document-protection-in-document-level-solutions.md)
- [Office ドキュメントのパスワード保護](../vsto/password-protection-on-office-documents.md)
- [Office ソリューションを設計して作成する](../vsto/designing-and-creating-office-solutions.md)
- [Office ソリューションをセキュリティで保護する](../vsto/securing-office-solutions.md)
- [Office ソリューションを配置する](../vsto/deploying-an-office-solution.md)
