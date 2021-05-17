---
title: ClickOnce 配置 API を使用したアプリの自動更新
description: ApplicationDeployment クラスを使用して、ユーザー要求などのイベントに基づいて更新を確認するコードを ClickOnce で記述する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- ClickOnce deployment, updates
- application updates
ms.assetid: 1a886310-67c8-44e5-a382-c2f0454f887d
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: db82151b7fd4dbe894cecf8fbf5f5b64cb2f5919
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/02/2021
ms.locfileid: "106213941"
---
# <a name="how-to-check-for-application-updates-programmatically-using-the-clickonce-deployment-api"></a>方法: ClickOnce 配置 API を使用してアプリケーションの更新プログラムをプログラムで確認する
ClickOnce には、アプリケーションを配置した後に更新する 2 つの方法が用意されています。 最初の方法では、特定の間隔で更新を自動的にチェックするように ClickOnce 配置を構成できます。 2 つ目の方法では、<xref:System.Deployment.Application.ApplicationDeployment> クラスを使用して、ユーザー要求などのイベントに基づいて更新をチェックするコードを記述できます。

 次の手順に、プログラムによる更新を実行するためのコードを示しています。さらに、プログラムによる更新チェックを有効にするように、ClickOnce 配置を構成する方法についても説明しています。

 ClickOnce アプリケーションをプログラムで更新するには、更新プログラムの場所を指定する必要があります。 これは配置プロバイダーと呼ばれることもあります。 このプロパティの設定の詳細については、「[ClickOnce の更新方法の選択](../deployment/choosing-a-clickonce-update-strategy.md)」を参照してください。

> [!NOTE]
> 以下に示す手法を使用して、ある場所からアプリケーションを配置するが、別の場所からそれを更新することもできます。 詳細については、「[方法: 配置の更新用に別の場所を指定する](../deployment/how-to-specify-an-alternate-location-for-deployment-updates.md)」を参照してください。

### <a name="to-check-for-updates-programmatically"></a>プログラムによって更新プログラムをチェックするには

1. 任意のコマンドラインまたはビジュアル ツールを使用して、新しい Windows フォーム アプリケーションを作成します。

2. ユーザーに、更新プログラムをチェックするために選択させる任意のボタン、メニュー項目、またはその他のユーザー インターフェイス項目を作成します。 その項目のイベント ハンドラーから、更新プログラムをチェックしてインストールする次のメソッドを呼び出します。

    :::code language="csharp" source="../snippets/csharp/VS_Snippets_Winforms/ClickOnceAPI/CS/Form1.cs" id="Snippet6":::
    :::code language="cpp" source="../snippets/cpp/VS_Snippets_Winforms/ClickOnceAPI/cpp/form1.cpp" id="Snippet6":::
    :::code language="vb" source="../snippets/visualbasic/VS_Snippets_Winforms/ClickOnceAPI/VB/Form1.vb" id="Snippet6":::

3. アプリケーションをコンパイルします。

### <a name="use-mageexe-to-deploy-an-application-that-checks-for-updates-programmatically"></a>Mage.exe を使用して、プログラムによって更新プログラムをチェックするアプリケーションを展開する

- 「[チュートリアル: ClickOnce アプリケーションを手動で配置する](../deployment/walkthrough-manually-deploying-a-clickonce-application.md)」で説明されているように、Mage.exe を使用してアプリケーションを配置する手順に従います。 Mage.exe を呼び出して、配置マニフェストを生成する場合は、コマンドライン スイッチ `providerUrl` を使用し、ClickOnce によって更新プログラムをチェックする URL を指定してください。 アプリケーションから更新する場合`http://www.adatum.com/MyApp`、たとえば、配置マニフェストを生成する呼び出しが、これのようになります。

    ```cmd
    mage -New Deployment -ToFile WindowsFormsApp1.application -Name "My App 1.0" -Version 1.0.0.0 -AppManifest 1.0.0.0\MyApp.manifest -providerUrl http://www.adatum.com/MyApp/MyApp.application
    ```

### <a name="using-mageuiexe-to-deploy-an-application-that-checks-for-updates-programmatically"></a>MageUI.exe を使用して、プログラムによって更新プログラムをチェックするアプリケーションを展開する

- 「[チュートリアル: ClickOnce アプリケーションを手動で配置する](../deployment/walkthrough-manually-deploying-a-clickonce-application.md)」で説明されているように、Mage.exe を使用してアプリケーションを配置する手順に従います。 **[配置オプション]** タブで、 **[開始場所]** フィールドを、アプリケーション マニフェスト ClickOnce によって更新プログラムがチェックされるように設定します。 **[更新オプション]** タブで、 **[このアプリケーションの更新プログラムを確認する]** チェック ボックスをオフにします。

## <a name="net-framework-security"></a>.NET Framework のセキュリティ
 プログラムによる更新を使用するには、アプリケーションに完全信頼アクセス許可が必要です。

## <a name="see-also"></a>関連項目
- [方法: 配置の更新用に別の場所を指定する](../deployment/how-to-specify-an-alternate-location-for-deployment-updates.md)
- [ClickOnce の更新方法の選択](../deployment/choosing-a-clickonce-update-strategy.md)
- [ClickOnce アプリケーションの発行](../deployment/publishing-clickonce-applications.md)