---
title: '方法: ClickOnce アプリケーションの URL アクティべーションを無効にする |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- disallowUrlActivation
- URL activation, ClickOnce applications
- ClickOnce deployment, URL activation
ms.assetid: db31a16b-960f-4264-91d7-c7c40f876068
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 6841b8a91cec24f467f6e3f684cbb27e25c9fa63
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "62899350"
---
# <a name="how-to-disable-url-activation-of-clickonce-applications"></a>方法: ClickOnce アプリケーションの URL アクティベーションを無効にする

通常、[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションは Web サーバーからインストールされた直後に自動的に起動します。 ただし、セキュリティ上の理由から、この動作を無効にすることもできます。その場合は、**[スタート]** メニューからアプリケーションを起動するようにユーザーに通知します。 次の手順では、URL アクティベーションを無効にする方法を説明します。

この手法は、Web サーバーからユーザーのコンピューターにインストールされた [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションにのみ使用できます。 URL を使用する方法でのみ起動できるオンライン専用のアプリケーションには使用できません。 オンライン専用アプリケーションとインストールされたアプリケーションの違いの詳細については、「[ClickOnce 配置ストラテジの選択](../deployment/choosing-a-clickonce-deployment-strategy.md)」を参照してください。

この手順では、Windows ソフトウェア開発キット (SDK) ツールの MageUI.exe を使用します。 このツールの詳細については、次を参照してください。 [MageUI.exe (Manifest Generation and Editing Tool, Graphical Client)](/dotnet/framework/tools/mageui-exe-manifest-generation-and-editing-tool-graphical-client)します。 Visual Studio を使用してこの手順を実行することもできます。

## <a name="procedure"></a>プロシージャ

### <a name="to-disable-url-activation-for-your-application"></a>アプリケーションの URL アクティベーションを無効にするには

1. MageUI.exe で配置マニフェストを開きます。 まだ作成していない 1 つ場合の手順に従います[チュートリアル。ClickOnce アプリケーションを手動で展開](../deployment/walkthrough-manually-deploying-a-clickonce-application.md)します。

2. **[配置オプション]** タブを選択します。

3. **[インストール後にアプリケーションを自動的に実行する]** チェックボックスをオフにします。

4. マニフェストを保存し、署名します。

## <a name="see-also"></a>関連項目

- [ClickOnce アプリケーションの発行](../deployment/publishing-clickonce-applications.md)