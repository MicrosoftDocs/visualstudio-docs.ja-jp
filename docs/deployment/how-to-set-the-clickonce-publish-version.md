---
title: ClickOnce の発行バージョンを設定する | Microsoft Docs
description: アプリケーションが更新プログラムかどうかを指定する、ClickOnce の [発行するバージョン] プロパティを設定する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- ClickOnce deployment, setting publish version
- publishing, ClickOnce
- Publish Version property
ms.assetid: 06f15504-6385-40a6-b01d-cd90ca36dc73
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 71d74d8b16e058b150187a231a1f3a7323c0c612
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99885028"
---
# <a name="how-to-set-the-clickonce-publish-version"></a>方法: ClickOnce の発行バージョンを設定する
[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] の `Publish Version` プロパティでは、発行するアプリケーションを更新プログラムとして扱うかどうかを指定します。 バージョンがインクリメントされるたびに、アプリケーションは更新プログラムとして発行されます。

 `Publish Version` プロパティは、**プロジェクト デザイナー** の **[発行]** ページで設定できます。

> [!NOTE]
> アプリケーションが発行されるたびに `Publish Version` プロパティが自動的にインクリメントされるプロジェクト オプションがあります。このオプションは既定で有効になっています。 詳細については、「[方法: ClickOnce の発行バージョンを自動的にインクリメントする](../deployment/how-to-automatically-increment-the-clickonce-publish-version.md)」を参照してください。

### <a name="to-change-the-publish-version"></a>発行バージョンを変更するには

1. **ソリューション エクスプ ローラー** でプロジェクトを選択し、 **[プロジェクト]** メニューの **[プロパティ]** をクリックします。

2. **[公開]** タブをクリックします。

3. **[発行するバージョン]** フィールドで、 **[メジャー]** 、 **[マイナー]** 、 **[ビルド]** 、または **[リビジョン]** のバージョン番号をインクリメントします。

    > [!NOTE]
    > バージョン番号をデクリメントしないでください。これを行うと、予期しない更新動作が発生する可能性があります。

## <a name="see-also"></a>関連項目
- [ClickOnce の更新方法の選択](../deployment/choosing-a-clickonce-update-strategy.md)
- [方法: ClickOnce の発行バージョンを自動的にインクリメントする](../deployment/how-to-automatically-increment-the-clickonce-publish-version.md)
- [ClickOnce アプリケーションの発行](../deployment/publishing-clickonce-applications.md)
- [方法: 発行ウィザードを使用して ClickOnce アプリケーションを発行する](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md)