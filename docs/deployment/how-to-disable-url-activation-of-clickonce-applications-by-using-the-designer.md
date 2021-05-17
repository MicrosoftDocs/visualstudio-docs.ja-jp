---
title: デザイナーを使用して ClickOnce アプリケーションの URL アクティべーションを無効にする
description: Visual Studio を使用して ClickOnce アプリケーションの自動起動を無効にし、ユーザーが [スタート] メニューからアプリケーションを起動する必要があるようにする方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- disallowURLActivation
- URL activation, ClickOnce applications
- ClickOnce deployment, URL activation
ms.assetid: a337a582-e67c-409a-b52e-607cd1a8fc57
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 520f9aea1dbd3d3f742293a95b4dd7bdbac62a3b
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99900758"
---
# <a name="how-to-disable-url-activation-of-clickonce-applications-by-using-the-designer"></a>方法: デザイナーを使用して ClickOnce アプリケーションの URL アクティベーションを無効にする
通常、[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションは Web サーバーからインストールされた直後に自動的に起動します。 ただし、セキュリティ上の理由から、この動作を無効にすることもできます。その場合は、 **[スタート]** メニューからアプリケーションを起動するようにユーザーに通知します。 次の手順では、URL アクティベーションを無効にする方法を説明します。

 この手法は、Web サーバーからユーザーのコンピューターにインストールされた [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションにのみ使用できます。 URL を使用する方法でのみ起動できるオンライン専用のアプリケーションには使用できません。 オンライン専用アプリケーションとインストールされたアプリケーションの違いの詳細については、「[ClickOnce 配置ストラテジの選択](../deployment/choosing-a-clickonce-deployment-strategy.md)」を参照してください。

 この手順では [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] を使用します。 このタスクは、[!INCLUDE[winsdklong](../deployment/includes/winsdklong_md.md)] を使用して実行することもできます。 詳細については、「[方法: ClickOnce アプリケーションの URL アクティベーションを無効にする](../deployment/how-to-disable-url-activation-of-clickonce-applications.md)」を参照してください。

## <a name="procedure"></a>手順

#### <a name="to-disable-url-activation-for-your-application"></a>アプリケーションの URL アクティベーションを無効にするには

1. **ソリューション エクスプローラー** でご利用のプロジェクト名を右クリックし、 **[プロパティ]** をクリックします。

2. **[プロパティ]** ページの **[発行]** タブをクリックします。

3. **[オプション]** をクリックします。

4. **[マニフェスト]** をクリックします。

5. **URL からアプリケーションがアクティブ化されるのを禁止する** チェックボックスをオンにします。

6. アプリケーションをデプロイします。

## <a name="see-also"></a>関連項目
- [ClickOnce アプリケーションの発行](../deployment/publishing-clickonce-applications.md)