---
title: 配置の更新用に別の場所を指定する
description: 配置マニフェストで ClickOnce アプリケーションの更新プログラム用に別の場所を指定する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- ClickOnce deployment, updates
- deployment update, alternative locations
ms.assetid: 7faacd35-2638-492d-80f6-6b57e5f820de
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: f0832105ccc203dd046461e40d27f8d50efc3009
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99940372"
---
# <a name="how-to-specify-an-alternate-location-for-deployment-updates"></a>方法: 配置の更新用に別の場所を指定する
最初に CD またはファイル共有から [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションをインストールできますが、アプリケーションでは Web で定期的な更新プログラムを確認する必要があります。 配置マニフェストで更新プログラム用に別の場所を指定して、アプリケーションが最初のインストール後に Web から自身を更新できるようにすることができます。

> [!NOTE]
> この機能を使用するには、アプリケーションをローカルにインストールするように構成する必要があります。 詳細については、「[チュートリアル: ClickOnce アプリケーションを手動で配置する](../deployment/walkthrough-manually-deploying-a-clickonce-application.md)」を参照してください。 さらに、ネットワークから [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションをインストールする場合、別の場所を設定すると、[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] では初回インストールとそれ以降のすべての更新プログラムに対してその場所が使用されます。 アプリケーションをローカルにインストールする場合 (たとえば CD から)、初回インストールは元のメディアを使用して実行され、それ以降のすべての更新プログラムでは代替の場所が使用されます。

### <a name="specify-an-alternate-location-for-updates-by-using-mageuiexe-windows-forms-based-utility"></a>MageUI.exe (Windows フォームベースのユーティリティ) を使用して、更新プログラム用に別の場所を指定する

1. .NET Framework コマンド プロンプトを開き、以下を入力します。

     **mageui.exe**

2. **[ファイル]** メニューの **[開く]** をクリックして、アプリケーションの配置マニフェストを開きます。

3. **[配置オプション]** タブを選択します。

4. **[起動場所]** という名前のテキスト ボックスに、アプリケーションの更新プログラムの配置マニフェストが格納されるディレクトリの URL を入力します。

5. 配置マニフェストを保存します。

### <a name="specify-an-alternate-location-for-updates-by-using-mageexe"></a>Mage.exe を使用して、更新プログラム用に別の場所を指定する

1. .NET Framework コマンド プロンプトを開きます。

2. 次のコマンドを使用して、更新プログラムの場所を設定します。 この例で、*HelloWorld.exe.application* は [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーション マニフェストのパスで、常にアプリケーション拡張子を持ちます。`http://adatum.com/Update/Path` は [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] がアプリケーションの更新プログラムをチェックする URL です。

    **Mage -Update HelloWorld.exe.application -ProviderUrl http:\//adatum.com/Update/Path**

3. ファイルを保存します。

   > [!NOTE]
   > 次に、*Mage.exe* を使用してファイルに署名し直す必要があります。 詳細については、「[チュートリアル: ClickOnce アプリケーションを手動で配置する](../deployment/walkthrough-manually-deploying-a-clickonce-application.md)」を参照してください。

## <a name="net-framework-security"></a>.NET Framework のセキュリティ
 CD などのオフライン メディアからアプリケーションをインストールし、コンピューターがオンラインの場合、[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] ではまず、配置マニフェストの `<deploymentProvider>` タグで指定された URL を確認して、更新プログラムの場所により新しいバージョンのアプリケーションが含まれているかどうかを判断します。 含まれている場合、[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] では、初回インストール ディレクトリからではなく、そこからアプリケーションを直接インストールします。また、共通言語ランタイム (CLR) によって、`<deploymentProvider>` を使用してアプリケーションの信頼レベルが決定されます。 コンピューターがオフラインである場合、または `<deploymentProvider>` にアクセスできない場合、[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] では CD からインストールし、CLR ではインストール場所に基づいて信頼を付与します。CD からのインストールの場合、アプリケーションが完全な信頼を付与されることを意味します。 それ以降のすべての更新プログラムは、その信頼レベルを継承します。

 `<deploymentProvider>` を使用するすべての [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションで、必要なアクセス許可をアプリケーション マニフェストで明示的に宣言して、アプリケーションが異なるコンピューターで異なる信頼レベルを付与されないようにする必要があります。

## <a name="see-also"></a>関連項目
- [チュートリアル: ClickOnce アプリケーションを手動で配置する](../deployment/walkthrough-manually-deploying-a-clickonce-application.md)
- [ClickOnce 配置マニフェスト](../deployment/clickonce-deployment-manifest.md)
- [ClickOnce アプリケーションのセキュリティ保護](../deployment/securing-clickonce-applications.md)
- [ClickOnce の更新方法の選択](../deployment/choosing-a-clickonce-update-strategy.md)