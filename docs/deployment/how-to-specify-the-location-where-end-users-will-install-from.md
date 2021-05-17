---
title: エンド ユーザーがインストールを開始する場所を指定する
description: 発行された ClickOnce アプリケーションがインストール用にホストされる場所である Installation URL プロパティを設定する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- deploying applications [ClickOnce], specifying an installation URL
- URLs, specifying an installation URL
- installation, specifying installation an URL
- Installation URL property
ms.assetid: 04a804bf-ed55-4a7a-a1e6-f63ed99c0276
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 61c81ab15a3f4f6ec89d1b37a2c96d963bbdf67b
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99900408"
---
# <a name="how-to-specify-the-location-where-end-users-will-install-from"></a>方法: エンド ユーザーがインストールを開始する場所を指定する

[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションを発行する場合、ユーザーがアプリケーションをダウンロードしてインストールする場所は、必ずしもアプリケーションが最初に発行される場所とは限りません。 たとえば、一部の組織では、開発者がアプリケーションをステージング サーバーに発行した後、管理者がアプリケーションを Web サーバーに移動する場合があります。

この場合、`Installation URL` プロパティを使用して、ユーザーがアプリケーションをダウンロードするためにアクセスする Web サーバーを指定できます。 これは、アプリケーション マニフェストが更新プログラムを検索する場所を認識するために必要です。

`Installation URL` プロパティは、**プロジェクト デザイナー** の **[発行]** ページで設定できます。

> [!NOTE]
> `Installation URL` プロパティは、**発行ウィザード** を使用して設定することもできます。 詳細については、「[方法: 発行ウィザードを使用して ClickOnce アプリケーションを発行する](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md)」を参照してください。

### <a name="to-specify-an-installation-url"></a>インストール URL を指定するには

1. **ソリューション エクスプローラー** でプロジェクトを選択し、 **[プロジェクト]** メニューの **[プロパティ]** をクリックします。

2. **[公開]** タブをクリックします。

3. [インストール URL] フィールドに、形式 `https://www.contoso.com/ApplicationName` を使用する完全修飾 URL を使用して、または形式 `\Server\ApplicationName` を使用する UNC パスを使用して、インストールの場所を入力します。

## <a name="see-also"></a>関連項目
- [方法: Visual Studio がファイルをコピーする場所を指定する](../deployment/how-to-specify-where-visual-studio-copies-the-files.md)
- [ClickOnce アプリケーションの発行](../deployment/publishing-clickonce-applications.md)
- [方法: 発行ウィザードを使用して ClickOnce アプリケーションを発行する](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md)