---
title: Office ソリューションのセキュリティのトラブルシューティング
description: Microsoft Office ソリューションをセキュリティで保護する際に発生する可能性のある一般的な問題を解決するためのヒントについて説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: troubleshooting
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- security [Office development in Visual Studio], troubleshooting
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 04b68a8207dad1edf83462a8284a69c73c668006
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99969205"
---
# <a name="troubleshoot-office-solution-security"></a>Office ソリューションのセキュリティのトラブルシューティング
  このトピックでは、Office ソリューションをセキュリティで保護する際に発生する可能性のある一般的な問題を解決するためのヒントについて説明します。

 [!INCLUDE[appliesto_all](../vsto/includes/appliesto-all-md.md)]

## <a name="trusted-solutions-cannot-be-installed-from-restricted-sites"></a>信頼できるソリューションを制限付きサイトからインストールできない
 Web サイトが Internet Explorer の制限付きサイト ゾーンに一覧表示されている場合、ユーザーは Web サイトからソリューションをインストールできません。 これは、ソリューションが信頼された証明書で署名されている場合でも当てはまります。

 配置マニフェストの URL は、次の 5 つのゾーンのいずれかに分類できます。

- [マイ コンピューター]

- インターネット

- ローカル イントラネット

- 信頼済みサイト

- 制限付きサイト

  配置マニフェストの場所が制限付きサイト ゾーンに割り当てられている場合、[!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] ではソリューションはインストールされません。 場所が既知で信頼できる場合、ユーザーは、制限付きサイト ゾーンから場所を削除して、ソリューションをインストールすることができます。 ゾーンの管理方法の詳細については、[ClickOnce 信頼された発行元の構成](/previous-versions/dotnet/articles/ms996418(v=msdn.10))に関するページを参照してください。

## <a name="solutions-cannot-be-installed-from-network-file-shares-or-web-locations-when-internet-explorer-enhanced-security-configuration-or-internet-explorer-7-is-installed"></a>Internet Explorer セキュリティ強化の構成または Internet Explorer 7 がインストールされている場合、ネットワーク ファイル共有または Web の場所からソリューションをインストールできない
 Windows Server 2003 以降の internet Explorer セキュリティ強化の構成 (IEESC)、および Internet Explorer 7 以降では、ユーザーがインターネットをブラウズする機能が大幅に制限されています。 ユーザーがネットワーク ファイル共有または Web の場所から Office ソリューションをインストールしようとすると、次のエラー メッセージが表示されることがあります。「"*SolutionName*" の配置マニフェストに署名するために使用される証明書が信頼されていないため、このアプリケーションのカスタマイズされた機能は正常に機能しません。 詳細については、管理者にお問い合わせください。」

 IEESC と Internet Explorer 7 以降では、配置マニフェストの URL がインターネット ゾーンに分類されている場合、マニフェストに信頼された発行元の証明書が含まれている必要があります。そうでない場合は、ソリューションをインストールできません。 IEESC を使用しない場合、既定の動作では、エンド ユーザーに対して信頼の決定を行うよう求めるメッセージが表示されます。

 IEESC と Internet Explorer 7 以降の影響を管理するには、信頼できる Web サイトと汎用名前付け規則 (UNC) パスを特定し、それらを信頼できるセキュリティ ゾーン (ローカル イントラネットまたは信頼済みサイト) のいずれかに追加します。ゾーンの管理方法の詳細については、[ClickOnce 信頼された発行元の構成](/previous-versions/dotnet/articles/ms996418(v=msdn.10))に関するページを参照してください。

## <a name="see-also"></a>関連項目
- [Office ソリューションをセキュリティで保護する](../vsto/securing-office-solutions.md)
- [Visual Studio トラブルシューティング](/troubleshoot/visualstudio/welcome-visual-studio/)
