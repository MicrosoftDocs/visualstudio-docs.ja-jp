---
title: Office ソリューションに信頼を付与する
description: Office ソリューションに信頼を付与するとは、ソリューション アセンブリ、配置マニフェスト、およびドキュメントを信頼するように各ターゲット コンピューターのセキュリティ ポリシーを変更することを意味します。
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
ms.openlocfilehash: f98f3154a0708ce7a01603968f0f5774dd86f40e
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99910227"
---
# <a name="grant-trust-to-office-solutions"></a>Office ソリューションに信頼を付与する
  Office ソリューションへの信頼の付与は、ソリューション アセンブリ、アプリケーション マニフェスト、配置マニフェスト、およびドキュメントを信頼するように各ターゲット コンピューターのセキュリティ ポリシーを変更することを意味します。 Office ソリューションに対する信頼は、ご自分で付与するか、エンド ユーザーが付与できます。

 アプリケーション マニフェストと配置マニフェストに署名することによって、Office ソリューションに対する完全な信頼を付与することができます。

 エンド ユーザーは、[!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)] 信頼プロンプトで信頼の決定を行うことによって、Office ソリューションに信頼を付与することができます。

 [!INCLUDE[appliesto_all](../vsto/includes/appliesto-all-md.md)]

## <a name="trust-the-solution-by-signing-the-application-and-deployment-manifests"></a><a name="Signing"></a> アプリケーション マニフェストと配置マニフェストに署名することによってソリューションを信頼する
 Office ソリューション用のすべてのアプリケーション マニフェストと配置マニフェストは、発行元を識別する証明書で署名されている必要があります。 証明書は、信頼の決定を行うための基礎となります。

 一時的な証明書が自動的に作成され、デバッグ中にソリューションが実行されるように、ビルド時に信頼が付与されます。 一時的な証明書で署名されたソリューションを発行すると、エンド ユーザーに対して信頼の決定を求めるメッセージが表示されます。

 既知の信頼された証明書を使用してソリューションに署名すると、エンド ユーザーに対して信頼の決定を求めることなく、ソリューションが自動的にインストールされます。 署名用の証明書を取得する方法の詳細については、「[ClickOnce と Authenticode](../deployment/clickonce-and-authenticode.md)」を参照してください。 証明書を取得した後は、信頼された発行元の一覧に追加することで、証明書を明示的に信頼する必要があります。 詳細については、「[方法: ClickOnce アプリケーション用の信頼された発行元をクライアント コンピューターに追加する](../deployment/how-to-add-a-trusted-publisher-to-a-client-computer-for-clickonce-applications.md)」を参照してください。

 開発者が一時的な証明書を使用してソリューションに署名する場合、管理者は、Microsoft .NET Framework ツールの 1 つであるマニフェスト生成および編集ツール (*mage.exe*) を使用して、既知の信頼された証明書でカスタマイズを再署名できます。 ソリューションの署名の詳細については、「[方法: Office ソリューションに署名する](../vsto/how-to-sign-office-solutions.md)」および「[方法: アプリケーション マニフェストと配置マニフェストに署名する](../ide/how-to-sign-application-and-deployment-manifests.md)」を参照してください。

## <a name="trust-the-solution-by-using-the-clickonce-trust-prompt"></a><a name="TrustPrompt"></a> ClickOnce 信頼プロンプトを使用してソリューションを信頼する
 ソリューションの証明書を信頼する組織全体のポリシーがない場合は、[!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)] によって信頼の決定を求めるプロンプトがエンド ユーザーに表示します。 エンド ユーザーがソリューションに信頼を付与すると、この信頼の決定を格納するための URL と公開キーを含む包含リスト エントリが作成されます。 信頼されたカスタマイズを後で実行したときに、エンド ユーザーにプロンプトが再度表示されることはありません。

 管理者は、[!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)] 信頼プロンプトを無効にしたり、Authenticode 証明書で署名されているソリューションに対してのみプロンプトが表示されるようにすることができます。 MyComputer、LocalIntranet、インターネット、TrustedSites、および UntrustedSites ゾーンのこれらの設定を変更する方法の詳細については、「[方法: ClickOnce 信頼プロンプトの動作を構成する](../deployment/how-to-configure-the-clickonce-trust-prompt-behavior.md)」を参照してください。

## <a name="see-also"></a>こちらもご覧ください

- [Office ソリューションをセキュリティで保護する](../vsto/securing-office-solutions.md)
- [ドキュメントへの信頼の付与](../vsto/granting-trust-to-documents.md)
- [Office ソリューションのセキュリティのトラブルシューティング](../vsto/troubleshooting-office-solution-security.md)
- [Office ソリューションに固有のセキュリティに関する考慮事項](../vsto/specific-security-considerations-for-office-solutions.md)