---
title: '方法: 変更、ClickOnce アプリケーションの発行の言語 |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- Publish language property
- ClickOnce deployment, changing publish language
- publishing, ClickOnce
ms.assetid: ef5024c4-cda1-4970-bc75-32a2a10c92c3
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 7e5bf51fd416fd9ccbb2343c17412984858429da
ms.sourcegitcommit: 1fc6ee928733e61a1f42782f832ead9f7946d00c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2019
ms.locfileid: "60115290"
---
# <a name="how-to-change-the-publish-language-for-a-clickonce-application"></a>方法: ClickOnce アプリケーションの発行言語を変更する

発行するときに、[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]アプリケーション、ユーザー インターフェイスの言語と開発用コンピューターのカルチャの既定のインストール中に表示されます。 ローカライズされたアプリケーションを発行する場合は、言語とローカライズされたバージョンと一致するカルチャを指定する必要があります。 これによって決定されますが、`Publish language`プロジェクトのプロパティ。

`Publish language`でプロパティを設定できる、**発行オプション**からアクセスできるダイアログ ボックス、**発行**のページ、**プロジェクト デザイナー**します。

> [!NOTE]
>  実際に画面に表示されるダイアログ ボックスとメニュー コマンドは、アクティブな設定またはエディションによっては、ヘルプの説明と異なる場合があります。 設定を変更するには、 **[ツール]** メニューの **[設定のインポートとエクスポート]** をクリックします。 詳細については、「[リセット設定](../ide/environment-settings.md#reset-settings)」を参照してください。

## <a name="to-change-the-publish-language"></a>発行の言語を変更するには

1. **ソリューション エクスプ ローラー**でプロジェクトを選択し、 **[プロジェクト]** メニューの **[プロパティ]** をクリックします。

2. **発行**タブをクリックします。

3. **オプション**ボタンをクリックして、**発行オプション** ダイアログ ボックスを開きます。

4. **説明**をクリックします。

5. **発行オプション** ダイアログ ボックスで、言語を選択し、カルチャから、**発行の言語**ドロップダウン リストをクリック**OK**します。

## <a name="see-also"></a>関連項目

- [ClickOnce アプリケーションの発行](../deployment/publishing-clickonce-applications.md)
- [方法: 発行ウィザードを使用して ClickOnce アプリケーションを発行する](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md)