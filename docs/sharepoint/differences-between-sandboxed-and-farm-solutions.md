---
title: サンドボックス ソリューションとファーム ソリューションの違い | Microsoft Docs
description: サンドボックス ソリューションとファーム ソリューションの違いを理解します。 どちらの種類のソリューションでも、Visual Studio がデバッグにどのように取り組むかを理解します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, sandboxed solutions
- sandboxed solutions [SharePoint development in Visual Studio]
- SharePoint development in Visual Studio, farm solutions
- farm solutions [SharePoint development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: cea66f313a8c6c8ad7fc390a3ca126d92139725c
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99948779"
---
# <a name="differences-between-sandboxed-and-farm-solutions"></a>サンドボックス ソリューションとファーム ソリューションの違い
  SharePoint ソリューションをコンパイルすると、SharePoint サーバーに配置され、デバッグするためにデバッガーがアタッチされます。 ソリューションのデバッグに使用されるプロセスは、サンドボックス ソリューションのプロパティの設定 (サンドボックス ソリューションまたはファーム ソリューション) によって異なります。

 詳細については、「[サンドボックス ソリューションに関する考慮事項](../sharepoint/sandboxed-solution-considerations.md)」を参照してください。

## <a name="farm-solutions"></a>ファーム ソリューション
 ファーム ソリューションは、IIS ワーカー プロセス (W3WP.exe) でホストされ、ファーム全体に影響を与える可能性のあるコードを実行します。 [サンドボックス ソリューション] プロパティが "ファーム ソリューション" に設定されている SharePoint プロジェクトをデバッグする場合、システムの IIS アプリケーション プールは、SharePoint が機能を取り消すか配置する前にリサイクルして、IIS ワーカー プロセスによってロックされているすべてのファイルを解放します。 SharePoint プロジェクトのサイト URL で使用されている IIS アプリケーション プールのみがリサイクルされます。

## <a name="sandboxed-solutions"></a>サンドボックス ソリューション
 サンドボックス ソリューションは、SharePoint ユーザー コード ソリューションのワーカー プロセス (SPUCWorkerProcess.exe) でホストされ、ソリューションのサイト コレクションにのみ影響を与えることができるコードを実行します。 サンドボックス ソリューションは IIS ワーカー プロセスでは実行されないため、IIS アプリケーション プールも IIS サーバーも再起動する必要はありません。 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] では、SharePoint の SPUserCodeV4 サービスが自動的にトリガーおよび制御する SPUCWorkerProcess プロセスにデバッガーをアタッチします。 SPUCWorkerProcess プロセスをリサイクルして最新バージョンのソリューションを読み込む必要はありません。

## <a name="either-type-of-solution"></a>両方の種類のソリューション
 どちらのソリューションの種類でも、[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] ではデバッガーをブラウザーにアタッチして、クライアント側のスクリプトのデバッグを有効にします。 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] では、この目的のためにスクリプト デバッグ エンジンを使用します。 スクリプトのデバッグを有効にするには、プロンプトが表示されたときに既定のブラウザーの設定を変更する必要があります。

 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] では、現在のサイトを実行している W3WP または SPUCWorkerProcess プロセスにのみデバッガーをアタッチします。 また、[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] では、マネージド COM Plus とワークフロー デバッグ エンジンもアタッチします。

## <a name="see-also"></a>関連項目
- [SharePoint ソリューションをデバッグする](../sharepoint/debugging-sharepoint-solutions.md)
- [SharePoint ソリューションのビルドとデバッグ](../sharepoint/building-and-debugging-sharepoint-solutions.md)
- [サンドボックス ソリューションの考慮事項](../sharepoint/sandboxed-solution-considerations.md)
