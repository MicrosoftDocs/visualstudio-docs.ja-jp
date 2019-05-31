---
title: デザイナーを使用する ClickOnce アプリの URL アクティべーションを無効にします。
ms.date: 11/04/2016
ms.topic: conceptual
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
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: b8296f08c29b3259c19393a860ee34f6c3f05a42
ms.sourcegitcommit: 117ece52507e86c957a5fd4f28d48a0057e1f581
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/28/2019
ms.locfileid: "66263275"
---
# <a name="how-to-disable-url-activation-of-clickonce-applications-by-using-the-designer"></a>方法: デザイナーを使用して ClickOnce アプリケーションの URL アクティベーションを無効にする
通常、 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] Web サーバーからインストールした後すぐに、アプリケーションが自動的に開始されます。 セキュリティ上の理由から、この動作を無効にしてからアプリケーションを起動するユーザーに通知すること可能性があります、**開始** メニューの代わりにします。 次の手順では、URL アクティベーションを無効にする方法を説明します。

 この手法は、Web サーバーからユーザーのコンピューターにインストールされた [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションにのみ使用できます。 その URL を使用してのみ開始できますオンライン専用アプリケーションを使用できません。 詳細とインストールされているオンライン専用アプリケーションの違いについては、次を参照してください。 [ClickOnce 配置ストラテジの選択](../deployment/choosing-a-clickonce-deployment-strategy.md)します。

 この手順では[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]します。 使用してこのタスクを実行することもできます、[!INCLUDE[winsdklong](../deployment/includes/winsdklong_md.md)]します。 詳細については、「[方法 :ClickOnce アプリケーションの URL アクティベーションを無効にする](../deployment/how-to-disable-url-activation-of-clickonce-applications.md)」を参照してください。

## <a name="procedure"></a>プロシージャ

#### <a name="to-disable-url-activation-for-your-application"></a>アプリケーションの URL アクティベーションを無効にするには

1. プロジェクト名を右クリックして**ソリューション エクスプ ローラー**、 をクリック**プロパティ**します。

2. **プロパティ** ページで、をクリックして、**発行**タブ。

3. **[オプション]** をクリックします。

4. クリックして**マニフェスト**します。

5. チェック ボックスをオン**URL 経由でアクティブ化からアプリケーションをブロック**します。

6. アプリケーションを配置します。

## <a name="see-also"></a>関連項目
- [ClickOnce アプリケーションの発行](../deployment/publishing-clickonce-applications.md)