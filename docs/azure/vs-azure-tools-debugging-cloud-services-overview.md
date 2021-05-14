---
title: Azure Cloud Services のデバッグのオプション | Microsoft Docs
description: Azure Cloud Services のデバッグ
author: mikejo5000
manager: jmartens
ms.topic: conceptual
ms.workload: azure-vs
ms.date: 03/18/2017
ms.author: mikejo
ms.technology: vs-ide-debug
ms.openlocfilehash: 12b327c65b83acde09eeac748d614ca560f3e012
ms.sourcegitcommit: 5654b7a57a9af111a6f29239212d76086bc745c9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/03/2021
ms.locfileid: "101683085"
---
# <a name="learn-the-various-ways-to-debug-an-azure-cloud-service"></a>Azure クラウド サービスをデバッグするためのさまざまな方法を理解する
この記事では、Azure クラウド サービスをデバッグするさまざまな方法へのリンクを提供します。

## <a name="debugging-an-azure-cloud-service-in-visual-studio"></a>Visual Studio で Azure クラウド サービスをデバッグする
Azure コンピューティング エミュレーターを使用してローカル コンピューターでクラウド サービスをデバッグすれば、時間とコストの節約になります。 サービスをデプロイする前にローカルでデバッグすると、コンピューティング時間の料金を支払うことなく、信頼性とパフォーマンスを改善できます。 ただし、一部には Azure でクラウド サービスを実行した場合にのみ発生するエラーもあります。 Azure でクラウド サービスを実行するときにのみ発生するエラーは、サービスの発行時にリモート デバッグを有効にしてから、ロール インスタンスにデバッガーをアタッチすることでデバッグできます。 詳細については、「 [ローカル コンピューターでクラウド サービスをデバッグする](vs-azure-tools-debug-cloud-services-virtual-machines.md#debug-your-cloud-service-on-your-local-computer)」を参照してください。

## <a name="using-intellitrace"></a>IntelliTrace の使用
Visual Studio Enterprise を使用して .NET Framework 4.5 を対象とするロールを作成する場合は、Visual Studio から Azure クラウド サービスをデプロイする時点で IntelliTrace を有効にすることができます。 IntelliTrace が提供するログを使用すると、Azure で実行しているかのようにアプリケーションを Visual Studio でデバッグすることができます。 詳細については、「 [IntelliTrace および Visual Studio を使用した発行済みのクラウド サービスのデバッグ](vs-azure-tools-intellitrace-debug-published-cloud-services.md)」を参照してください。

## <a name="remote-debugging"></a>リモート デバッグ
Visual Studio からクラウド サービスをデプロイするときに、そのリモート デバッグを有効にできます。 デプロイメントのリモート デバッグを有効にすると、各ロール インスタンスを実行する仮想マシンにリモート デバッグ サービスがインストールされます。 `msvsmon.exe` をはじめとするこれらのサービスは、パフォーマンスに影響せず、追加コストも発生しません。 詳細については、「 [Azure でクラウド サービスをデバッグする](vs-azure-tools-debug-cloud-services-virtual-machines.md#debug-a-cloud-service-in-azure)」を参照してください。

## <a name="next-steps"></a>次のステップ
- [Visual Studio での Azure クラウド サービスまたは仮想マシンのデバッグ](./vs-azure-tools-debug-cloud-services-virtual-machines.md) - Azure クラウド サービスをデバッグする方法の詳細を説明します。
