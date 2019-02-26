---
title: 信頼のリストを使用して Office ソリューションを信頼
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- permissions [Office development in Visual Studio]
- inclusion lists [Office development in Visual Studio], about inclusion lists
- security [Office development in Visual Studio], inclusion lists
- inclusion lists [Office development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 34b4ed5dbc0996239e73db38f1d6bea9e43d6de4
ms.sourcegitcommit: d0425b6b7d4b99e17ca6ac0671282bc718f80910
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/21/2019
ms.locfileid: "56640598"
---
# <a name="trust-office-solutions-by-using-inclusion-lists"></a>信頼のリストを使用して Office ソリューションを信頼
  信頼のリストによって、ユーザーは発行者を識別する証明書で署名されている Office ソリューションに信頼を付与することができます。 信頼のリストはユーザー固有であり、ドキュメント レベルのカスタマイズと VSTO アドインに使用できます。

 [!INCLUDE[appliesto_all](../vsto/includes/appliesto-all-md.md)]

 ユーザーが信頼を付与されていない Office ソリューションを起動するとき、Microsoft Office ソリューションでは、 [!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)] 信頼プロンプトでその人にセキュリティ上の決定を求めます。 ユーザーがソリューションを信頼すると決定した場合、カスタマイズが実行され、次回からはプロンプトは出されません。

## <a name="inclusion-list-and-windows-installer"></a>信頼のリストと Windows インストーラー
 Office ソリューションのインストール、 *Program Files* Windows インストーラーを使用してディレクトリには、管理者権限が必要です。 Office ソリューションの*Program Files*ディレクトリに、Visual Studio Tools for Office ランタイムは、Office ソリューションが FullTrust アクセス許可を付与されて既にがあるため、不要になった信頼のリストをチェックします。

## <a name="clickonce-trust-prompt"></a>ClickOnce 信頼プロンプト
 Office ソリューションに [!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)] の実装を使用すると、管理者は、プロンプトを許可するか、プロンプトを無効にするか、または信頼された証明書を要求するように、信頼プロンプト レベルを構成することができます。 この構成を行うには、信頼のリストへのアクセスを制御するレジストリ キーを使用します。

 プロンプトを無効にすると、既知の信頼される証明書を持つソリューションのみをインストールすることができます。 プロンプト レベルのAuthenticode が必須に設定されている場合、ソリューションは既知の機関から証明書で署名を得る必要がありますが、信頼されたルート機関 (信頼された証明書) にチェーンする証明書は必要ありません。 プロンプトが許可されている場合、ソリューションは、ID が不明な証明書で署名することが可能になります。 このシナリオでは、信頼性に関する判断はエンド ユーザーまで持ち越されており、ソリューションのインストールには一時的な証明書で十分です。

 詳細については、「[方法 :信頼のリストのセキュリティを構成する](../vsto/how-to-configure-inclusion-list-security.md)と表 2、プロンプト レベル レジストリ キー値起動時の効果、という[構成 ClickOnce 信頼された発行者](http://go.microsoft.com/fwlink/?LinkId=94774)します。

## <a name="structure-of-the-inclusion-list"></a>信頼のリストの構造
 有効な信頼のリストのエントリには、配置マニフェストへのパスと、ソリューションの署名に使用する公開キーという 2 つの部分があります。 ソリューションが信頼のリストに追加されると、信頼されているとみなされます。 Office ソリューションが実行されると、Office アプリケーションによって信頼リストのパブリックキーが配置マニフェストの署名キーと比較され、現在実行中のソリューションが元の信頼バージョンと同じであることが確認されます。

## <a name="see-also"></a>関連項目
- [Office ソリューションに信頼を付与](../vsto/granting-trust-to-office-solutions.md)
- [セキュリティで保護された Office ソリューション](../vsto/securing-office-solutions.md)
