---
title: ClickOnce アプリケーションの既定の Web ページをカスタマイズする
description: ClickOnce アプリケーションを Web に発行するときに生成される Web ページについて説明します。これには、アプリケーションの名前とその他の情報が含まれています。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- Publish.htm Web page
- ClickOnce deployment default Web page
- deploying applications [ClickOnce], publishing
- publishing, ClickOnce
ms.assetid: 418de18c-bee9-4f24-9cd9-0252d175070d
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 0377bdc5fa38c814bb5cd6ff02d12dcec117266d
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99900783"
---
# <a name="how-to-customize-the-default-web-page-for-a-clickonce-application"></a>方法: ClickOnce アプリケーションの既定の Web ページをカスタマイズする
ClickOnce アプリケーションを Web に発行すると、Web ページが自動的に生成され、アプリケーションと共に発行されます。 既定のページには、アプリケーションの名前、およびアプリケーションをインストールする、前提条件をインストールする、または MSDN 上のヘルプへアクセスするためのリンクが含まれます。

> [!NOTE]
> ページに表示される実際のリンクは、ページが表示されているコンピューターと、含める前提条件によって異なります。

 Web ページの既定の名前は *Publish.htm* です。**プロジェクト デザイナー** で名前を変更できます。 詳細については、「[方法: ClickOnce アプリケーションの発行ページを指定する](../deployment/how-to-specify-a-publish-page-for-a-clickonce-application.md)」を参照してください。

 *Publish.htm* Web ページは、新しいバージョンが検出された場合にのみ発行されます。

> [!NOTE]
> **発行** 設定に加えた変更は、*Publish.htm* ページに影響しませんが、1 つ例外があります。最初の発行後に前提条件を追加または削除した場合、前提条件の一覧は正確ではなくなります。 変更内容を反映するには、前提条件リンクのテキストを編集する必要があります。

### <a name="to-customize-the-publish-web-page"></a>Web の発行ページをカスタマイズするには

1. ClickOnce アプリケーションを Web の場所に発行します。 詳細については、「[方法: 発行ウィザードを使用して ClickOnce アプリケーションを発行する](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md)」を参照してください。

2. Web サーバーで、Visual Web Designer または他の HTML エディターで *Publish.htm* ファイルを開きます。

3. 必要に応じてページをカスタマイズして保存します。

4. 省略可能。 カスタマイズされた Web 発行ページが Visual Studio によって上書きされないようにするには、 **[発行オプション]** ダイアログ ボックスで **[発行後に毎回配置 Web ページを自動的に生成する]** チェック ボックスをオフにします。

## <a name="see-also"></a>関連項目
- [ClickOnce のセキュリティと配置](../deployment/clickonce-security-and-deployment.md)
- [ClickOnce アプリケーションの発行](../deployment/publishing-clickonce-applications.md)
- [方法: ClickOnce アプリケーションと共に必須コンポーネントをインストールする](../deployment/how-to-install-prerequisites-with-a-clickonce-application.md)
- [方法: ClickOnce アプリケーションの発行ページを指定する](../deployment/how-to-specify-a-publish-page-for-a-clickonce-application.md)