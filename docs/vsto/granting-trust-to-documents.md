---
title: ドキュメントに信頼を付与する
description: ドキュメント レベルのプロジェクトでは、証明書を使用したマニフェストへの署名や、信頼プロンプトのクリックなど、アプリケーション レベルのプロジェクトと同じセキュリティ要件が適用されることを説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- security [Office development in Visual Studio], trust
- inclusion lists [Office development in Visual Studio], about inclusion lists
- trust [Office development in Visual Studio], 2007 Office system
- granting trust [Office development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: e2871741d7297b6efabf53bb6f258355c41cac49
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99910260"
---
# <a name="grant-trust-to-documents"></a>ドキュメントに信頼を付与する
  ドキュメント レベルのプロジェクトでは、証明書を使用したマニフェストへの署名や、信頼プロンプトのクリックなど、アプリケーション レベルのプロジェクトと同じセキュリティ要件が適用されます。 また、ドキュメントまたはブックは、信頼できる場所として指定されたディレクトリに置く必要があります。

 [!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]

## <a name="trusted-locations"></a>信頼できる場所
 [!INCLUDE[Office_15_short](../vsto/includes/office-15-short-md.md)] のアプリケーションおよび Office 2010 には、信頼できる場所などの、ユーザーがセキュリティとプライバシー設定を構成できるセキュリティ センターがあります。 Officeソリューションでは、ローカル コンピューターは信頼できる場所と見なされます。 ただし、ディレクトリの中には、リスクが高めであるために信頼できないものもあります (システム、各ユーザー、Internet Explorer 用の一時フォルダーなど)。

 トラスト センターの詳細については、[Office 2010 のセキュリティとポリシーと設定](/previous-versions/office/office-2010/cc178946(v=office.14))に関するページを参照してください。 信頼されたフォルダーを作成、管理、削除、および構成する方法の詳細については、「[2007 Office システムで信頼できる場所と信頼された発行元の設定を構成する](/previous-versions/office/office-2007-resource-kit/cc178948(v=office.12))」および[ファイルの信頼できる場所の作成、削除、変更](https://support.office.com/article/Create-remove-or-change-a-trusted-location-for-your-files-f5151879-25ea-4998-80a5-4208b3540a62)に関するページを参照してください。

## <a name="security-considerations-for-office-solutions"></a>Office ソリューションのセキュリティに関する考慮事項
 どのフォルダーを信頼できる場所に追加するかを検討するときには、以下のセキュリティ上の問題に留意する必要があります。

- ローカル フォルダーは安全性が高いと見なされ、暗黙的に信頼されます。  ファイル共有などのリモートの場所は、信頼できる場所として指定する必要があります。

- 信頼できる場所にディレクトリを追加すると、Office ソリューションだけでなく VBA コードおよび ActiveX コードにも完全な信頼が付与されます。 そのため、ルート ディレクトリや *マイ ドキュメント* フォルダーは信頼できる場所として指定しないでください。

- ドキュメント自体は信頼できる場所を使用することによって信頼されますが、カスタマイズを信頼するためには追加のアクセス許可が必要です。 カスタマイズに完全な信頼を付与するには、証明書を使用したマニフェストへの署名、信頼プロンプトのクリック、Office ソリューションの *Program Files* ディレクトリへのインストールのいずれかを行います。

- ドキュメント レベルのソリューションのドキュメントまたはブックは、アセンブリと同じディレクトリ、または別のディレクトリに保存できます。 たとえば、ドキュメントを SharePoint サーバー上に置き、アセンブリをネットワーク ファイル共有に置くことも可能です。 詳細については、「[方法: ClickOnce を使用してドキュメント レベルの Office ソリューションを SharePoint Server に発行する](/previous-versions/bb608595(v=vs.110))」を参照してください。

## <a name="see-also"></a>関連項目
- [Office ソリューションへの信頼の付与](../vsto/granting-trust-to-office-solutions.md)
- [Office ソリューションのセキュリティのトラブルシューティング](../vsto/troubleshooting-office-solution-security.md)
- [Office ソリューションをセキュリティで保護する](../vsto/securing-office-solutions.md)