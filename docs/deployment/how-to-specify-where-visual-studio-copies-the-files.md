---
title: ファイルのコピー先を指定する | Microsoft Docs
description: ClickOnce アプリケーションの Publish Location プロパティを設定する方法について説明します。これはアプリケーション ファイルとマニフェストが配置される場所を指定します。
ms.custom:
- SEO-VS-2020
- seodec18
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- publishing, specifying location
- Publish Location property
ms.assetid: 6c552700-dda3-49fe-af98-4717344fda07
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 50f3e5d8500e57dd336919a5da58af094db97169
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99887420"
---
# <a name="how-to-specify-where-visual-studio-copies-the-files"></a>方法: Visual Studio がファイルをコピーする場所を指定する
ClickOnce を使用してアプリケーションを発行する場合、`Publish Location` プロパティによってアプリケーション ファイルとマニフェストが配置される場所が指定されます。 これには、ファイル パスまたは FTP サーバーへのパスを指定できます。

 **[プロジェクト デザイナー]** の **[発行]** ページで、または、発行ウィザードを使用して `Publish Location` プロパティを指定することができます。 詳細については、「[方法: 発行ウィザードを使用して ClickOnce アプリケーションを発行する](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md)」を参照してください。

> [!NOTE]
> ClickOnce を使用してアプリケーションの複数のバージョンをインストールすると、以前のバージョンのアプリケーションは、指定した発行場所の Archive というフォルダーに移されます。 以前のバージョンがこのようにアーカイブされることで、インストール ディレクトリが以前のバージョンのフォルダーから分離されます。

### <a name="to-specify-a-publishing-location"></a>発行場所を指定するには

1. **ソリューション エクスプローラー** でプロジェクトを選択し、 **[プロジェクト]** メニューの **[プロパティ]** をクリックします。

2. **[公開]** タブをクリックします。

3. **[発行場所]** フィールドに、次の形式のいずれかを使用して、発行場所を入力します。

   - ファイル共有またはディスク パスを発行するには、UNC パス ( *\\\Server\ApplicationName*) またはファイル パス (*C:\Deploy\ApplicationName*) のいずれかを使用して、パスを入力します。

   - FTP サーバーを発行するには、<em>ftp://ftp.microsoft.com/\<ApplicationName></em> の形式を使用して、パスを入力します。

     **[発行場所]** ボックスでは、テキストは参照 **[...]** ボタンが機能する順番で並んでいる必要があります。

## <a name="see-also"></a>関連項目
- [ClickOnce アプリケーションの発行](../deployment/publishing-clickonce-applications.md)
- [方法: 発行ウィザードを使用して ClickOnce アプリケーションを発行する](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md)