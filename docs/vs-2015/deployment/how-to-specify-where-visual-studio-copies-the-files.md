---
title: '方法: Visual Studio 2015 のコピーのファイルの場所の指定 |Microsoft Docs'
titleSuffix: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-deployment
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- publishing, specifying location
- Publish Location property
ms.assetid: 6c552700-dda3-49fe-af98-4717344fda07
caps.latest.revision: 14
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 6b9f44f3d4f1a9d1b110501d0178e0e2e8dc4e47
ms.sourcegitcommit: 8b538eea125241e9d6d8b7297b72a66faa9a4a47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/23/2019
ms.locfileid: "58977709"
---
# <a name="how-to-specify-where-visual-studio-copies-the-files"></a>方法: Visual Studio がファイルをコピーする場所を指定する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

ClickOnce を使用してアプリケーションを発行する場合、`Publish Location` プロパティによってアプリケーション ファイルとマニフェストが配置される場所が指定されます。 これには、ファイル パスまたは FTP サーバーへのパスを指定できます。

 **[プロジェクト デザイナー]** の **[発行]** ページで、または、発行ウィザードを使用して `Publish Location` プロパティを指定することができます。 詳細については、「[方法 :発行ウィザードを使用して ClickOnce アプリケーションを発行する](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md)」を参照してください。

> [!NOTE]
>  ClickOnce を使用してアプリケーションの複数のバージョンをインストールすると、以前のバージョンのアプリケーションは、指定した発行場所の Archive というフォルダーに移されます。 以前のバージョンがこのようにアーカイブされることで、インストール ディレクトリが以前のバージョンのフォルダーから分離されます。

### <a name="to-specify-a-publishing-location"></a>発行場所を指定するには

1. **ソリューション エクスプ ローラー**でプロジェクトを選択し、 **[プロジェクト]** メニューの **[プロパティ]** をクリックします。

2. **発行**タブをクリックします。

3. **[発行場所]** フィールドに、次の形式のいずれかを使用して、発行場所を入力します。

   - にファイル共有またはディスク パスを発行するには、UNC パスを使用してパスを入力 (\\\Server\ApplicationName) またはファイル パス (C:\Deploy\ApplicationName)。

   - FTP サーバーを発行するには、ftp://ftp.microsoft.com/ApplicationName という形式を使用して、パスを入力します。

     **[発行場所]** ボックスでは、テキストは参照 **[...]** ボタンが機能する順番で並んでいる必要があります。

## <a name="see-also"></a>関連項目
 [ClickOnce アプリケーションの発行](../deployment/publishing-clickonce-applications.md)[方法。発行ウィザードを使用して ClickOnce アプリケーションを発行する](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md)
